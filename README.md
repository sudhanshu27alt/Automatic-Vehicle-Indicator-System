# 🚗 Automatic Vehicle Indicator System Using Arduino

### An Intelligent Vehicle Safety System with Automatic Turn Detection and Self-Cancelling Indicators

![Arduino](https://img.shields.io/badge/Platform-Arduino_Uno-00979D?logo=arduino)
![Language](https://img.shields.io/badge/Language-C%2B%2B-blue)
![Sensor](https://img.shields.io/badge/Sensor-MPU6050-orange)
![Project](https://img.shields.io/badge/Project-Embedded_Systems-green)
![Status](https://img.shields.io/badge/Status-Prototype-yellow)

---

## 📌 1. Project Overview

The **Automatic Vehicle Indicator System Using Arduino** is an intelligent embedded system designed to improve road safety by automating vehicle turn indicators.

Traditional vehicle indicators require drivers or riders to manually activate and deactivate turn signals. Sometimes, drivers forget to activate indicators before turning or leave them ON even after completing a turn, which can confuse other road users and potentially cause accidents.

This project introduces an automated solution using an Arduino Uno R3 and an MPU6050 Inertial Measurement Unit (IMU) sensor.

The system continuously monitors vehicle movement, detects left and right turning movements, activates the corresponding indicators, and automatically switches them OFF when the vehicle returns to a straight position.

An additional ultrasonic sensor monitors the rear blind spot and provides an audible warning when an obstacle is detected during a turning maneuver.

The system also retains manual indicator control for situations where automatic detection is insufficient.

---

## 🎯 2. Project Objectives

The major objectives of this project are:

- **Automatic Turn Detection:** Detect left and right turning movements using an MPU6050 sensor.
- **Automatic Indicator Activation:** Activate the corresponding indicator based on vehicle movement.
- **Self-Cancellation:** Automatically turn OFF indicators after completing a turn.
- **Blind-Spot Monitoring:** Detect nearby objects using an ultrasonic sensor.
- **Audible Warning:** Generate a buzzer alert when an obstacle is detected during a turning maneuver.
- **Manual Override:** Allow users to operate indicators manually.
- **Cost-Effective Design:** Develop an affordable vehicle safety solution using commonly available electronic components.

---

## ⚙️ 3. Technologies Used

| Technology | Purpose |
|---|---|
| Arduino IDE | Programming and uploading code |
| Arduino Uno R3 | Main microcontroller |
| Embedded C/C++ | Firmware development |
| MPU6050 | Motion and orientation detection |
| HC-SR04 | Ultrasonic distance measurement |
| Relay Module | Indicator switching |
| DC-DC Buck Converter | Voltage regulation |
| Electronic Sensors | Vehicle movement monitoring |

---

## 🔩 4. Hardware Components

The following components are used to develop the prototype:

| Component | Quantity | Function |
|---|---:|---|
| Arduino Uno R3 | 1 | Main processing unit |
| MPU6050 Sensor | 1 | Detects vehicle movement and tilt |
| HC-SR04 Ultrasonic Sensor | 1 | Detects nearby rear obstacles |
| 2-Channel 5V Relay Module | 1 | Controls left and right indicators |
| LM2596 Buck Converter | 1 | Converts 12V to regulated 5V |
| Active Piezo Buzzer | 1 | Provides audible alerts |
| 12V LED Indicators | 2 sets | Displays turning direction |
| Connecting Wires | As required | Electrical connections |
| Push Button | 1 | Hazard/reset control |
| Protection Components | As required | Circuit protection |

---

## 🧠 5. Working Principle

The system operates through four major stages:

### Stage 1: Motion Detection

The MPU6050 sensor continuously measures the vehicle's movement using its built-in:

- 3-axis accelerometer
- 3-axis gyroscope

These measurements help determine vehicle tilt, angular velocity, and turning movement.

### Stage 2: Data Processing

The Arduino Uno receives motion data from the MPU6050 through the I2C communication protocol.

A complementary filter combines accelerometer and gyroscope readings to calculate a more stable roll angle.

The Arduino compares the calculated values with predefined turning thresholds.

### Stage 3: Automatic Indicator Activation

When the vehicle crosses the specified turning threshold:

- Left movement activates the left indicator.
- Right movement activates the right indicator.

The Arduino sends signals to the relay module, which controls the corresponding 12V indicator lamps.

### Stage 4: Automatic Cancellation

After completing the turn, the system detects when the vehicle returns to a stable, straight-line position.

Once the stabilization condition is maintained for the required duration, the Arduino automatically deactivates the indicator.

This prevents indicators from remaining ON unnecessarily.

### Additional Feature: Blind-Spot Warning

The HC-SR04 ultrasonic sensor continuously checks the rear-side detection area.

If an object is detected within the configured distance while a turn signal is active, the buzzer generates an audible warning.

---

## 🔌 6. Arduino Pin Configuration

The following pin configuration is described in the project report:

| Arduino Pin | Connected Component | Function |
|---|---|---|
| A4 | MPU6050 SDA | I2C Data |
| A5 | MPU6050 SCL | I2C Clock |
| D2 | Manual Left Switch | Left Indicator Input |
| D3 | Manual Right Switch | Right Indicator Input |
| D4 | Hazard/Reset Button | Hazard Control |
| D5 | HC-SR04 TRIG | Ultrasonic Trigger |
| D6 | HC-SR04 ECHO | Ultrasonic Echo |
| D7 | Left Relay | Left Indicator Control |
| D8 | Right Relay | Right Indicator Control |
| D9 | Buzzer | Audible Warning |

**Power Supply:**
- Vehicle Battery: 12V DC
- Buck Converter Output: 5V DC
- Arduino and Sensor Supply: 5V

Note: Automotive 12V inputs must be properly protected and conditioned before interfacing with Arduino logic. The actual circuit should be verified before implementation.

---

## 📐 7. System Architecture

The project consists of four major subsystems:

**1. Power Conditioning Unit**

Receives 12V vehicle battery power and converts it into a regulated 5V supply using the LM2596 buck converter.

**2. Sensor Unit**

Uses MPU6050 for motion detection and HC-SR04 for rear obstacle detection.

**3. Processing Unit**

Arduino Uno processes sensor readings, evaluates turning conditions, and determines the appropriate indicator state.

**4. Output and Alert Unit**

The relay module controls left and right indicators, while the buzzer provides audible warnings.

### Overall System Flow

Vehicle Battery (12V)  
↓  
LM2596 Voltage Regulator  
↓  
Arduino Uno R3  
↓  
MPU6050 Motion Detection  
↓  
Motion Data Processing  
↓  
Turning Direction Detection  
↓  
Relay Activation  
↓  
Left / Right Indicator ON  
↓  
Vehicle Stabilization Detection  
↓  
Automatic Indicator OFF

---

## 🧮 8. Algorithm and Logic

The system uses a complementary filter to combine accelerometer and gyroscope readings.

### Turn Activation Conditions

- Left Turn: Roll angle less than -14°.
- Right Turn: Roll angle greater than +14°.
- Confirmation Time: 160 milliseconds.

### Turn Cancellation Conditions

The indicator automatically switches OFF when:

- Absolute roll angle becomes less than 5°.
- Absolute yaw angular velocity becomes less than 4°/s.
- Both conditions remain satisfied for 1.2 seconds.

### Additional Safety Condition

A maximum automatic indicator timeout of 25 seconds is included in the proposed control logic.

### Indicator Control States

The firmware uses a state-based control approach:

- IDLE
- AUTO_LEFT
- AUTO_RIGHT
- MANUAL_LEFT
- MANUAL_RIGHT
- HAZARD

This makes the system easier to manage and reduces conflicts between automatic and manual indicator operations.

---

## 📊 9. Testing and Performance Evaluation

According to the experimental results documented in the project report, the prototype was evaluated through different vehicle maneuvers and sensor testing.

| Test Scenario | Trials | Successful Trigger/Cancel |
|---|---:|---:|
| 90° Left/Right Turns | 40 | 40/40 |
| Urban Lane Changes | 30 | 28/30 |
| Roundabout Navigation | 20 | 19/20 |
| Rough/Pothole Roads | 15 | No false triggering |
| Manual Switch Override | 15 | 15/15 |

### Key Performance Observations

- Average turn detection latency ranged from approximately 168 ms to 182 ms across the reported maneuver tests.
- Average automatic cancellation time ranged from 1.21 to 1.28 seconds.
- No false activations were reported during the specified rough-road testing.
- Manual indicator control remained functional during the tests.

These figures are results reported in the supplied technical report and should be independently reproduced before being treated as verified product performance.

---

## ⭐ 10. Key Features and Advantages

1. Automatic left and right turn detection.
2. Intelligent self-cancelling indicators.
3. MPU6050-based motion sensing.
4. Ultrasonic rear-obstacle detection.
5. Audible warning through a buzzer.
6. Manual indicator override.
7. Low-cost embedded system architecture.
8. Modular hardware design.
9. Reduced possibility of forgotten indicators.
10. Potential compatibility with multiple vehicle categories.

---

## ⚠️ 11. Limitations

Although the system provides several useful features, it has some limitations:

- Pre-turn signaling cannot be predicted using inertial sensing alone.
- Very low-speed turns may not produce sufficient vehicle tilt.
- Fixed turning thresholds may require vehicle-specific calibration.
- Ultrasonic sensors have limited detection range.
- Electronic components require proper protection against vibration, moisture, and automotive electrical transients.

The prototype is an educational engineering project and should not replace factory vehicle safety systems or be used on public roads without appropriate engineering validation.

---

## 🚀 12. Future Scope

The project can be improved further by introducing advanced technologies.

**1. GPS Integration**

GPS can help identify upcoming intersections and provide anticipatory turn signaling.

**2. Machine Learning Integration**

TinyML can classify different vehicle movements and distinguish intentional turns from sudden evasive movements.

**3. IoT Connectivity**

Wireless communication can allow vehicles to exchange turn-related information.

**4. Advanced Blind-Spot Detection**

Automotive radar sensors can improve rear-approach detection and measure relative vehicle speed.

**5. CAN Bus Integration**

Integration with vehicle CAN bus systems can provide access to vehicle speed and other relevant parameters.

**6. Custom PCB Development**

A dedicated automotive-grade PCB and weatherproof enclosure can improve reliability and make the system more suitable for practical deployment.

---

## 📁 13. Repository Structure

The recommended GitHub repository structure is:

```text
Automatic-Vehicle-Indicator-System/
│
├── README.md
│
├── Arduino_Code/
│   └── Automatic_Vehicle_Indicator.ino
│
├── Circuit_Diagram/
│   └── circuit_diagram.png
│
├── Images/
│   ├── project_setup.jpg
│   ├── arduino_uno.jpg
│   ├── mpu6050_sensor.jpg
│   ├── relay_module.jpg
│   └── final_prototype.jpg
│
├── Documentation/
│   └── Project_Report.pdf
│
└── LICENSE
```

---

## 🎓 14. Applications

This project can potentially be applied to:

- Motorcycles and scooters.
- Three-wheelers and auto-rickshaws.
- Older passenger vehicles.
- Educational embedded systems projects.
- Intelligent transportation research.
- Automotive safety system prototyping.

---

## 🏁 15. Conclusion

The Automatic Vehicle Indicator System using Arduino demonstrates how embedded systems and motion sensors can improve conventional vehicle signaling mechanisms.

By integrating the Arduino Uno R3, MPU6050, HC-SR04 ultrasonic sensor, and relay module, the system provides automatic turn detection, indicator activation, self-cancellation, and rear-obstacle warning capabilities.

The project demonstrates the practical application of sensor interfacing, embedded C/C++ programming, real-time data processing, and electronic control systems.

With future improvements such as GPS integration, machine learning, IoT connectivity, and automotive-grade hardware, this project has the potential to evolve into a more advanced intelligent vehicle safety solution.

---

## 👨‍💻 16. Author

**Project:** Automatic Vehicle Indicator System Using Arduino

**Domain:** Embedded Systems | Arduino | IoT | Automotive Safety

**Institution:** Shri Ramswaroop Memorial University, Barabanki

**Course:** B.Tech Computer Science (Data Science & Artificial Intelligence)

---

⭐ If you find this project interesting, consider giving this repository a star!
