# Digital Inclinometer for Structural Monitoring

## Project Overview
This project presents a digital inclinometer prototype for monitoring the tilt of structures such as buildings, bridges and metro pillars. It measures inclination and provides an audible alert when the measured angle exceeds a predefined threshold.

The prototype uses an ESP32 NodeMCU with an MPU6050 accelerometer and gyroscope sensor connected over I2C. The ESP32 calculates Pitch and Roll from the accelerometer readings, displays the values on an SSD1306 OLED display, and activates a buzzer when either absolute angle exceeds the threshold.

## Hardware Components
- ESP32 NodeMCU / ESP32 DevKit V1
- MPU6050 accelerometer and gyroscope module
- SSD1306 0.96-inch OLED display (128 × 64)
- Buzzer
- Breadboard and jumper wires
- USB cable

## Software and Libraries
- Arduino IDE and ESP32 board package
- Wire
- Adafruit GFX
- Adafruit SSD1306
- Math (`math.h`)

## Connections

| Component | ESP32 connection |
|---|---|
| MPU6050 VCC | 3.3 V (check your breakout-board specifications) |
| MPU6050 GND | GND |
| MPU6050 SDA | GPIO 21 |
| MPU6050 SCL | GPIO 22 |
| MPU6050 AD0 | GND for I2C address 0x68 |
| OLED VCC | 3.3 V |
| OLED GND | GND |
| OLED SDA | GPIO 21 |
| OLED SCL | GPIO 22 |
| Buzzer (+) | GPIO 26 |
| Buzzer (–) | GND |

## Working Principle
1. The ESP32 initializes I2C, wakes the MPU6050, and initializes the OLED.
2. The program reads the accelerometer's X, Y and Z raw readings.
3. It calculates Pitch and Roll using `atan2()` and displays them on the OLED.
4. The readings are also sent to the Serial Monitor at 115200 baud.
5. If the absolute value of Pitch or Roll exceeds `30.0` degrees, the buzzer is pulsed.

## Repository Contents
- `README.md` — project documentation
- `digital_inclinometer.ino` — ESP32 Arduino source code
- `Project_Report_Digital_Inclinometer_MPU6050.docx` — updated project report

## Implementation Notes
- The supplied firmware calculates angles using accelerometer readings only. It does not read or combine gyroscope data.
- The supplied firmware does not implement a calibration routine or a sensor-fusion filter.
- `THRESHOLD` is 30.0 degrees and is compared against the absolute Pitch and Roll values.
- The code assumes six bytes are available when reading accelerometer registers. A more robust version should check the number of bytes returned by `Wire.requestFrom()` before reading.
- This is an educational prototype, not a certified structural safety or early-warning device.
- Confirm that your physical sensor module is an MPU6050 before using this repository description.

## Future Scope
- Add sensor calibration and filtering.
- Fuse accelerometer and gyroscope readings.
- Add Wi-Fi remote monitoring and data logging.
- Develop a mobile application for live readings and alerts.
- Add battery-powered operation.

## Project Team
- Arjun R Prasad
- Harshith M
- Rehan Kalaiah K S
- S Balaji Chandan

Department of Electronics and Instrumentation Engineering  
Dayananda Sagar College of Engineering, Bengaluru, India
