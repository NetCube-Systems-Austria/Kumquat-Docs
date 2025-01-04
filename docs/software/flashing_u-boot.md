# Flashing U-Boot onto the SPI-NOR

This guide provides detailed steps to flash U-Boot onto the SPI-NOR of the Kumquat board using the **sunxi-fel** tool. This process requires a host computer and the Kumquat board connected via USB.

## Prerequisites

Before starting, ensure you have the following:

- **Host Computer Requirements:**
  - A serial terminal application (e.g., Putty, Minicom).
  - **sunxi-fel** installed on the host system, with the necessary udev rules or run as root.
  - The new **nor-flash.img** file, either built yourself or downloaded from the releases page:
    
    [Download nor-flash.img](https://git.netcubesystems.at/NetCube-Systems-Austria/kumquat-buildroot-releases/releases)

- **Hardware Requirements:**
  - A USB-C console cable.
  - A USB-C OTG cable (one cable is sufficient, but two are recommended to avoid swapping ports).

## Step-by-Step Instructions

### Step 1: Enter the Bootloader

1. Connect the Kumquat board to your host computer using the USB-C console cable.
2. Power on the Kumquat board and monitor the serial terminal.
3. When prompted, press any key in the terminal to interrupt the boot process and enter the U-Boot bootloader.

*Note: If there is no bootloader on the board, you can skip to Step 3.*

### Step 2: Prepare the SPI-NOR Flash for FEL Mode

1. In the U-Boot bootloader, run the following commands to erase the boot area of the SPI-NOR flash:

   ```
   sf probe
   sf erase 0 0x1000
   reset
   ```

2. The system will reboot. Since the boot area is erased, the SoC will automatically enter **FEL Mode**.

### Step 3: Flash the SPI-NOR with the New U-Boot Image

1. Connect the Kumquat board to your host computer using the USB-OTG port.
2. On the host computer, run the following command to flash the **nor-flash.img** onto the SPI-NOR:

   ```
   sunxi-fel -p spiflash-write 0 nor-flash.img
   ```

3. Once flashing is complete, reboot the Kumquat board using:

   ```
   sunxi-fel wdreset
   ```

   The board should now boot into the new U-Boot.

### Troubleshooting

- If **sunxi-fel** reports no device or no access, try running the same command again. In some cases, it may take a few attempts to successfully communicate with the device.

### Notes

- Ensure the **sunxi-fel** tool is correctly installed on your host system. If running without udev rules, use `sudo` for all commands.
- Always verify the integrity of the **nor-flash.img** file before flashing.

By following these steps, you can successfully flash the U-Boot bootloader onto the SPI-NOR of the Kumquat board.

