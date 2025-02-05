# Network Booting the Kumquat Board (TFTP, DHCP, and NFS)

This guide explains how to set up a network boot environment for the Kumquat board for development or testing purposes. In this configuration, the board will boot over the network using TFTP for the kernel and device tree, DHCP for IP assignment, and NFS for the root filesystem.

---

## Requirements

- A **Linux system** with a spare network interface (USB, PCI, etc.)
- **Buildroot output** containing:
  - `zImage` (Kernel)
  - `sun8i-v3s-netcube-kumquat.dtb` (Device Tree Blob)
  - `rootfs.ext4` (Root filesystem image)
- A **TFTP directory** with the following structure:

  ```
  tftpd
  ├── pxelinux.cfg
  │   └── default-arm-sunxi
  ├── sun8i-v3s-netcube-kumquat.dtb
  └── zImage
  ```

- The **default PXELINUX configuration file** (`default-arm-sunxi`) should contain:

  ```
  LABEL default
    kernel zImage
    fdt sun8i-v3s-netcube-kumquat.dtb
    append root=/dev/nfs nfsroot=192.168.100.50:/mnt/netboot,tcp,v3 ip=dhcp console=${console} rootfstype=ext4 panic=3 ${mtdparts}
  ```

- **NFS export** for the root filesystem.

---

## 1. Install Required Packages

Install all necessary packages in one command:

```bash
sudo apt update && sudo apt install -y nfs-kernel-server dnsmasq
```

---

## 2. Configure the NFS Server

1. **Create the Export Directory**

   Create the mount point for the root filesystem:

   ```bash
   sudo mkdir -p /mnt/netboot
   ```

2. **Edit `/etc/exports`**

   Add the following line to `/etc/exports`:

   ```
   /mnt/netboot 192.168.100.0/24(rw,no_subtree_check,no_root_squash)
   ```

3. **Apply the Export Changes**

   Reload the export table:

   ```bash
   sudo exportfs -ra
   ```

4. **Mount the Root Filesystem**

   Mount the Buildroot rootfs image to the export directory:

   ```bash
   sudo mount -t ext4 output/images/rootfs.ext4 /mnt/netboot
   ```

   > **Note:** Replace `output/images/rootfs.ext4` with the actual path to your rootfs image.

---

## 3. Set Up the TFTP Boot Environment

1. **Create the TFTP Directory Structure**

   In your working directory, create a folder named `tftpd` with the following structure:

   ```bash
   mkdir -p tftpd/pxelinux.cfg
   ```

2. **Copy the Required Files**

   Copy the `zImage` and `sun8i-v3s-netcube-kumquat.dtb` from your Buildroot output:

   ```bash
   cp output/images/zImage tftpd/
   cp output/images/sun8i-v3s-netcube-kumquat.dtb tftpd/
   ```

3. **Create the PXELINUX Configuration File**

   Create a file named `default-arm-sunxi` inside the `tftpd/pxelinux.cfg` directory with the following content:

   ```bash
   cat <<EOF > tftpd/pxelinux.cfg/default-arm-sunxi
   LABEL default
     kernel zImage
     fdt sun8i-v3s-netcube-kumquat.dtb
     append root=/dev/nfs nfsroot=192.168.100.50:/mnt/netboot,tcp,v3 ip=dhcp console=\${console} rootfstype=ext4 panic=3 \${mtdparts}
   EOF
   ```

   > **Placeholder for configuration image:**
   >
   > ![PXELINUX Config File](placeholder_image_link)

---

## 4. Configure and Start dnsmasq

Set your spare Ethernet port to a **static IP of 192.168.100.50/24**. For example, if your interface is `ethX`:

```bash
sudo ip addr add 192.168.100.50/24 dev ethX
```

> **Note:** Replace `ethX` with the correct interface name.

Now, start **dnsmasq** to provide DHCP and TFTP services:

```bash
sudo dnsmasq --port=0 \
  --dhcp-range=192.168.100.100,192.168.100.200,12h \
  --enable-tftp --tftp-root=$PWD/tftpd \
  --log-dhcp --log-queries --log-facility=/dev/stdout \
  --no-daemon --listen-address=192.168.100.50
```

> **Note:** `$PWD/tftpd` is the full path to your TFTP directory.

---

## 5. Boot the Kumquat Board

With the NFS export, TFTP directory, and dnsmasq running:

1. **Power on the Kumquat board** (ensure no bootable USB stick or SD card is inserted, or that they are non-bootable).
2. The board's **U-Boot** will attempt network boot:
   - It will use DHCP to get an IP address.
   - It will retrieve the kernel (`zImage`) and device tree (`sun8i-v3s-netcube-kumquat.dtb`) via TFTP.
   - It will mount the NFS export as the root filesystem.

### **Example Boot Log**

```
U-Boot SPL 2024.10 (Jan 22 2025 - 20:15:31 +0100)
DRAM: 64 MiB
Trying to boot from sunxi SPI

U-Boot 2024.10 (Jan 22 2025 - 20:15:31 +0100) Allwinner Technology

CPU:   Allwinner V3s (SUN8I 1681)
Model: NetCube Systems Kumquat
DRAM:  64 MiB
Net:   eth0: ethernet@1c30000
Hit any key to stop autoboot:  0 
ethernet@1c30000 Waiting for PHY auto negotiation to complete. done
BOOTP broadcast 1
DHCP client bound to address 192.168.100.109 (13 ms)
Using ethernet@1c30000 device
TFTP from server 192.168.100.50; our IP address is 192.168.100.109
Filename 'pxelinux.cfg/default-arm-sunxi'.
Load address: 0x41a00000
Loading: #
   46.9 KiB/s
done
Bytes transferred = 195 (c3 hex)
Retrieving file: zImage
Using ethernet@1c30000 device
TFTP from server 192.168.100.50; our IP address is 192.168.100.109
Filename 'zImage'.
Load address: 0x41000000
Loading: ####################################################
done
Bytes transferred = 6042920 (5c3528 hex)
append: root=/dev/nfs nfsroot=192.168.100.50:/mnt/netboot,tcp,v3 ip=dhcp console=ttyS0,115200 rootfstype=ext4 panic=3 mtdparts=...
Retrieving file: sun8i-v3s-netcube-kumquat.dtb
Using ethernet@1c30000 device
TFTP from server 192.168.100.50; our IP address is 192.168.100.109
Filename 'sun8i-v3s-netcube-kumquat.dtb'.
Load address: 0x41800000
Loading: ##
done
Bytes transferred = 17367 (43d7 hex)
Kernel image @ 0x41000000 [ 0x000000 - 0x5c3528 ]
## Flattened Device Tree blob at 41800000
   Booting using the fdt blob at 0x41800000
Working FDT set to 41800000
   Loading Device Tree to 42d40000, end 42d473d6 ... OK
Working FDT set to 42d40000

Starting kernel ...

[    0.000000] Booting Linux on physical CPU 0x0
[    0.000000] Linux version 6.12.11 (build details...) #2 SMP Tue Jan 28 22:26:13 CET 2025
...
```

---

## Troubleshooting

- **TFTP Errors:**  
  Check the dnsmasq logs for missing or misnamed files. Ensure the `tftpd` directory contains `zImage`, `sun8i-v3s-netcube-kumquat.dtb`, and the PXELINUX configuration in `pxelinux.cfg/default-arm-sunxi`.

- **DHCP Issues:**  
  Verify the static IP is set correctly on your spare network interface (`192.168.100.50/24`) and that dnsmasq is listening on this address.

- **NFS Mount Problems:**  
  Confirm the NFS export is active with:

  ```bash
  sudo showmount -e localhost
  ```
