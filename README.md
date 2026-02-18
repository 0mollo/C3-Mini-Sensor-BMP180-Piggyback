![image alt](https://github.com/0mollo/C3-Mini-Sensor-BMP180-Piggyback/blob/main/BMP%20180%20GY-68%20top%20view.png)  ![image alt](https://github.com/0mollo/C3-Mini-Sensor-BMP180-Piggyback/blob/main/BMP%20180%20GY-68%20bottom%20view.png)

# C3-Mini-Sensor-BMP180-Piggyback

Barometric Pressure, Altitude & Temperature Monitoring Module  
Version: V1.1  


##  Overview

The C3-Mini BMP180 Piggyback is a compact add-on board designed for seamless integration with the C3-Mini development board.

It enables:

- Barometric pressure measurement
- Altitude calculation
- Ambient temperature monitoring
- Indoor climate logging
- Weather forecasting applications

This board is part of the Carenuity modular ecosystem.



##  Technical Specifications

| Parameter | Value |
|------------|--------|
| Sensor | Bosch BMP180 |
| Interface | I2C |
| Operating Voltage | 3.3V |
| Logic Level | 3.3V |
| Pressure Range | 300 – 1100 hPa |
| Temperature Range | -40°C to +85°C |
| Resolution | 0.01 hPa |
| Accuracy | ±1 hPa |



##  Pin Configuration (BMP180 Header)

| Pin | Function |
|------|----------|
| VIN | 3.3V |
| GND | Ground |
| SCL | I2C Clock |
| SDA | I2C Data |


##  C3-Mini Header Mapping

The piggyback aligns directly with the C3-Mini GPIO layout.

Recommended I2C pins:

| C3-Mini Pin | BMP180 |
|-------------|--------|
| GPIO8 | SDA |
| GPIO10 | SCL |
| 3V3 | VIN |
| GND | GND |


##  Included Files

- KiCad Schematic File [See](https://github.com/0mollo/C3-Mini-Sensor-BMP180-Piggyback/blob/main/BMP%20180%20GY-68.pdf)
- 3D model (Pictorial)
- Example firmware



##  Example Arduino Code

```cpp
#include <Wire.h>
#include <Adafruit_BMP085.h>

Adafruit_BMP085 bmp;

void setup() {
  Serial.begin(115200);
  Wire.begin(8, 10);  // SDA, SCL for C3 Mini

  if (!bmp.begin()) {
    Serial.println("BMP180 not detected!");
    while (1);
  }
}

void loop() {
  Serial.print("Temperature = ");
  Serial.print(bmp.readTemperature());
  Serial.println(" *C");

  Serial.print("Pressure = ");
  Serial.print(bmp.readPressure());
  Serial.println(" Pa");

  Serial.print("Altitude = ");
  Serial.print(bmp.readAltitude());
  Serial.println(" m");

  Serial.println();
  delay(2000);
}
