# 🚗 Gesture-Controlled UGV using ESP32 and MPU6050

A real-time gesture-based RC car project where a wearable glove detects hand tilts and wirelessly controls an Unmanned Ground Vehicle (UGV) using peer-to-peer communication via ESP-NOW.

---

## 🧠 Overview

This project implements a hands-free gesture control system for a UGV using:
- A **wearable glove controller** with an **MPU6050 IMU sensor** and **ESP32**
- A **UGV (car)** platform with **ESP32** and **L293D motor driver**
- **ESP-NOW protocol** for fast, router-less wireless communication

The glove reads hand gestures (tilt) and sends motion commands to the UGV, which mimics the direction in real time.

---

## ⚙️ System Architecture

### 1. **Controller Glove**
- **Hardware**:  
  - ESP32 Dev Module  
  - MPU6050 (connected via I2C)  
  - Powered by Li-ion battery or USB power bank  
- **Function**:  
  - Captures pitch and roll angles from MPU6050  
  - Converts angles into movement commands (FWD, BWD, LEFT, RIGHT)  
  - Sends commands via ESP-NOW to UGV ESP32

### 2. **UGV (Car)**
- **Hardware**:  
  - ESP32 Dev Module  
  - L293D Motor Driver  
  - 2 DC Motors (connected in differential drive config)  
  - Li-ion Battery (7.4V or 11.1V)  
- **Function**:  
  - Receives commands via ESP-NOW  
  - Drives motors accordingly to replicate hand movement

---

## 📡 Communication Protocol

- **ESP-NOW**  
  - Peer-to-peer wireless protocol by Espressif  
  - No router needed  
  - Low-latency, perfect for real-time control  
  - MAC address used for pairing glove and UGV

---

## 🛠️ How I Built It

### Step 1: Setup Controller
- Wired MPU6050 to ESP32 using I2C (SCL: GPIO 22, SDA: GPIO 21)
- Read pitch/roll from MPU using `Wire.h` and custom filtering
- Classified direction:
  - `pitch > 10°` → Move Forward  
  - `pitch < -10°` → Move Backward  
  - `roll > 10°` → Move Right  
  - `roll < -10°` → Move Left
- Sent encoded string commands over ESP-NOW (`'F'`, `'B'`, `'L'`, `'R'`)

### Step 2: Setup UGV
- Connected ESP32 to L293D motor driver
- Used GPIOs to control motor direction pins (`IN1, IN2, IN3, IN4`)
- Decoded received characters and drove motors accordingly

### Step 3: ESP-NOW Integration
- Registered each other's MAC addresses
- Used `esp_now_send()` and `esp_now_recv()` callbacks for TX/RX
- Debugged using Serial Monitor

---

## 🧾 Components Used

| Component          | Quantity |
|--------------------|----------|
| ESP32 Dev Board    | 2        |
| MPU6050 IMU        | 1        |
| L293D Motor Driver | 1        |
| DC Motors          | 2        |
| Li-ion Battery     | 1        |
| Jumper Wires       | –        |
| Car Chassis        | 1        |
| Glove Base         | 1        |

---

## 💻 Code Structure


- `controller_glove/` → MPU6050 + ESP-NOW transmitter code  
- `ugv_car/` → Motor driving code that receives and executes commands

---

## 🎥 Demo

👉 [Project Video](https://github.com/sowmith12/ugv-gesture_control)

---

## 📚 What I Learned

- IMU data filtering and gesture classification
- ESP-NOW setup, MAC pairing, TX/RX callbacks
- Real-time motor control using Arduino code
- Debugging wireless communication

---

## 🧩 Future Improvements

- Add Stop gesture (e.g., flat palm)
- Include acceleration based on tilt magnitude
- Integrate obstacle detection (e.g., ultrasonic sensors)
- Display status on OLED for debugging

---

## 📬 Contact

sowmithmdr@gmail.com

