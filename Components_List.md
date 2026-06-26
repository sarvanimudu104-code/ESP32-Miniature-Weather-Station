# Components List

| Item | Quantity | Purpose | Notes |
| --- | ---: | --- | --- |
| ESP32 development board | 1 | Main controller | Lolin D32 or similar ESP32 board |
| BME280 sensor module | 1 | Temperature, humidity, pressure | I2C address used by firmware: `0x76` |
| SSD1306 OLED display | 1 | Local display | I2C address used by firmware: `0x3C` |
| Wind speed sensor / anemometer | 1 | Wind speed pulse input | Signal connected to GPIO15 |
| Jumper wires | As needed | Wiring | Use short wires for I2C reliability |
| Breadboard or prototype board | 1 | Assembly | Breadboard for demo, soldered board for final display |
| USB cable | 1 | Programming and power | Must support data, not charge-only |

Optional:

| Item | Quantity | Purpose | Notes |
| --- | ---: | --- | --- |
| 0.1 uF capacitor | 1 | Wind input debounce/noise reduction | Place close to signal input and ground |
| Pull-up resistor | 1 | Wind sensor signal conditioning | Only if the sensor module requires external pull-up |
| Enclosure | 1 | Demonstration quality | Keep BME280 exposed to ambient air |

