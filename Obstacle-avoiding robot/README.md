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

### 3. The Left motor was more powerful than the right motor
* **Error:** The Left motor was more "powerful" than the right, causing the car to drift to the right.
* ** Solution** // We lower the Left motor (pin 5) and raise the Right motor (pin 3)
     // to compensate for the drift to the right.
     analogWrite(5, 150); // Left Motor
     analogWrite(3, 155); // Right Motor

### 4. Control Logic Optimization
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

### More about this on my YouTube channel!

## 🚀 Overview
The core of this project is a **reactive control system**. If an object is detected within a specific threshold (20cm), the robot executes an evasion maneuver (stop, backup, and turn) before resuming forward motion.

## 🛠️ Hardware & Components
- **Microcontroller:** Arduino R3 (Atmega328P)
- **Chassis:** 2WD LAFVIN Smart Car Kit
- **Sensors:** HC-SR04 Ultrasonic Sensor
- **Actuators:** DC Motors with L298N Motor Driver
- **IDE:** VS Code + PlatformIO

## 🧠 Technical Logic
The software is structured into modular functions to ensure clean code and efficient execution:
- **Distance Calculation:** Measures the time of flight of sound waves to determine object proximity.
- **Decision Matrix:** 
  - // --- NAVIGATION LOGIC ---
  // If the distance is 0 or greater than 25, CLEAR PATH!
  if (distance > 20 || distance == 0)

  - // If it detects something less than 20cm away, stop, turn, and go to a clear path.
  if (distance > 0 and distance < 20) 

## 📂 Project Structure
- `src/main.cpp`: The main control logic written in C++.
- `platformio.ini`: Project configuration for the R3 board.

## 🎓 What I Learned
