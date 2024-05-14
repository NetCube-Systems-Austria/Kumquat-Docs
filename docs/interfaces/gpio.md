# Inputs & Outputs

The Kumquat has various connectors with different functionalities. This document demonstrates how to use these connectors using gpiod's command-line tools.

## Connector Pinout Description

### X4 - 2 Relays

This connector features two relays:

| Location | Output Name | Description     |
| -------- | ----------- | --------------- |
| X4.1     | Q9          | Relay 1 (NO)    |
| X4.2     | Q9          | Relay 1 (COM)   |
| X4.3     | Q10         | Relay 2 (NO)    |
| X4.4     | Q10         | Relay 2 (COM)   |

### X5 - 2 Relays

This connector also features two relays:


| Location | Output Name | Description     |
| -------- | ----------- | --------------- |
| X5.1     | Q11         | Relay 3 (NO)    |
| X5.2     | Q11         | Relay 3 (COM)   |
| X5.3     | Q12         | Relay 4 (NO)    |
| X5.4     | Q12         | Relay 4 (COM)   |

### X6 - 4 Digital I/Os

This connector provides four Digital I/Os along with one Ground connection. Both input (In) and output (Qn) are available on the same pins:

| Pinout | Input Name | Output Name | Description   |
| ------ | ---------- | ----------- | ------------- |
| X6.1   | I1         | Q1          | Digital I/O 1 |
| X6.2   | I2         | Q2          | Digital I/O 2 |
| X6.3   | I3         | Q3          | Digital I/O 3 |
| X6.4   | I4         | Q4          | Digital I/O 4 |
| X6.5   | -          | -           | Ground        |

### X7 - 4 Digital I/Os

Similar to X6, this connector provides four Digital I/Os along with one Ground (COM) connection. Both input (In) and output (Qn) are available on the same pins:

| Pinout | Input Name | Output Name | Description   |
| ------ | ---------- | ----------- | ------------- |
| X7.1   | I5         | Q5          | Digital I/O 5 |
| X7.2   | I6         | Q6          | Digital I/O 6 |
| X7.3   | I7         | Q7          | Digital I/O 7 |
| X7.4   | I8         | Q8          | Digital I/O 8 |
| X7.5   | -          | -           | Ground        |

## Using gpiod's Command-Line Tools

### Controlling Digital I/Os

To control the digital I/Os connected to your board, we'll use gpiod's command-line tools along with gpiofind to dynamically locate the GPIO pins based on the In and Qn names.

For example, to set a Digital I/O pin to a specific value:

```sh
gpioset $(gpiofind Q1)=1
```

This command dynamically locates the GPIO pin associated with Digital I/O 1 (Q1) using gpiofind and then sets its value to high using gpioset.

Similarly, you can set the value of other Digital I/O pins:

```sh
gpioset $(gpiofind Q2)=0
```

This command sets the value of Digital I/O 2 (Q2) to low.

### Controlling Relays

To control the relays connected to your board, you can use `gpioset` in combination with gpiofind.

For example, to turn on Relay 1 (connected to Q9), you can use:

```sh
gpioset $(gpiofind Q9)=1
```

To turn it off:

```sh
gpioset $(gpiofind Q9)=0
```

### Reading Digital Inputs

You can also read the state of digital inputs using `gpioget`.

For example, to monitor the state of Digital Input 1 (connected to I1), you can use:

```sh
gpioget $(gpiofind I1)
```

This command will print the state of the input.