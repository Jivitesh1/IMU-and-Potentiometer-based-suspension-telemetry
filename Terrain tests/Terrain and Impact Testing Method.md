# Terrain and Impact Testing Methodology

All physical terrain obstacles and drop heights in these tests were scaled relative to the dimensions and operating environment of the RC vehicle platform, rather than representing full-scale vehicle road conditions.

## Controlled Drop Tests
Drop tests were performed to isolate and evaluate suspension behavior during vertical impact events.

* **10 cm Drop (Moderate Impact):**
  * **Setup 1 (Underdamped):** Successfully absorbed the impact but utilized the largest portion of available suspension travel.
  * **Setup 2 (Balanced Damping):** Absorbed the impact while maintaining controlled suspension travel.
  * **Setup 3 (Overdamped):** Showed limited compression due to high damping resistance.

* **20 cm Drop (Severe Impact):**
  * **Setup 1 (Underdamped):** The suspension bottomed out completely, indicating insufficient damping force to control the drop energy.
  * **Setup 2 (Balanced Damping):** Absorbed the impact without bottoming out, utilizing approximately 90% of the available suspension travel to provide the most controlled response.
  * **Setup 3 (Overdamped):** Exhibited hydraulic locking behavior. The suspension compressed very little, resulting in a harsh impact transferred directly to the chassis and suspension components.

## Scaled Terrain Testing
Suspension behavior was evaluated across dynamic terrain to observe continuous damping performance and chassis stability.

* **Gravel and Rough Terrain:**
  * **Setup 1:** Tracked terrain exceptionally well due to low damping resistance, but suffered from excessive chassis oscillation, wallow, and rebound overshoot.
  * **Setup 2:** Provided the best balance between terrain compliance and stability. Responded to bumps in a controlled manner and prevented excessive post-impact bouncing.
  * **Setup 3:** Resisted motion and transmitted heavy vibration to the chassis. Failed to fully absorb larger inputs, kicking the chassis upward instead.

* **Scaled Speed Breakers:**
  * **Setup 1:** Compressed deeply but rebounded noticeably after crossing the obstacle, leading to chassis wallow.
  * **Setup 2:** Compressed and returned with a single, highly controlled rebound cycle.
  * **Setup 3:** Climbed over the obstacle and dropped heavily rather than absorbing it smoothly, producing a noticeable chassis kick at higher speeds.

* **Sharp Edge Impacts (Potholes & Ruts):**
  * **Setup 1:** Absorbed the sharp inputs but rebounded excessively. The tire acted as an undamped spring (bouncy ball effect), kicking the swingarm upward and reducing overall traction.
  * **Setup 2:** Responded in a controlled manner, avoiding bottoming out while strictly maintaining the tire contact patch over the sharp edges.
  * **Setup 3:** Excessive damping resistance prevented compression, causing a harsh upward chassis kick and a loss of mechanical grip over the edge as the damper hydro-locked.