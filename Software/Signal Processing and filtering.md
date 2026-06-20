# Signal Filtering and Data Correction

Because the hardware operates in an environment with high vibrational and electrical noise, raw sensor data must be processed locally on the ESP32 before being transmitted to the Telemetry Viewer. 

* **1. Hardware Over-Sampling (Averaging Filter):**
  * **Function:** The ESP32 rapid-samples the potentiometer ADC pin 4 times per main loop iteration and averages the result before proceeding.
  * **Purpose:** Cuts down high-frequency electrical noise and localizes ADC jitter before any math operations are applied.
  
* **2. Exponential Moving Average (EMA) Low-Pass Filter:**
  * **Function:** Applies an EMA filter with a smoothing factor (`EMA_ALPHA`) of `0.05` to the mapped wheel position data.
  * **Purpose:** Smooths the incoming data stream to preserve actual suspension dynamics while removing erratic micro-fluctuations that survive the over-sampling phase.

* **3. Pull-to-Zero (Deadband) Filter:**
  * **Function:** Intercepts the final calculated velocity. If the absolute shaft speed is `< 2.0 mm/s`, it forces the output to strictly `0.0 mm/s`.
  * **Purpose:** The potentiometer will output micro-fluctuations even when the suspension is entirely static. Without this absolute deadband, stationary electrical noise plots as false movements, resulting in an inaccurate Gaussian distribution on the histogram.