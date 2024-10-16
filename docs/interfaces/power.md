# Power Supply

The power supply for the Kumquat board is provided through a single terminal block. This document explains how to connect the power supply and provides information about the fuse used for protection.

## Connector Pinout Description

| Location | Description  |
| -------- | ------------ |
| X1.1     | M (Negative) |
| X1.2     | L+ (Positive)|

![Power Supply Connector Location](placeholder_image_link)

## Prerequisites

Before connecting the power supply, ensure you have the following:

- A 12V or 24V power supply capable of delivering at least 1 Amp of current.

## Hardware Setup

1. **Connect the Power Supply**:

   - Connect the positive terminal of the power supply to the `L+` terminal.
   - Connect the negative terminal of the power supply to the `M` terminal.

2. **Power On**:

   - Once connected, turn on the power supply. The Kumquat board should begin booting immediately.

![Power Supply Setup](placeholder_image_link)

## Fuse (F1)

The Kumquat board is equipped with a preinstalled 3 Amp Slow Blow fuse (F1). This fuse protects the board's wiring from short circuits or overloads.

![Fuse Location](placeholder_image_link)

### Replacement Information
If you need to replace the fuse, ensure the replacement matches the specifications of the original. The replacement part can be ordered from most suppliers. 

**Replacement Part Number**:
[Littelfuse 0453003](https://www.littelfuse.de/products/fuses/surface-mount-fuses/nano-2-fuses/453/453003.aspx)

## Note on 13w24b Revision Boards

**Important**: Boards with the 13w24b revision have a known bug in the Digital IO section, which causes them to get hotter than usual when using a 24V power supply. If you are using this revision, consider using a 12V supply to avoid excessive heat.
