# Documentation

## Rust
### Embassy RTOS
[Embassy Book](https://embassy.dev/book/dev/index.html)

## ESP32
* Bluetooth classic and BLE supported by ESP-IDF using bluedroid: [docs](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-reference/bluetooth/index.html). Bluetooth Classic is required for the game controller.
* NimBLE only supports BLE (vibrators, glasses)
* Using [Rust ESP-IDF template](https://github.com/esp-rs/esp-idf-template) should offer everything ESP-IDF exposes, with C and Rust mixed
* [Lilygo LoRa32](https://www.lilygo.cc/products/lora3) supports Bluetooth version 4.2

## Nordic nRF52840
* [nRF52840](https://www.nordicsemi.com/Products/nRF52840) supports Bluetooth 5.4 (BLE, etc.)
* For development, we can use the Nordic nrf52840-dongle
* For Luciole, we want to use te Seeed Xiao nrf52840 

### SoftDevices
Pre-compiled blobs of proprietary Nordic code. [Description](https://infocenter.nordicsemi.com/topic/ug_gsg_ses/UG/gsg/softdevices.html)
We need the nRF52840 to perform a Peripheral role in BLE.

#### [S140](https://infocenter.nordicsemi.com/topic/struct_nrf52/struct/s140.html)
* [Spec](https://infocenter.nordicsemi.com/pdf/S140_SDS_v2.1.pdf)
* Version 7.3.0 Id `0x123`
* Content of `memory.x`
    ```
    MEMORY
    {
      /* NOTE 1 K = 1 KiBi = 1024 bytes */
      /* These values correspond to the NRF52840 with Softdevices S140 7.3.0 */
      FLASH : ORIGIN = 0x00027000, LENGTH = 868K // Length = 0x100000 - 0x27000
      RAM : ORIGIN = 0x20020000, LENGTH = 128K
    }
    ```

### Nordic nrf52840 dongle
This uses `Open DFU` bootloader. We need `nrfutil` command to be able to flash it.
[Nordic Devzone Tutorial](https://devzone.nordicsemi.com/guides/short-range-guides/b/getting-started/posts/nrf52840-dongle-programming-tutorial)

For instance, for a binary called `blinky`:

* Make sure to update `memory.x` to account for the soft-device reserved flash and ram memory.
* Compile
    ```bash
    cargo build --bin blinky
    ```
    This generate an ELF file.
* Convert the ELF file into a hex file
    ```bash
    arm-none-eabi-objcopy -O ihex target/thumbv7em-none-eabi/debug/blinky blinky.hex
    ```
* Create a DFU package (SoftDevice s140 7.3 has version number 0x123). This supposes the softdevice already exists on the chip.
    ```bash
    nrfutil pkg generate --hw-version 52 --sd-req 0x123 --application blinky.hex --application-version 0 dfu.zip
    ```
* **Alternative** Create a DFU package with the application AND the softdevice
    ```bash
    nrfutil pkg generate --hw-version 52 --sd-req 0x00 --sd-id 0x123 --application blinky.hex --application-version 0 --softdevice s140_nrf52_7.3.0_softdevice.hex dfu.zip
    ```
* Put the dongle in DFU mode: press Reset once while plugged
* Flash the DFU package
    ```bash
    nrfutil dfu usb-serial -pkg dfu.zip -p /dev/ttyACM0 -b 115200
    ```

### Seed Xiao nrf52840
This uses the Arduino UF2 bootloader

* Compile
    ```bash
    cargo build --bin blinky
    ```
    This generate an ELF file.
* Convert the ELF file into a hex file
    ```bash
    arm-none-eabi-objcopy -O ihex target/thumbv7em-none-eabi/debug/blinky blinky.hex
    ```
* Convert the hex file to UF2 (to keep the offsets defined in `memory.x` )
    ```bash
    uf2conv.py blinky.hex -c -f 0xADA52840 -o blinky.uf2
    ```
* Put the dongle in DFU mode: quickly press Reset twice while plugged
* Copy UF2 files to XIAO
    ```bash
    cp blinky.uf2 /media/jlg/XIAO-SENSE
    ```
* Reset the XIAO


## Rust on ESP
Following the [Rust on ESP Book](https://esp-rs.github.io/book/introduction.html) using the standard library (ESP-IDF)

### 1. Development Environment
The Lilygo LoRa32 board is powered by an ESP32 chip from xtensa. Follow the [specific instructions](https://esp-rs.github.io/book/installation/riscv-and-xtensa.html).

* 3.3 espup
* 3.4 std dev requirements

### 2. Application
From `esp-idf-template`

In directory `esp32-lilygo/lilygo-hello-world`

`cargo run`

## OLED Screen
[SSD1306](https://docs.rs/ssd1306/latest/ssd1306/) and [embedded-graphics](https://docs.rs/embedded-graphics/latest/embedded_graphics/) libs.

* [I2C example](https://github.com/esp-rs/std-training/blob/main/advanced/i2c-sensor-reading/examples/part_1.rs)
* [SSD1306 + embedded-graphics example](https://github.com/jamwaffles/ssd1306/blob/master/examples/text_i2c.rs)

This just works! See project [oled-test](https://github.com/luciole-freeflight/rust-oled-test)

## LoRa
The [Lilygo Lora32 board](https://www.lilygo.cc/products/lora3) contains a [SX1276 LoRa chip](https://www.semtech.com/products/wireless-rf/lora-connect/sx1276) from Semtech.

Using [sx127x_lora](https://docs.rs/sx127x_lora/latest/sx127x_lora/) crate.

Example: [Issue 13](https://github.com/mr-glt/sx127x_lora/issues/13)

Starting to work a bit. See project [lora-test](https://github.com/luciole-freeflight/rust-lora-test)

## BLE

[Adafruit tutorial](https://learn.adafruit.com/introduction-to-bluetooth-low-energy)
