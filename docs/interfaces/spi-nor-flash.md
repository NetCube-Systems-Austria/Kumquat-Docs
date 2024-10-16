# SPI-Nor Flash

The Kumquat board includes an 8MB SPI-Nor Flash memory chip, the Winbond W25Q64JVSIQ. This memory is used to store critical components like the bootloader (U-Boot) and its environment variables, along with providing additional storage for user data. The flash memory is managed using `mtdparts` and divided into several partitions.

## Information

The SPI-Nor Flash contains the following partitions:

- **Bootloader (U-Boot)**: A read-only partition for the bootloader.
- **U-Boot Environment (env1 and env2)**: Two redundant partitions for U-Boot configuration.
- **User Partition**: A partition available for storing user data.

The current configuration is as follows:

```
mtdparts=firmware:512k(u-boot)ro,256k(u-boot-env1),256k(u-boot-env2),-(user)
```

This setup assigns 512KB to U-Boot, 256KB each for U-Boot environment 1 and 2, and the remainder to the `user` partition.

## Checking if the SPI-Nor Flash is Detected

To verify the presence of the SPI-Nor Flash, you can list the MTD devices using the following command:

```sh
cat /proc/mtd
```

The expected output should resemble the following:

```sh
mtd0: 00080000 00010000 "u-boot"
mtd1: 00040000 00010000 "u-boot-env1"
mtd2: 00040000 00010000 "u-boot-env2"
mtd3: 00700000 00010000 "user"
```

The `user` partition (`mtd3` in this case) is where user data can be stored.

## Writing to the SPI-Nor Flash

To write data to the `user` partition of the SPI-Nor Flash, you can use standard Linux tools like `dd` for writing raw data to the MTD block device.

Here is an example of how to write a file to the `user` partition:

1. Prepare the file you want to store in the Flash.
2. Use `dd` to copy the file to the `user` partition:

```sh
dd if=mydata.bin of=/dev/mtd3 bs=4096
```

This writes the contents of `mydata.bin` to the `user` partition (`mtd3`), using a block size of 4096 bytes.

### Reading from the SPI-Nor Flash

To read data from the `user` partition, you can use `dd` to copy the contents to a file:

```sh
dd if=/dev/mtd3 of=readback.bin bs=4096
```

This command copies the content of the `user` partition to `readback.bin`. You can then inspect or process this file as needed.

Alternatively, you can display the content directly in the terminal:

```sh
cat /dev/mtd3
```

This command will print the raw contents of the `user` partition to the terminal.

## Summary of the Flash Layout

| MTD Block | Size   | Description        |
| --------- | ------ | ------------------ |
| mtd0      | 512KB  | U-Boot             |
| mtd1      | 256KB  | U-Boot Environment 1 |
| mtd2      | 256KB  | U-Boot Environment 2 |
| mtd3      | ~6MB   | User Partition     |

The SPI-Nor Flash on the Kumquat board is divided into fixed partitions, with the `user` partition available for data storage. By using standard Linux commands, you can write and read data to and from the SPI-Nor Flash without needing external tools like `flashcp`.
