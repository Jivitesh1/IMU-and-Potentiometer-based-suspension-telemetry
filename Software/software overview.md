# Software and Telemetry Overview

The software stack handles the rapid ingestion of analog and I2C signals, processes them locally on the microcontroller, and pushes them to a PC for live visualization.

* **Microcontroller:** Code was developed in the Arduino IDE and flashed to an ESP32.
* **Data Acquisition Rate:** The ESP32 is configured to sample the sensors at 250Hz. This specific frequency provides ample oversampling headroom to capture rapid suspension shaft velocities without dropping data points during sharp impacts.
* **Serial Communication:** Data is transmitted to the PC via USB UART at a high baud rate of 500,000 to ensure zero bottlenecking during live telemetry transmission.
* **Visualization Tool:** "Telemetry Viewer" is used on the PC side for plotting real-time graphs, logging data, and generating the final suspension velocity histograms.

