# WiFi & Bluetooth

The Kumquat board is equipped with an **ESP32 module** for both WiFi and Bluetooth functionality. The ESP32 uses the **Espressif esp-hosted-ng firmware**, and the necessary kernel modules are pre-installed on the system. This guide provides an overview of how to connect to a WiFi network using the `NetworkManager` service and how to manage Bluetooth connections.

## Key Features

- **WiFi Interface**: The WiFi interface on the Kumquat board is named `espsta0`.
- **Bluetooth Interface**: The Bluetooth interface is named `hci0`.
- **Firmware**: The ESP32 is controlled via the Espressif esp-hosted-ng firmware.

## Using WiFi with `NetworkManager`

The Kumquat board uses the standard `NetworkManager` service to manage WiFi connections. Here’s how to connect to a WiFi network and enable internet access.

### Checking the WiFi Interface

First, check if the `espsta0` interface is up and running:

```sh
nmcli device status
```

This should show `espsta0` listed as a WiFi device. If it’s not listed, you may need to bring the interface up manually:

```sh
ip link set espsta0 up
```

### Scanning for Available Networks

To scan for nearby WiFi networks:

```sh
nmcli device wifi list
```

This command will output a list of available WiFi networks. Note the SSID of the network you wish to connect to.

### Connecting to a WiFi Network

To connect to a WiFi network, use the following command:

```sh
nmcli device wifi connect "<SSID>" password "<password>"
```

Replace `<SSID>` with the name of your network and `<password>` with the network’s password.

Once connected, you can verify the connection with:

```sh
nmcli connection show
```

This will display the active network connections, including the one established via `espsta0`.

### Verifying Internet Access

After successfully connecting, test the internet connection by pinging a reliable external server:

```sh
ping 8.8.8.8
```

You should receive a response if the connection is successful.

## Using Bluetooth (`hci0`)

The Kumquat board supports Bluetooth through the **hci0** interface, managed by the `BlueZ` stack, which is pre-installed. Below are some common Bluetooth operations such as scanning, pairing, and connecting to devices.

### Bringing Up the Bluetooth Interface

Ensure the Bluetooth interface is up by running:

```sh
hciconfig hci0 up
```

### Scanning for Bluetooth Devices

To scan for nearby Bluetooth devices, use the following command:

```sh
hcitool scan
```

This will output a list of discoverable devices, showing their MAC addresses and device names. Note the MAC address of the device you wish to connect to.

### Pairing with a Bluetooth Device

Once you have the device's MAC address, you can initiate pairing using `bluetoothctl`, a command-line utility to manage Bluetooth devices.

1. Start the `bluetoothctl` tool:

    ```sh
    bluetoothctl
    ```

2. Enter pairing mode:

    ```sh
    agent on
    default-agent
    ```

3. Scan for devices again within `bluetoothctl`:

    ```sh
    scan on
    ```

4. Pair with the device by specifying its MAC address:

    ```sh
    pair XX:XX:XX:XX:XX:XX
    ```

   Replace `XX:XX:XX:XX:XX:XX` with the actual MAC address of the Bluetooth device.

5. To connect after pairing, use:

    ```sh
    connect XX:XX:XX:XX:XX:XX
    ```

6. Trust the device for automatic connections in the future:

    ```sh
    trust XX:XX:XX:XX:XX:XX
    ```

7. Finally, exit `bluetoothctl`:

    ```sh
    exit
    ```

### Verifying the Bluetooth Connection

You can verify that the Bluetooth device is connected by running:

```sh
hciconfig hci0
```

This will provide information on the current state of the Bluetooth interface, including any active connections.

## Summary

The Kumquat board offers robust WiFi and Bluetooth support through its integrated ESP32 module. Using standard tools like `NetworkManager` and `bluetoothctl`, you can easily connect to WiFi networks and pair with Bluetooth devices. The board’s dual connectivity capabilities make it ideal for embedded IoT projects requiring wireless communication.

For more advanced uses, refer to the [BlueZ Bluetooth stack documentation](https://www.kernel.org/pub/linux/bluetooth/) and the [NetworkManager documentation](https://networkmanager.dev/docs/).
