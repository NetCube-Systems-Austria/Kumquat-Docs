# USB-OTG Port

The Kumquat board features a USB On-The-Go (OTG) port via a USB-C connector that supports USB 2.0 dual-role functionality. This means the port can act either as a USB host or a USB device, depending on the mode selected. The mode switching is handled by the TUSB320 controller, which is managed directly by the Linux kernel.

| Location | Description         |
| -------- | ------------------- |
| X11      | USB-C OTG Connector |

![USB-OTG Connector Location](../../img/interfaces/connectors.png)

## Key Features

- **USB-C Connector**: Supports USB 2.0 protocol.
- **Dual Role Support**: Can function as both a USB host (for peripherals) and a USB device.
- **Power Supply**: In host mode, the port can supply 5V at 500mA to connected devices.
- **Mode Switching**: Automatically managed by the Linux kernel via the TUSB320 controller.

## Mode Switching with TUSB320

The TUSB320 controller allows the system to dynamically switch between USB host mode and USB device mode. In host mode, the Kumquat board can connect and power peripherals like keyboards, mice, or flash drives. In device mode, the board can act as a USB peripheral, such as a mass storage device or a serial device.

The Linux kernel automatically handles the negotiation between device and host modes based on the connected device.

## Sysfs Interface

The USB controller on the Kumquat board is the **Allwinner V3s MUSB** controller, which uses the Linux kernel's MUSB driver. You can access and manage USB OTG settings via the sysfs interface.

The typical path for the MUSB controller's sysfs interface will look something like:

```
/sys/class/udc/musb-hdrc.1.auto/
```

## Example 1: Using USB-OTG as a USB-Serial Device (Device Mode)

In this example, we will configure the Kumquat board to act as a USB-serial device when connected to a host computer using the OTG port.

### Steps to Configure USB-Serial Device

- **Connect the Kumquat Board to the Host PC**

   Use a USB Type-C cable to connect the USB-OTG port on the Kumquat board to the host PC.

- **Enable Device Mode**

   The Linux kernel should automatically detect the connection and switch the Kumquat board to device mode via the TUSB320 controller.

- **Load the USB Gadget Module**

   Load the **g_serial** module, which creates a USB serial device that can communicate with the host PC over the USB-OTG port.

   ```
   modprobe g_serial
   ```

- **Verify the USB Serial Device**

   After loading the module, the board will create a new serial device that the host PC can detect. You can check the created device by looking at `/dev`:

   ```
   ls /dev/ttyGS0
   ```

   The device `/dev/ttyGS0` should appear, representing the USB-serial interface on the Kumquat board.

- **Connect to the USB-Serial Device from the Host PC**

   On the host PC, open a terminal and use a serial communication program such as `screen` or `minicom` to connect to the serial device. For example:

   ```
   screen /dev/ttyUSB0 115200
   ```

   This command connects to the USB-serial device at a baud rate of 115200. You should now be able to send and receive data between the Kumquat board and the host PC.

- **Stop the USB Serial Device**

   To stop the USB-serial device and return to the previous configuration, unload the `g_serial` module:

   ```
   rmmod g_serial
   ```

## Example 2: Using USB-OTG as a USB Host (Connecting a USB Stick)

In this example, we will use the Kumquat board as a USB host to connect and access a USB storage device (such as a USB flash drive).

### Steps to Connect a USB Stick

- **Connect the USB Stick to the USB-OTG Port**

   Plug your USB stick into the USB-C OTG port using an appropriate adapter, if necessary.

- **Verify Device Detection**

   Use the `lsusb` command to verify that the USB stick has been detected by the Kumquat board:

   ```
   lsusb
   ```

   You should see output similar to the following, listing the USB stick:

   ```
   Bus 001 Device 002: ID 0781:5581 SanDisk Corp. 
   ```

- **Mount the USB Stick**

   First, create a mount point where the USB stick will be mounted:

   ```
   mkdir /mnt/usb
   ```

   Then, find the device name of the USB stick by using the `dmesg` or `lsblk` command:

   ```
   lsblk
   ```

   You should see a block device like `/dev/sda1`. Mount the USB stick to the mount point:

   ```
   mount /dev/sda1 /mnt/usb
   ```

- **Access Files on the USB Stick**

   You can now access files on the USB stick from the `/mnt/usb` directory:

   ```
   ls /mnt/usb
   ```

- **Unmount the USB Stick**

   After finishing, unmount the USB stick to safely remove it:

   ```
   umount /mnt/usb
   ```

## Power Considerations

When the Kumquat board operates in host mode, it can supply up to **500mA of current at 5V** to the connected device. This power is supplied directly via the USB-C connector, making it suitable for low-power USB devices.

However, ensure that the total current consumption of all connected devices does not exceed 500mA, as the board may become unstable or fail to power high-demand devices.

## Summary

The USB-OTG port on the Kumquat board provides flexible connectivity for both host and device roles, controlled by the TUSB320 IC. In host mode, the board can connect to and power external devices like USB sticks, while in device mode, it can function as a USB peripheral such as a serial interface. Mode switching is automatic, making the port versatile for a variety of embedded use cases.

For more advanced use cases, such as creating custom USB gadgets, consult the [Linux USB Gadget API documentation](https://www.kernel.org/doc/Documentation/usb/gadget_configfs.txt).
