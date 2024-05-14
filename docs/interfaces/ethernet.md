# Ethernet

The Kumquat has a single 10/100 Ethernet interface built in. This document shows you how to use this interface.

| Location | Description        |
| -------- | ------------------ |
| X10      | Ethernet Connector |

![Ethernet Connector Location](placeholder_image_link)

## Prerequisites

Before you begin, ensure you have the following:

- CAT5e (or better) RJ45 Cable
- Network connection with DHCP Server

## Ethernet Connection

Once you are connected to your Network you should be seeing the Yellow and Green LED's on the Ethernet connector indicating that a link has been established

By default the Kumquat is configured to get an IP-Address using DHCP

### Finding the IP Address of eth0

To find the IP address of eth0 on Linux, you can use the `ip` command. Open a terminal and type:

```sh
ip addr show eth0
```

This command will display the IP address, subnet mask, and other network information associated with the eth0 interface.

### Checking the Link State of eth0

To check the link state of eth0, you can again use the `ip` command:

```sh
ip link show eth0
```

This command will display the status of the eth0 interface, including whether it is up or down, and whether the link is connected or disconnected.

### Configuring Static IP Instead of DHCP

To configure a static IP address for eth0 instead of using DHCP, you need to edit the network configuration file. In Buildroot, this file is typically located in `/etc/network/interfaces`.

Open the network configuration file in a text editor:

```sh
nano /etc/network/interfaces
```

Add or modify the configuration for eth0 to specify a static IP address, subnet mask, gateway, and DNS servers. For example:

```
auto eth0
iface eth0 inet static
    address 192.168.1.100
    netmask 255.255.255.0
    gateway 192.168.1.1
    dns-nameservers 8.8.8.8 8.8.4.4
```

Replace `192.168.1.100` with the desired static IP address, `255.255.255.0` with the appropriate subnet mask, `192.168.1.1` with the gateway address, and `8.8.8.8` and `8.8.4.4` with the DNS server addresses.

Save the file and exit the text editor.

After making these changes, you need to restart the networking service to apply the new configuration:

```sh
/etc/init.d/network restart
```

This will bring up the eth0 interface with the configured static IP address.