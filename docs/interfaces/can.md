# CAN Bus

The Kumquat offers two terminal blocks to access the isolated CAN-FD interface onboard. The following document describes how you can use SocketCAN to evaluate this bus.

SocketCAN provides a set of utilities for working with Controller Area Network (CAN) interfaces on Linux systems. 

## Connector Pinout Description

| Location | Description | 
| -------- | ----------- |
| X2.1     | CAN High    |
| X2.2     | CAN Low     |
| X2.3     | Shield      |

| Location | Description | 
| -------- | ----------- |
| X3.1     | CAN High    |
| X3.2     | CAN Low     |
| X3.3     | Shield      |

![CAN Bus Connector Locations](../../img/interfaces/connectors.png)

## Prerequisites

Before you begin, ensure you have the following:

- 120R Termination Resistor
- Secondary CAN Interface on another Computer using SocketCAN

## Hardware Setup

Connect the Termination Resistor to CAN-H and CAN-L onto on of the two CAN-Connectors on the Kumquat.

Connect your Computer's CAN-Interface to the other CAN-Connector on the Kumquat.

## Configuring and Setting Up SocketCAN Interface

### Configuring Bitrate

To configure the bitrate of the CAN interface, use the `ip` command with the `link` option:

```
ip link set can0 type can bitrate 500000
```

This command sets the bitrate of the `can0` interface to 500 kbit/s. Adjust the bitrate value as per your requirements.

### Setting Interface Up

To bring the CAN interface up, use the `ip` command:

```
ip link set can0 up
```

This command activates the `can0` interface and makes it operational for communication.

## Checking SocketCAN Interface

### Checking Interface Status

To check the status of your SocketCAN interface, use the `ip` command:

```
ip -details link show can0
```

This command displays detailed information about the `can0` interface, including its status and configuration.

### Checking CAN Interface Statistics

To view statistics for the CAN interface, use the `ip` command with the `stat` option:

```
ip -details link show can0 stat
```

This command provides statistics such as the number of transmitted and received frames, error counts, and interface state.

## Sending and Receiving CAN Frames

### Sending CAN Frames

To send CAN frames using SocketCAN, you can use the `cansend` command:

```
cansend can0 123#1122334455667788
```

This command sends a CAN frame with ID `123` and data `1122334455667788` on the `can0` interface.

### Receiving CAN Frames

To receive CAN frames, you can use the `candump` command:

```
candump can0
```

This command continuously monitors the `can0` interface and prints received CAN frames to the console.

## Analyzing CAN Traffic

### Filtering CAN Frames

You can filter CAN frames based on their ID using the `candump` command with filters:

```
candump can0,123:7FF
```

This command only displays CAN frames with ID `123` on the `can0` interface.

### Analyzing CAN Traffic with Wireshark

To analyze CAN traffic using Wireshark, first, capture CAN frames using `candump` and save them to a file:

```
candump can0 > can_traffic.log
```

Then, transfer the log file to a system with Wireshark installed and open it for analysis.