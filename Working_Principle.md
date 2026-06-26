# Working Principle

## Data Flow

```text
BME280 Sensor -> I2C -> ESP32 -> Unit Conversion -> Status Logic -> OLED
Wind Sensor -> GPIO15 Interrupt -> ESP32 -> Wind Speed Average -> OLED
```

## Startup

1. ESP32 starts serial debugging at 115200 baud.
2. I2C is started on SDA/SCL.
3. OLED is initialised so startup or error messages can be displayed.
4. ESP32 checks for the BME280 at address `0x76`.
5. If BME280 is not detected, the OLED displays `Sensor Error`.
6. If BME280 is detected, WiFi and NTP time services are started.
7. Wind sensor interrupt handling is configured on GPIO15.

## Sensor Processing

The BME280 provides:

- Temperature in Celsius.
- Humidity in percent relative humidity.
- Pressure in Pascals, converted to hPa.

The firmware applies a pressure calibration offset and converts units depending
on the configured display format.

## Weather Status

Weather status is based on calibrated pressure:

| Pressure | Status |
| --- | --- |
| `>= 1020 hPa` | Sunny |
| `1005 hPa` to below `1020 hPa` | Normal |
| `< 1005 hPa` | Rain Possible |

This is a simple status indicator, not a meteorological forecast.

## Comfort Status

Comfort status is based on temperature and humidity:

| Condition | Status |
| --- | --- |
| Temperature `< 18 C` | Cold |
| Temperature `> 32 C` | Hot |
| Temperature `18 C` to `28 C` and humidity `<= 70%` | Comfortable |
| Remaining warm or high-humidity conditions | Warm |

## Daily Temperature Range

The firmware stores the current day's minimum and maximum temperature in RAM.
The range resets automatically when the displayed calendar date changes or when
the ESP32 restarts.

## Display Logic

The OLED rotates every four seconds:

1. Live measurements.
2. Weather and comfort status.
3. Daily minimum and maximum temperature.

