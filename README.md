# Documentation

## ESP32
* Bluetooth classic and BLE supported by ESP-IDF using bluedroid: [docs](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-reference/bluetooth/index.html). Bluetooth Classic is required for the game controller.
* NimBLE only supports BLE (vibrators, glasses)
* Using [Rust ESP-IDF template](https://github.com/esp-rs/esp-idf-template) should offer everything ESP-IDF exposes, with C and Rust mixed

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
