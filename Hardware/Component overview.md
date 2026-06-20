
## Component Overview
The hardware system was designed to capture high-speed, accurate metrics of the suspension's mechanical movements and the resulting chassis response.

* **Inertial Measurement Unit (IMU):**
  * **Primary Metric:** Measures chassis harshness (a major factor in suspension comfort and NVH).
  * **Mounting:** Hard-mounted to the chassis directly above the rear wheel to capture vertical acceleration spikes.
* **Linear Slide Potentiometer:**
  * **Primary Metric:** Measures direct wheel travel and stroke speed in mm/s.
  * **Mounting:** Attached between the chassis and the rear swingarm.
  * **Stroke Utilization:** Budget potentiometers exhibit non-linearity at the extremes of their stroke. To ensure accuracy, only the 20% to 80% range of the potentiometer's physical stroke was utilized.
  * **Alignment:** The sensor was mounted specifically to ensure a linear 1:1 reading with wheel travel (achieving 96% linearity), avoiding progressive or digressive travel paths.

