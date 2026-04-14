# 🤖 Obstacle Avoidance Robot (C++)
This project features a 2WD Smart Robot designed to navigate environments autonomously. Using C++ and an Ultrasonic sensor, the robot detects obstacles in its path and makes real-time decisions to avoid collisions.

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
