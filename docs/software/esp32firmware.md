# Flashing the ESP32

This guide provides detailed steps to flash the ESP32 module on the Kumquat board. The ESP32 is used for WiFi and Bluetooth via the **ESP-Hosted-NG** firmware, which is provided by Espressif. To perform flashing or other configuration tasks, you must first stop the driver and disable the SDIO bus to gain control over the ESP32 strapping pins.

## Prerequisites

Before proceeding, ensure you have:

- **esptool.py**, **espefuse.py**, and **espsecure.py** pre-installed on the Kumquat demo image. These tools are available by default.
- A valid **ESP-Hosted-NG** firmware file. You can download the latest version using the following command:
  
  ```
  wget https://github.com/espressif/esp-hosted/releases/download/release%2Fng-v1.0.2/ESP-Hosted-NG_release_v1.0.2.tgz
  ```

- Extract the downloaded file:

  ```
  gzip -d ESP-Hosted-NG_release_v1.0.2.tgz
  tar -xvf ESP-Hosted-NG_release_v1.0.2.tart
  ```

- The **ESP-Hosted-NG** firmware is located inside `ESP-Hosted-NG_release_v1.0.2/esp32/sdio_only/`.

## Step-by-Step Instructions

### Step 1: Stop the ESP32 Driver

First, stop the running ESP-Hosted driver. This driver is responsible for WiFi and Bluetooth functionality on the ESP32:

```
/etc/init.d/S35esphosted stop
```

This will release control of the ESP32 and allow you to flash it.

### Step 2: Disable the SDIO Bus

You need to disable the SDIO bus because the **D0 strapping pin** of the ESP32 is controlled via the SDIO bus. Disabling the bus ensures that the ESP32 can enter bootloader mode without interference.

```
echo "1c10000.mmc" > /sys/bus/platform/drivers/sunxi-mmc/unbind
```

### Step 3: Set ESP32 to Bootloader Mode

Next, set the ESP32 to bootloader mode by adjusting the GPIO pins:

- Set the strapping pins to bootloader mode:

   ```
   gpioset $(gpiofind ESP_nBOOT)=0 && gpioset $(gpiofind ESP_D0)=0
   ```

- Reset the ESP32 to apply the changes:

   ```
   gpioset $(gpiofind ESP_nRST)=0 && gpioset $(gpiofind ESP_nRST)=1
   ```

At this point, the ESP32 is ready to be flashed.

### Step 4: Setting Flash Voltage (If Needed)

If you have replaced the ESP32 on the Kumquat board, you'll need to set the flash voltage to **3.3V** by burning the e-fuse.

- Run the following command during the bootloader mode:

   ```
   espefuse.py -p /dev/ttyS1 -b 115200 --chip esp32 set_flash_voltage 3.3V
   ```

- When prompted, type `BURN` in all caps to confirm and permanently burn the fuse. This step cannot be undone.

### Step 5: Flash the ESP-Hosted-NG Firmware

Once the ESP32 is in bootloader mode, you can flash the **ESP-Hosted-NG** firmware:

- Navigate to the firmware directory:

   ```
   cd ESP-Hosted-NG_release_v1.0.2/esp32/sdio_only/
   ```

- Erase the flash using `esptool.py`:

   ```
   esptool.py -p /dev/ttyS1 -b 115200 --chip esp32 erase_flash
   ```

- Run the flashing command using `esptool.py`:

   ```
   esptool.py -p /dev/ttyS1 -b 115200 --chip esp32 write_flash --flash_mode dio --flash_size detect --flash_freq 40m 0x1000 bootloader.bin 0x8000 partition-table.bin 0xd000 ota_data_initial.bin 0x10000 network_adapter.bin
   ```

### Step 6: Reset ESP32 to Normal Flashing Mode

After flashing the ESP32, reset the strapping pins back to normal operation:

```
gpioset $(gpiofind ESP_nBOOT)=0
```

Reset the ESP32 again to apply the changes:

```
gpioset $(gpiofind ESP_nRST)=0 && gpioset $(gpiofind ESP_nRST)=1
```

### Step 7: Re-enable the SDIO Bus

Rebind the SDIO bus to restore communication with the ESP32 module:

```
echo "1c10000.mmc" > /sys/bus/platform/drivers/sunxi-mmc/bind
```

### Step 8: Restart the ESP-Hosted Driver

Finally, restart the **ESP-Hosted** driver to enable WiFi and Bluetooth services:

```
/etc/init.d/S35esphosted start
```

## Summary

This guide covers the process of flashing the ESP32 on the Kumquat board. You'll need to stop the driver, disable the SDIO bus, and adjust GPIOs to put the ESP32 into bootloader mode. After flashing the firmware, reset the ESP32 and restore the SDIO bus and driver. If replacing the ESP32, don't forget to set the flash voltage using **espefuse.py**.