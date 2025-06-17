
---

## 🔧 Hardware Used

| Component        | Quantity |
|------------------|----------|
| ESP32 Dev Board  | 2        |
| MPU6050 Module   | 1        |
| L298N Motor Driver | 1      |
| DC Motors        | 2–4      |
| UGV Chassis      | 1        |
| Breadboard & Jumper Wires | as needed |
| Power Supply (for motors) | 1 |

---

## 🎮 How It Works

- The **controller ESP32** reads pitch and roll data from the MPU6050 via I2C.
- Based on tilt direction:
  - Forward tilt → move forward
  - Backward tilt → move backward
  - Left tilt → turn left
  - Right tilt → turn right
- These commands (`'F'`, `'B'`, `'L'`, `'R'`, `'S'`) are sent over **ESP-NOW** to the UGV ESP32.
- The **UGV ESP32** receives the command and drives the motors using the **L298N** module.

---

## 🔌 Connections

### MPU6050 to Controller ESP32

| MPU6050 | ESP32    |
|---------|----------|
| VCC     | 3.3V     |
| GND     | GND      |
| SDA     | GPIO 21  |
| SCL     | GPIO 22  |

### L298N to UGV ESP32 

| L298N   | ESP32    |
|---------|----------|
| IN1     | GPIO 32  |
| IN2     | GPIO 33  |
| IN3     | GPIO 25  |
| IN4     | GPIO 26  |
| ENA/ENB | Connect to 5V (enabled) |
| GND     | GND      |
| VCC     | Motor supply (e.g., 9V) |

---

## 🧠 Code Highlights

### Controller (controller_esp)
- Uses `Wire.h` and `MPU6050` library.
- Calculates pitch and roll from MPU data.
- Maps angle ranges to directions and sends them via ESP-NOW.

### UGV (ugv_esp32)
- Receives direction characters via ESP-NOW.
- Controls motor GPIOs based on received command.

---

## 🚀 Features

- No Wi-Fi router required (ESP-NOW based peer-to-peer communication)
- Intuitive control via hand gestures
- Lightweight and power-efficient setup
- Easily extendable to swarm robotics or gesture-mapped speed control

---

## 🧪 Future Improvements

- Speed variation based on tilt angle
- Integration with ultrasonic sensors for obstacle avoidance
- Swarm coordination with multiple UGVs
- PID control for smoother motion

---

## 📽️ Demo

*Insert video/GIF link here*

---


## 👤 Author

**Sowmith**  


