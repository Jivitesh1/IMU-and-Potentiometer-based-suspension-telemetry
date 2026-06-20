## code

#include <Wire.h>

// --- Configuration & Hardware Pins ---
const unsigned long INTERVAL_US = 4000; // 250Hz loop
const int POT_PIN = 4;                 // Slide Pot ADC Pin
const int IMU_SDA_PIN = 21;             // MPU6050 Data Pin
const int IMU_SCL_PIN = 22;             // MPU6050 Clock Pin

// --- EMPIRICAL CALIBRATION VALUES ---
const float ADC_EXTENDED = 3775.0;     
const float ADC_COMPRESSED = 1770.0;   
const float TOTAL_WHEEL_TRAVEL_MM = 110.0; 

const float EMA_ALPHA = 0.05;            
const int MPU_ADDR = 0x68; 
const int ACCEL_XOUT_H = 0x3B;

// State Variables
unsigned long previousMicros = 0;
float filteredWheelPosition = 0;
float previousWheelPosition = 0;

void setup() {
  Serial.begin(500000);
  while (!Serial);

  delay(5000);

  analogReadResolution(12); 

  // Initialize I2C with our explicitly defined pins
  Wire.begin(IMU_SDA_PIN, IMU_SCL_PIN);
  Wire.setClock(400000); // 400kHz Fast Mode

  // Wake up MPU6050
  Wire.beginTransmission(MPU_ADDR);
  Wire.write(0x6B); 
  Wire.write(0);    
  Wire.endTransmission(true);

  // Set MPU6050 to +/- 8g
  Wire.beginTransmission(MPU_ADDR);
  Wire.write(0x1C); 
  Wire.write(0x10); 
  Wire.endTransmission(true);
}

// ... (The loop() remains exactly the same as before)

void loop() {
  unsigned long currentMicros = micros();

  if (currentMicros - previousMicros >= INTERVAL_US) {
    float dtSeconds = (currentMicros - previousMicros) / 1000000.0;
    previousMicros = currentMicros; 

    // 1. Read and Constrain the Slide Potentiometer
    // 1. Oversampled ADC Read
    int rawADC = 0;
    for (int i = 0; i < 4; i++) {
      rawADC += analogRead(POT_PIN);
    }
    rawADC = rawADC / 4; // Get the average
    float constrainedADC = constrain(rawADC, min(ADC_EXTENDED, ADC_COMPRESSED), max(ADC_EXTENDED, ADC_COMPRESSED));
    
    // 2. Direct Empirical Mapping to Wheel Travel
    float rawWheelPositionMM = ((constrainedADC - ADC_EXTENDED) / (ADC_COMPRESSED - ADC_EXTENDED)) * TOTAL_WHEEL_TRAVEL_MM;

    // 3. Apply EMA Low-Pass Filter
    filteredWheelPosition = (EMA_ALPHA * rawWheelPositionMM) + ((1.0 - EMA_ALPHA) * filteredWheelPosition);

    // 4. Calculate Wheel Velocity (mm/sec)
    float wheelVelocity = (filteredWheelPosition - previousWheelPosition) / dtSeconds;
    
    // --- THE DEADBAND FILTER ---
    // If the speed is less than 2 mm/s, force it to 0.
    if (abs(wheelVelocity) < 2.0) { 
      wheelVelocity = 0.0;
    }

    previousWheelPosition = filteredWheelPosition;

    // 5. Read IMU Data
    Wire.beginTransmission(MPU_ADDR);
    Wire.write(ACCEL_XOUT_H); 
    Wire.endTransmission(false);
    Wire.requestFrom(MPU_ADDR, 6, true); 
    
    int16_t accelX = (Wire.read() << 8 | Wire.read());
    int16_t accelY = (Wire.read() << 8 | Wire.read());
    int16_t accelZ = (Wire.read() << 8 | Wire.read());

    float gX = accelX / 4096.0;
    float gY = accelY / 4096.0;
    float gZ = accelZ / 4096.0;

    // 6. Output to Telemetry Viewer
    Serial.print(currentMicros);           Serial.print(",");
    Serial.print(filteredWheelPosition);   Serial.print(",");
    Serial.print(wheelVelocity);           Serial.print(",");
    Serial.print(gX);                      Serial.print(",");
    Serial.print(gY);                      Serial.print(",");
    Serial.println(gZ);              
  }
}