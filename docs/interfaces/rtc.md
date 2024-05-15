# RTC

The Real Time Clock (RTC) on the Kumquat serves the basic purpose of keeping the time of day. The RTC can keep track of the year, month, date, weekday, hour, minute and seconds. This document will guide you on how to use the RTC on the Kumquat.

| Device Name | Description                                           |
| ----------- | ----------------------------------------------------- |
| /dev/rtc0   | DS3232 connected over I2C1 with battery backup on X15 |
| /dev/rtc1   | built in to SoC, disabled by default                  |

## Battery Connector

| Location | Name | Description   |
| -------- | ---- | ------------- |
| X15.1    | VBAT | Battery +     |
| X15.2    | GND  | Battery -     |

![Battery Connector Location](placeholder_image_link)

## Prerequisites
Before you begin, make sure you have the following:

- Backup Battery connected to Xn in order for the RTC to keep working when the board is powered off.

## Accessing the RTC

- With the following command, check that the RTC is detected correctly

```sh
cat /sys/class/rtc/rtc0/device/name
```

It's output should look something like this:

```sh
ds3232
```

- If the RTC is detected you can proceed to the next steps.

## Setting the Time

- Write the current system time to the RTC:

```sh
hwclock -w -f /dev/rtc0
```

- Read back the time stored in the RTC:

```sh
hwclock -r -f /dev/rtc0
```

## Testing the Backup Battery

- Now that you have set the RTC, you may power down the board using the following command:

```sh
poweroff
```

- Unplug the power supply from the Kumquat

- After about a minute you can connect the power supply again and boot into Buildroot

- Running the following command, should show you the accurately advanced time to when the board was powered off

```sh
hwclock -r -f /dev/rtc0
```

