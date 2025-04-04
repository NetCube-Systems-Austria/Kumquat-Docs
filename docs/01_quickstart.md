# Quickstart Guide

## Introduction
Welcome to the quickstart guide for the Kumquat by NetCube Systems! This guide will walk you through the initial setup process to get your board up and running quickly. Whether you're a novice or an advanced user, follow these steps to start exploring the capabilities of your Kumquat board.

## Prerequisites
Before you begin, make sure you have the following:

- Kumquat board
- Kumquat Flash Adapter
- USB Type-C cable
- 12V or 24V power supply (with at least 1A of power)
- Computer capable of running a serial terminal application
- Micro-SD card and card reader

## Step 1: Prepare the SD Card
1. Insert the SD card into the card reader of your computer.

## Step 2: Download and Write Buildroot or Alpine Image
1. Download the latest example Buildroot image [here](https://git.netcubesystems.at/NetCube-Systems-Austria/kumquat-buildroot-releases/releases/tag/demo-build) or the Alpine Linux image [here](https://github.com/NetCube-Systems-Austria/Kumquat-Alpine-Linux/releases).
3. Use Balena Etcher (or similar tool) to write the Buildroot image to the SD card.

## Step 3: Insert SD Card into Kumquat Board
1. Eject the SD card from your computer.
2. Insert the SD card into the "Flash Module Adapter" provided with the Kumquat board.
3. Insert the adapter into the top right pin header (X16) just below the audio connectors on the Kumquat board.

![Insert Adapter](img/quickstart/insert-adapter.png)

## Step 4: Connect USB Cable
1. Connect one end of the USB cable to the right port (X12) of the Kumquat board.
2. Insert the other end of the USB cable into an available USB port on your computer.

![Connect USB Cable](img/quickstart/connect-console.png)

## Step 5: Open Serial Terminal

See [Serial Console](interfaces/console) for more Information

1. Open a serial terminal application such as PuTTY or GtkTerm on your computer.
2. Select the newly detected serial port with the following settings: 

    - Baud rate: 115200
    - Data bits: 8
    - Parity: None
    - Stop bits: 1

## Step 6: Connect Power Supply
1. Connect the 12V or 24V power supply to the bottom right terminal block (X1) of the Kumquat board.
2. Ensure that the positive pin of the power connector is on the right side.

![Connect Power Supply](img/quickstart/connect-power.png)

## Step 7: Boot up the Kumquat Board
1. Check the serial console for output.
2. You should see the start sequence: U-Boot Bootloader, followed by the Buildroot or Alpine Operating System.
3. After a few seconds, you should be prompted with a login. You can log in with the username `root`.
4. If you installed Alpine Linux, you may now also run `setup-alpine` to do basic system configuration.

## Conclusion
Congratulations! You have successfully set up your NetCube Systems Kumquat. Start exploring and experimenting with its capabilities. Refer to the next pages for more advanced usage and customization options.
