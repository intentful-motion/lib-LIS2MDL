# LIS2MDL
Arduino library for the LIS2MDL magnetometer with communication over SPI / I2C

Heavily inspired by the [SparkFun LSM6DS3 library](https://github.com/sparkfun/SparkFun_LSM6DS3_Arduino_Library)

Calibration code adapted from [Kris Winer's library](https://github.com/kriswiner/LSM6DSM_LIS2MDL_LPS22HB)

## Usage

```c++
#include <Arduino.h>
#include <LIS2MDL.h>

float x, y, z;

void setup() {
  LIS2MDL mag;
  Serial.begin(115200);

  // configure the magnetometer
  // setting below is a default setting
  mag.settings.tempCompensationEnabled = LIS2MDL_TEMP_COMPENSATION_ENABLED;
  mag.settings.magSampleRate = LIS2MDL_MAG_ODR_10Hz;

  // set up the wire interface
  mag.begin();

  // probably a good idea to calibrate
  Serial.println("Calibriating: move the magnetometer all around");
  delay(4000);
  mag.calibrate();

  Serial.println("Calibration Complete");
}

void loop() {
  x = readFloatMagX();
  y = readFloatMagY();
  z = readFloatMagZ();
  Serial.print("x: ");
  Serial.print(x);
  Serial.print(" y: ");
  Serial.print(y);
  Serial.print(" z: ");
  Serial.println(z);
}
```

# License Information
This code is released under [the MIT License](LICENSE).