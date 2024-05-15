# QWIIC

If the connectivity options on the Kumquat are insufficient for your project, you can expand its capabilities using the QWIIC I²C Bus.

This document provides descriptions of the connections available and instructions on how to check if your device is detected.

## Connector Pinout Description

| Location | Description | 
| -------- | ----------- |
| X13.1    | Ground      |
| X13.2    | +3.3V       |
| X13.3    | I2C_SDA     |
| X13.4    | I2C_SCL     |

| Location | Description | 
| -------- | ----------- |
| X14.1    | Ground      |
| X14.2    | +3.3V       |
| X14.3    | I2C_SDA     |
| X14.4    | I2C_SCL     |

![QWIIC Connector Locations](placeholder_image_link)

## Connecting the Qwiic Device

Connect your Qwiic device to one of the available Qwiic connectors on the Kumquat. Ensure that the connections are secure and that the device is powered properly.

## Checking for Connected Devices

Use the `i2cdetect` command to scan the I2C bus for connected devices. Replace `0` with the appropriate bus number if your I2C bus is different.

```sh
sudo i2cdetect -y 0
```

This command will display a grid showing the addresses of connected devices. The device address will be shown as a number if it is detected.

## Reading Data from the Device

Once the device is detected, you can use the `i2cget` command to read data from specific registers of the device. Replace `<device-address>` and `<register-address>` with the appropriate values for your device.

```sh
sudo i2cget -y 0 <device-address> <register-address>
```

This command will read a byte of data from the specified register of the device and display it in hexadecimal format.

## Writing Data to the Device

You can use the `i2cset` command to write data to specific registers of the device. Replace `<device-address>`, `<register-address>`, and `<data>` with the appropriate values for your device.

```sh
sudo i2cset -y 0 <device-address> <register-address> <data>
```

This command will write the specified byte of data to the specified register of the device.