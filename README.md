# Documentation

## ESP32
* Bluetooth classic and BLE supported by ESP-IDF using bluedroid: [docs](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-reference/bluetooth/index.html). Bluetooth Classic is required for the game controller.
* NimBLE only supports BLE (vibrators, glasses)
* Using [Rust ESP-IDF template](https://github.com/esp-rs/esp-idf-template) should offer everything ESP-IDF exposes, with C and Rust mixed

## LoRa
The [Lilygo Lora32 board](https://www.lilygo.cc/products/lora3) contains a [SX1276 LoRa chip](https://www.semtech.com/products/wireless-rf/lora-connect/sx1276) from Semtech.

## Rust on ESP
Following the [Rust on ESP Book](https://esp-rs.github.io/book/introduction.html) using the standard library (ESP-IDF)

### 3. Development Environment
The Lilygo LoRa32 board is powered by an ESP32 chip from xtensa. Follow the [specific instructions](https://esp-rs.github.io/book/installation/riscv-and-xtensa.html).

* 3.3 espup
* 3.4 std dev requirements

### 4 Application
From `esp-idf-template`

In directory `esp32-lilygo/lilygo-hello-world`

`cargo run`
