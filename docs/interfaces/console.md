# Serial Console

In this document you will find a guide on how to use PuTTY or GtkTerm to connect to the Serial Console on the Kumquat.

| Location | Description   |
| -------- | ------------- |
| X12      | USB Console   |

![USB Console Connector Location](../../img/interfaces/connectors.png)

## Prerequisites

Before you begin, ensure you have the following:

- USB Type-C Cable
- Computer running Windows or Linux

## Hardware Setup

Connect the USB Cable to the right USB Type-C connector on the Kumquat, and plug the other end of the cable into your computer

## Using PuTTY to Connect to a USB-Serial Interface

- **Download and Install PuTTY**: If you haven't already, download and install PuTTY from the official website: [PuTTY Download Page](https://www.putty.org/).

- **Connect the USB-Serial Adapter**: Connect the USB-Serial adapter to your Kumquat device and ensure that the drivers are properly installed on your computer.

- **Open PuTTY**: Launch PuTTY from your desktop or start menu.

- **Configure the Serial Connection**:
   - In the PuTTY Configuration window, select the "Serial" connection type.
   - In the "Serial line" field, enter the COM port to which your USB-Serial adapter is connected (e.g., COM1, COM2, etc.).
   - Set the "Speed" to 115200 baud.
   - Ensure that the "Data bits" are set to 8, "Stop bits" to 1, and "Parity" to None (8N1 configuration).
   - Click the "Open" button to start the serial connection.

- **Interact with the Kumquat**: Once the connection is established, you should see a terminal window where you can interact with the Kumquat device. You can now send commands and receive responses as needed.

## Using GtkTerm to Connect to a USB-Serial Interface

- **Install GtkTerm**: If GtkTerm is not already installed on your system, you can install it using your package manager. For example, on Ubuntu-based systems, you can install GtkTerm using the following command:
```
sudo apt-get install gtkterm
```

- **Connect the USB-Serial Adapter**: Connect the USB-Serial adapter to your Kumquat device and ensure that the drivers are properly installed on your computer.

- **Open GtkTerm**: Launch GtkTerm from your applications menu or terminal.

- **Configure the Serial Connection**:
   - In the GtkTerm window, go to "Configuration" > "Port" and select the appropriate serial port (e.g., /dev/ttyUSB0).
   - Set the "Baudrate" to 115200.
   - Set the "Data bits" to 8, "Stop bits" to 1, and "Parity" to None (8N1 configuration).
   - Click the "Open" button to establish the serial connection.

- **Interact with the Kumquat**: Once the connection is established, you should see a terminal window where you can interact with the Kumquat device. You can now send commands and receive responses as needed.


By following these steps, you can use PuTTY or GtkTerm to connect to the Kumquat and interact with the device via the serial connection.