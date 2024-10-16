# System Buttons and LEDs

The Kumquat is equipped with buttons and LEDs designed to assist users in tasks such as troubleshooting issues and monitoring system status. This document will provide descriptions of the locations and functions of these LEDs and buttons.

## Buttons

![Button Locations](../../img/interfaces/buttons-and-leds.png)

| Location | Name   | Description              |
| -------- | ------ | ------------------------ |
| SW101    | user   | User Programmable Button |
| SW102    | reset  | System Reset             |

### Using the User Button

The user button on the Kumquat is initially configured as a keyboard with only a single key. Your application can handle it just like any other keyboard input.

To test the functionality of the button, you can use the following command with `evtest`:

```
evtest /dev/input/by-path/platform-gpio-keys-event
```

When you press the user button, you should see messages appear for the keydown and keyup events. This allows you to verify that the button is functioning properly and capturing input events.

## LEDs

![LED Locations](../../img/interfaces/buttons-and-leds.png)

| Location | Name      | Description              |
| -------- | --------- | ------------------------ |
| D101     | disk      | Storage Activity on mmc0 |
| D102     | heartbeat | Processor Activity       |
| D103     | power     | Main 3.3V Supply Rail    |
| D301     | con-rx    | USB-Console Data Receive |
| D302     | con-tx    | USB-Console Data Send    |

### Reconfiguring the Disk or Heartbeat LEDs

If your project requires displaying simple status indications, you can reconfigure the disk and heartbeat LEDs to function as standard LEDs or display different statuses.

To identify the supported triggers for the LED, use the following command with either `green:disk` or `green:heartbeat` for the LED you wish to configure:

```
cat /sys/class/leds/green:heartbeat/trigger
```

This command will output a list of supported triggers, with the currently selected trigger surrounded by square brackets `[]`.

To change the trigger, use the following command:

```
echo "mmc1" > /sys/class/leds/green:heartbeat/trigger
```

This command will set the heartbeat LED to illuminate when there is activity on the mmc1 bus.

Additionally, you can set the trigger to `none` and manually control the LED state using the following commands:

```
echo 0 > /sys/class/leds/green:heartbeat/brightness # To turn the LED off

echo 1 > /sys/class/leds/green:heartbeat/brightness # To turn the LED on
```

These commands allow you to set the LED to a custom state as needed for your project requirements.