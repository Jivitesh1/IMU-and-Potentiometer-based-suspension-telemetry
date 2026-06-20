# IMU and Potentiometer Based Suspension Analysis

![Test Rig Photo](./Images/project%20image.jpg)

## Project Overview
This repository contains the hardware specifications, ESP32 C++ firmware, signal processing methodology, and telemetry results for a custom suspension analysis system. 

The primary objective of this project is to move away from subjective suspension tuning by developing a telemetry system that objectively measures suspension motion on a scaled RC vehicle platform. By analyzing high-speed shaft velocities and chassis acceleration, this project evaluates how different damping configurations influence real-world metrics:
* **Bottoming Resistance**
* **Harshness (NVH)**
* **Small-Bump Compliance**
* **Mechanical Grip & Stability**

## Repository Structure
To keep the documentation modular and easy to read, the project details are divided into the following sections:
* 📂 **[Hardware Details](./Hardware/Component%20overview.md):** Information on the RC telelever/trailing-swingarm platform, sensor mounting specifications (MPU-6050 and linear potentiometer), and damper variables.
* 📂 **[Test-rig Details](./Hardware/Test%20rig%20details.md):** Information on the RC telelever/trailing-swingarm platform, sensor mounting specifications (MPU-6050 and linear potentiometer), and damper variables.
* 📂 **[Software & Telemetry Overview](./Software/Software%20overview.md):** Details on the ESP32 data acquisition parameters (250Hz sample rate, 500k baud UART) and data formatting.
* 📂 **[Signal Processing & Data Correction](./Software/Signal%20processing%20and%20filtering.md):** Explanation of the local ESP32 filtering pipeline, including hardware over-sampling, EMA low-pass filtering, and absolute deadband application.
* 📂 **[Terrain & Impact Testing Methodology](./Terrain%20Tests/Terrain%20and%20Impact%20Testing%20Method.md):** Breakdown of the physical testing, including controlled drop tests and scaled terrain tracking (gravel, speed breakers, ruts).
* 📂 **[Application-Specific Tuning Profiles](./Results/Application-Specific%20Tuning.md):** How the scaled data extrapolates to full-size vehicle tuning (motorcycles, track cars, off-road rigs).

## Quick Start / Usage
1. Flash the ESP32 with the firmware located in `/Code/ESP32_Firmware.ino`.
2. Ensure your MPU-6050 and potentiometer are wired according to the pinout in `Hardware.md`.
3. Connect the ESP32 to your PC via USB.
4. Open [Telemetry Viewer](http://www.farrellf.com/TelemetryViewer/) (or your preferred serial plotter) and connect at `500000` baud.
5. The data frame format is: `[Timestamp (ms)], [Position (mm)], [Velocity (mm/s)], [Acc X (g)], [Acc Y (g)], [Acc Z (g)]`.

## Limitations and Future Scope
While this telemetry system provides objective data, the scaled testing environment introduces specific constraints:
* **Damper Architecture:** The dampers used were simple orifice-type units, limiting the fine-tuning capabilities compared to advanced shim-stack dampers found in full-scale vehicle suspensions.
* **Non-Linear Leverage:** The multi-damper arrangement featured rising rate behavior, introducing non-linear mechanical characteristics that influence the direct measurements.
* **Mass and Inertia:** The significantly lower sprung-to-unsprung mass ratio of the RC platform required running a 50% sag (compared to a standard 30-40%), and the inertia carried by full-scale vehicles is unaccounted for in these scaled tests.