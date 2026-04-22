# 🤖 Obstacle Avoidance Robot (C++)
This project features a 2WD Smart Robot designed to navigate environments autonomously. Using C++ and an Ultrasonic sensor, the robot detects obstacles in its path and makes real-time decisions to avoid collisions.


## 🛠️ Lessons Learned (Troubleshooting)

In the `Unsuccessful_Robot_Code` folder, you can find the previous version that failed. Here, I explain why the robot was moving in circles or crashing:

### 1. Compilation Conflicts in VS Code
* **Error:** Duplicate `main.cpp` files within the workspace in VSCODE.
* **Solution:** Clean the workspace to ensure the Arduino compiler uses the correct file.

### 2. Hardware Calibration (Ultrasonic Sensor)
* **Error:** The sensor was **tilted downward**.
* **Result:** The robot detected the ground as a constant obstacle, entering an infinite loop of turning.

### 3. Control Logic Optimization
The decision threshold was improved to filter out false sensor readings:

* **Before:** `if (distance > 15)` (Too short and sensitive to noise).
* **Now:** 
```cpp
// Improved logic to avoid false positives
if (distance > 25 || distance < 5) {
    moveForward(); // Only move forward if there is actual space or if the object is right up close (noise)
}
```
*With this condition, the robot ignores readings under 5 cm (ground noise) and only moves forward if it has a clear path of at least 25 cm.*

## 🚀 Overview
The core of this project is a **reactive control system**. If an object is detected within a specific threshold (15cm), the robot executes an evasion maneuver (stop, backup, and turn) before resuming forward motion.

## 🛠️ Hardware & Components
- **Microcontroller:** Arduino R3 (Atmega328P)
- **Chassis:** 2WD LAFVIN Smart Car Kit
- **Sensors:** HC-SR04 Ultrasonic Sensor
- **Actuators:** DC Motors with L298N Motor Driver
- **IDE:** VS Code + PlatformIO

## 🧠 Technical Logic
The software is structured into modular functions to ensure clean code and efficient execution:
- **Distance Calculation:** Measures the time of flight of sound waves to determine object proximity.
- **Pulse Width Modulation (PWM):** Used to control motor torque and speed (0-255 range).
- **Decision Matrix:** 
  - `Distance > 15cm`: Forward motion.
  - `Distance <= 15cm`: Obstacle detected -> Trigger avoidance protocol.

## 📂 Project Structure
- `src/main.cpp`: The main control logic written in C++.
- `platformio.ini`: Project configuration for the R3 board.

## 🎓 What I Learned
