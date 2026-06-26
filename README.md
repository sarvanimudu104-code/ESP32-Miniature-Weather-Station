# ESP32 Weather Monitoring Station

Beginner-to-medium ESP32 weather monitoring station built for an ECE internship
portfolio. The project reads local environmental data from a BME280 sensor,
measures wind speed from a pulse sensor, and displays live readings, status
messages, and daily temperature range on an SSD1306 OLED.

The main firmware is in:

```text
/ESP32_Miniature_OLED_Weather_Station_SSD1306_v01/
```

## Project Overview

This project demonstrates a complete embedded sensing workflow:

```text
BME280 + Wind Sensor -> ESP32 -> Processing and Status Logic -> OLED Display
```

The ESP32 reads temperature, humidity, and pressure over I2C, captures wind
sensor pulses on GPIO15, applies simple threshold-based interpretation, and
updates a multi-page OLED interface. WiFi is used only for NTP date/time
synchronisation.

## Features

- ESP32-based embedded weather monitoring station.
- BME280 temperature, humidity, and pressure measurement.
- SSD1306 OLED display with three rotating data pages.
- Wind speed sensor using GPIO interrupt input.
- Pressure-based weather status:
  - `Sunny`
  - `Normal`
  - `Rain Possible`
- Temperature/humidity-based comfort status:
  - `Cold`
  - `Comfortable`
  - `Warm`
  - `Hot`
- Daily minimum and maximum temperature tracking.
- OLED error screen if the BME280 is not detected.
- NTP-based date and time display.

This project intentionally does not include MQTT, Firebase, cloud services,
mobile apps, OTA updates, AI, machine learning, deep sleep, or SD card logging.

## Hardware Components

See [Components_List.md](Components_List.md) for the full bill of materials.

Core components:

- ESP32 development board
- BME280 sensor module
- SSD1306 I2C OLED display
- Wind speed sensor / anemometer
- Jumper wires
- Breadboard or soldered prototype board

## Wiring Table

| Module | Module Pin | ESP32 Pin | Signal Type | Notes |
| --- | --- | --- | --- | --- |
| BME280 | SDA | GPIO21 | I2C data | Shared with OLED SDA |
| BME280 | SCL | GPIO22 | I2C clock | Shared with OLED SCL |
| BME280 | VCC | 3.3V | Power | Use 3.3 V |
| BME280 | GND | GND | Ground | Common ground |
| SSD1306 OLED | SDA | GPIO21 | I2C data | Shared with BME280 SDA |
| SSD1306 OLED | SCL | GPIO22 | I2C clock | Shared with BME280 SCL |
| SSD1306 OLED | VCC | 3.3V | Power | Use 3.3 V |
| SSD1306 OLED | GND | GND | Ground | Common ground |
| Wind Speed Sensor | Signal | GPIO15 | Digital interrupt | Rising-edge pulse input |
| Wind Speed Sensor | VCC | 3.3V | Power | Match the sensor module rating |
| Wind Speed Sensor | GND | GND | Ground | Common ground |

Detailed wiring documentation is available in
[Wiring_Table.md](Wiring_Table.md).

## Circuit Diagram

The GitHub-ready circuit diagram target is [circuit.png](circuit and related images/circuit.png).

## Working Principle

See [docs/Working_Principle.md](docs/Working_Principle.md) for the detailed
workflow.

Short version:

1. ESP32 starts I2C on GPIO21/GPIO22.
2. ESP32 checks for the BME280 at address `0x76`.
3. If BME280 is missing, the OLED displays a sensor error page.
4. If BME280 is detected, the ESP32 connects to WiFi for NTP time.
5. BME280 readings are converted into display units.
6. Wind sensor pulses are captured on GPIO15.
7. Firmware calculates wind speed and tracks daily temperature min/max.
8. OLED rotates between live readings, status, and daily range pages.

## Installation

1. Install ESP32 board support in Arduino IDE.
2. Install required libraries:
   - Adafruit BME280 Library
   - Adafruit Unified Sensor
   - ESP8266 and ESP32 OLED driver for SSD1306 displays
3. Open:

```text
firmware/ESP32_Miniature_OLED_Weather_Station_SSD1306_v01/
ESP32_Miniature_OLED_Weather_Station_SSD1306_v01.ino
```

4. Update these values near the top of the sketch:
   - `ssid`
   - `password`
   - `Timezone`
   - `pressure_offset`
   - `WS_Calibration`
5. Select the ESP32 board and port.
6. Compile and upload.

## Usage

1. Wire the hardware according to the wiring table.
2. Power the ESP32 through USB or a suitable regulated supply.
3. Wait for WiFi/NTP synchronisation.
4. View live measurements and status pages on the OLED.
5. If `Sensor Error` appears, check BME280 power, SDA, SCL, ground, and I2C
   address.

## Results

Implemented outputs:

- Live temperature, humidity, pressure, and wind speed.
- Weather status from pressure threshold rules.
- Comfort status from temperature and humidity rules.
- Daily minimum and maximum temperature.
- BME280 hardware error screen.
- Clean firmware folder for Arduino IDE use.

## Future Scope

Beginner-to-medium upgrades that fit this portfolio level:

- Replace placeholder images with real OLED and hardware photos.
- Calibrate wind speed against a known reference.
- Add a small enclosure and label wiring.
- Add a hardware test checklist.
- Create a short demo video showing all OLED pages.

Out of scope for this version:

- MQTT
- Firebase
- Cloud dashboards
- Mobile apps
- OTA updates
- AI or machine learning forecasting
- Deep sleep


Skills demonstrated:

- ESP32 firmware development
- I2C sensor integration
- OLED display interface
- GPIO interrupt handling
- Embedded calibration
- Sensor error handling
- Technical documentation

