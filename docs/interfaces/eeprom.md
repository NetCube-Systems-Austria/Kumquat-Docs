# EEPROM

The Kumquat comes equipped with an Electrically Erasable Programmable Read-Only Memory (EEPROM), a type of memory that retains stored data even when the power is turned off. Specifically, it features a 24AA02E48 2Kb EEPROM with a Pre-Programmed EUI-48 MAC ID, offering non-volatile memory capabilities. This EEPROM is connected to the primary I2C bus at the address 0x50. This guide outlines the process of storing and retrieving custom data in the EEPROM for your specific needs.

## Information

This EEPROM contains the MAC-Address of the System in the Read-Only lower 1Kb section. Only the upper 1Kb of memory is writeable by the user

## Checking if the EEPROM is detected

To check if the EEPROM is connected we can let Linux print the name of the loaded driver using the following command:

```
cat /sys/class/i2c-dev/i2c-0/device/0-0050/name
```

If the EEPROM is detected the expected result is 24c02.

## Writing to the EEPROM

To write to the EEPROM, you can utilize the kernel's built-in EEPROM driver.

You can write a string to the EEPROM using the `echo` command to write data directly to the appropriate sysfs file. For example, to write the string "Hello, EEPROM!" to the start of an EEPROM connected to I2C bus `i2c-0` at address `0x50`, you can use the following command:

```
echo -n -e "Hello, EEPROM!" > /sys/class/i2c-dev/i2c-0/device/0-0050/eeprom
```

The `eeprom` file in the device directory represents the EEPROM, and writing data to it will store the string at the beginning of the EEPROM's memory.

### Reading from the EEPROM

Similarly, you can read a string from the EEPROM using the kernel's built-in EEPROM driver. To read the string, you can simply read the content of the `eeprom` file corresponding to the start of the EEPROM's memory. For example, to read the string stored at the beginning of an EEPROM connected to I2C bus `i2c-0` at address `0x50`, you can use the following command:

```
cat /sys/class/i2c-dev/i2c-0/device/0-0050/eeprom
```

This command will output the string "Hello, EEPROM!" stored at the start of the EEPROM on I2C bus `i2c-0`.

By leveraging the kernel's built-in EEPROM driver and accessing the sysfs interface, you can write and read strings from an I2C EEPROM directly within the Linux environment, without relying on external tools.