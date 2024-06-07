# eMMC & SD-Card

The Kumquat features an SDIO interface accessible through a 2x10 1.27mm Pin Header. This interface is primarily intended for connecting storage devices such as SD cards or eMMC modules to the Kumquat. However, users also have the flexibility to utilize this interface for custom solutions. The following document outlines the pinout details of the SDIO Interface.

## Connector Pinout Description

| Location | Name | Description  | Location | Name  | Description         |
| -------- | ---- | ------------ | -------- | ----- | ------------------- |
| X16.1    | D0   | SDIO Data 0  | X16.2    | D1    | SDIO Data 1         |
| X16.3    | D2   | SDIO Data 2  | X16.4    | D3    | SDIO Data 3         |
| X16.5    | D4   | SDIO Data 4  | X16.6    | D5    | SDIO Data 5         |
| X16.7    | D6   | SDIO Data 6  | X16.8    | D7    | SDIO Data 7         |
| X16.9    | STRB | SDIO Strobe  | X16.10   | GND   | Ground              |
| X16.11   | CMD  | SDIO Command | X16.12   | CLK   | SDIO Clock          |
| X16.13   | -    | Reserved     | X16.14   | GND   | Ground              |
| X16.15   | -    | Reserved     | X16.16   | VCCQ  | IO Supply (+3.3V)   |
| X16.17   | RST  | Card Reset   | X16.18   | VCC   | Core Supply (+3.3V) |
| X16.19   | GND  | Ground       | X16.20   | GND   | Ground              |

![SDIO Connector Location](placeholder_image_link)