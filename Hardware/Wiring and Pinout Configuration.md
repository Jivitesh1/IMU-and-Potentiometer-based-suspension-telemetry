## Wiring and Pinout Configuration

* **Microcontroller:** ESP32 Development Board
* **MPU-6050 (IMU):** * Communicates via I2C. The bus is configured for Fast Mode (400kHz) to minimize loop delay.
  * Accelerometer scale is initialized to ±8g to handle high-g suspension impacts without clipping.
  * `SDA` -> ESP32 Pin 21
  * `SCL` -> ESP32 Pin 22
  * `VCC` -> 3.3V
  * `GND` -> GND
* **Linear Slide Potentiometer:** * Configured as an analog voltage divider. 
  * ESP32 ADC resolution is explicitly set to 12-bit (0-4095 range).
  * `Signal` -> ESP32 Pin 4
  * `VCC` -> 3.3V
  * `GND` -> GND