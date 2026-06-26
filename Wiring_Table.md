# Wiring Table

## Exact Connections

| Module | Module Pin | ESP32 Pin | Signal | Protocol / Type |
| --- | --- | --- | --- | --- |
| BME280 | SDA | GPIO21 | SDA | I2C data |
| BME280 | SCL | GPIO22 | SCL | I2C clock |
| BME280 | VCC | 3.3V | Power | 3.3 V supply |
| BME280 | GND | GND | Ground | Common ground |
| SSD1306 OLED | SDA | GPIO21 | SDA | I2C data |
| SSD1306 OLED | SCL | GPIO22 | SCL | I2C clock |
| SSD1306 OLED | VCC | 3.3V | Power | 3.3 V supply |
| SSD1306 OLED | GND | GND | Ground | Common ground |
| Wind Speed Sensor | Signal | GPIO15 | Pulse | Digital interrupt |
| Wind Speed Sensor | VCC | 3.3V | Power | 3.3 V supply |
| Wind Speed Sensor | GND | GND | Ground | Common ground |

## Bus Notes

- BME280 and SSD1306 OLED share the same I2C bus.
- GPIO21 is the ESP32 SDA line.
- GPIO22 is the ESP32 SCL line.
- All modules must share a common ground.
- The wind sensor signal is read as a digital pulse input on GPIO15.
- Firmware enables `INPUT_PULLUP` for the wind sensor pin.

## Default I2C Addresses

| Device | Address |
| --- | --- |
| BME280 | `0x76` |
| SSD1306 OLED | `0x3C` |

