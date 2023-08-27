# Documentation

## ESP32
* Bluetooth classic and BLE supported by ESP-IDF using bluedroid: [docs](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-reference/bluetooth/index.html). Bluetooth Classic is required for the game controller.
* NimBLE only supports BLE (vibrators, glasses)
* Using [Rust ESP-IDF template](https://github.com/esp-rs/esp-idf-template) should offer everything ESP-IDF exposes, with C and Rust mixed

## OLED Screen
[SSD1306](https://docs.rs/ssd1306/latest/ssd1306/) and [embedded-graphics](https://docs.rs/embedded-graphics/latest/embedded_graphics/) libs.

* [I2C example](https://github.com/esp-rs/std-training/blob/main/advanced/i2c-sensor-reading/examples/part_1.rs)
* [SSD1306 + embedded-graphics example](https://github.com/jamwaffles/ssd1306/blob/master/examples/text_i2c.rs)

This just works! See project [oled-test](https://github.com/luciole-freeflight/rust-oled-test)

## LoRa
Using [sx127x_lora](https://docs.rs/sx127x_lora/latest/sx127x_lora/) crate.

Example: [Issue 13](https://github.com/mr-glt/sx127x_lora/issues/13)

Starting to work a bit. See project [lora-test](https://github.com/luciole-freeflight/rust-lora-test)
