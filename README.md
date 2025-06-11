# Arduino LPG Leakage Detection and Safety System

**University Course Project**  
**Computer Peripherals Course - 3rd Year, 1st Semester**

A comprehensive safety system designed to detect LPG (Liquefied Petroleum Gas) leakage using Arduino microcontroller and provide immediate safety responses to prevent potential hazards.

## 🎯 Project Overview

This embedded system project demonstrates real-world application of microcontroller programming and sensor interfacing for home safety. The system continuously monitors LPG gas levels and triggers multiple safety mechanisms when dangerous concentrations are detected.

### 🏫 Academic Context
- **Course**: Computer Peripherals 
- **Level**: 3rd Year, 1st Semester
- **Focus**: Embedded Systems, Sensor Integration, Safety Applications
- **Learning Objectives**: Arduino programming, analog sensor interfacing, real-time monitoring

## 🔧 Hardware Components

| Component | Quantity | Purpose |
|-----------|----------|---------|
| Arduino Uno R3 | 1 | Main microcontroller |
| MQ-2 Gas Sensor | 1 | LPG/Gas detection |
| 16×2 LCD Display (I2C) | 1 | Real-time data display |
| Active Buzzer | 1 | Audio alarm |
| RGB LED | 1 | Visual status indicator |
| SG90 Servo Motor | 1 | Valve control mechanism |
| Relay Module | 1 | Power cutoff control |
| Breadboard | 1 | Circuit prototyping |
| Jumper Wires | Multiple | Connections |
| Resistors (220Ω, 10kΩ) | As needed | Current limiting |

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                    LPG Safety Detection System                  │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌──────────────┐    ┌─────────────────┐    ┌─────────────────┐ │
│  │  Input Layer  │    │ Processing Unit │    │  Output Layer   │ │
│  │              │    │                 │    │                 │ │
│  │ ┌──────────┐ │    │  ┌───────────┐  │    │ ┌─────────────┐ │ │
│  │ │   MQ-2   │ │───▶│  │  Arduino  │  │───▶│ │   Buzzer    │ │ │
│  │ │  Sensor  │ │    │  │    Uno    │  │    │ │   Alarm     │ │ │
│  │ └──────────┘ │    │  └───────────┘  │    │ └─────────────┘ │ │
│  │              │    │        │        │    │                 │ │
│  │ ┌──────────┐ │    │        ▼        │    │ ┌─────────────┐ │ │
│  │ │   ADC    │ │    │  ┌───────────┐  │    │ │  LCD Display│ │ │
│  │ │ Reading  │ │    │  │  Safety   │  │    │ │  (I2C)      │ │ │
│  │ └──────────┘ │    │  │Algorithm  │  │    │ └─────────────┘ │ │
│  └──────────────┘    │  └───────────┘  │    │                 │ │
│                      │        │        │    │ ┌─────────────┐ │ │
│                      │        ▼        │    │ │  RGB LED    │ │ │
│                      │  ┌───────────┐  │    │ │ Indicator   │ │ │
│                      │  │Threshold  │  │    │ └─────────────┘ │ │
│                      │  │Comparison │  │    │                 │ │
│                      │  └───────────┘  │    │ ┌─────────────┐ │ │
│                      └─────────────────┘    │ │Servo Motor  │ │ │
│                                             │ │Valve Control│ │ │
│                                             │ └─────────────┘ │ │
│                                             │                 │ │
│                                             │ ┌─────────────┐ │ │
│                                             │ │   Relay     │ │ │
│                                             │ │Power Cutoff │ │ │
│                                             │ └─────────────┘ │ │
│                                             └─────────────────┘ │
└─────────────────────────────────────────────────────────────────┘
```

## ⚡ Circuit Diagram

```
Arduino Uno Connections:

MQ-2 Gas Sensor:
├── VCC → 5V
├── GND → GND
└── A0  → A0 (Analog Pin)

LCD Display (I2C):
├── VCC → 5V
├── GND → GND
├── SDA → A4
└── SCL → A5

Buzzer:
├── Positive → Pin 8
└── Negative → GND

RGB LED:
├── Red   → Pin 9 (PWM)
├── Green → Pin 10 (PWM)
├── Blue  → Pin 11 (PWM)
└── Common Cathode → GND (through 220Ω resistor)

Servo Motor:
├── Red    → 5V
├── Brown  → GND
└── Orange → Pin 6 (PWM)

Relay Module:
├── VCC → 5V
├── GND → GND
└── IN  → Pin 7
```

## 💻 Code Structure

### Main Components

1. **Sensor Reading Module**
   ```cpp
   int readGasSensor() {
       return analogRead(A0);
   }
   ```

2. **Safety Threshold Logic**
   ```cpp
   bool checkSafetyLevel(int gasValue) {
       return gasValue > DANGER_THRESHOLD;
   }
   ```

3. **Alert System**
   ```cpp
   void triggerAlarm() {
       digitalWrite(BUZZER_PIN, HIGH);
       setRGBColor(255, 0, 0); // Red alert
   }
   ```

4. **Safety Response**
   ```cpp
   void activateSafetyMeasures() {
       cutOffPower();
       closeGasValve();
       displayEmergencyMessage();
   }
   ```

## 🚀 Features

### 🔍 **Gas Detection**
- MQ2 sensor can detect LPG, propane, methane, hydrogen, and other combustible gases
- Real-time analog-to-digital conversion
- Calibrated threshold levels for accurate detection

### 🚨 **Multi-Level Alert System**
- **Visual**: RGB LED color coding (Green→Yellow→Red)
- **Audio**: Progressive buzzer alerts
- **Display**: Real-time gas concentration on LCD

### 🛡️ **Safety Mechanisms**
- **Automatic Valve Control**: Servo motor closes gas supply
- **Power Cutoff**: Relay disconnects electrical appliances
- **Emergency Display**: Clear status messages on LCD

### 📊 **Real-Time Monitoring**
- Continuous gas level monitoring
- Percentage-based concentration display
- Historical data logging capability

## 🔧 Installation & Setup

### 1. Hardware Assembly
```bash
# Follow the circuit diagram above
# Ensure proper power connections (5V/GND)
# Double-check sensor orientation
# Test continuity before powering on
```

### 2. Software Installation
```bash
# Install Arduino IDE
# Install required libraries:
# - LiquidCrystal_I2C
# - Servo.h (built-in)

# Upload the code to Arduino Uno
```

### 3. Calibration Process
```cpp
// In setup() function:
void calibrateSystem() {
    // Allow sensor warm-up time (60 seconds)
    // Set baseline readings in clean air
    // Configure threshold values
}
```

## 📈 System Operation

### Normal Operation
- **Green LED**: Safe gas levels
- **LCD Display**: Current gas concentration (%)
- **Servo Position**: Valve open
- **Relay Status**: Power connected

### Alert Condition
- **Yellow LED**: Warning level detected
- **Buzzer**: Intermittent beeping
- **LCD**: "WARNING: Gas Detected"

### Emergency Response
- **Red LED**: Danger level exceeded
- **Buzzer**: Continuous alarm
- **LCD**: "DANGER! EVACUATE NOW!"
- **Servo**: Valve closed
- **Relay**: Power disconnected

## 🧪 Testing Procedures

### 1. Baseline Testing
```
- Power on system in clean environment
- Verify normal readings (0-10%)
- Check all indicators show "SAFE" status
```

### 2. Response Testing
```
- Introduce controlled gas source
- Observe graduated response levels
- Verify safety mechanisms activate
- Test emergency reset functionality
```

### 3. Reliability Testing
```
- 24-hour continuous operation test
- Power cycle stability test
- False positive/negative analysis
```

## 📊 Technical Specifications

| Parameter | Value | Unit |
|-----------|-------|------|
| Supply Voltage | 5 | VDC |
| Power Consumption | <2 | Watts |
| Detection Range | 200-10000 | ppm |
| Response Time | <30 | seconds |
| Operating Temperature | -10 to +50 | °C |
| Sensitivity | ±5% | accuracy |

## 🎓 Learning Outcomes

### Technical Skills Gained
- **Embedded Programming**: Arduino C++ development
- **Sensor Interfacing**: Analog sensor integration
- **Real-time Systems**: Time-critical safety responses
- **Hardware Integration**: Multi-component system design

### Safety Engineering Concepts
- **Hazard Analysis**: Gas leakage risk assessment
- **Safety Interlocks**: Multiple protection layers
- **Fail-Safe Design**: System behavior during failures
- **Human-Machine Interface**: Clear status communication

## 🔬 Academic Applications

### Course Relevance
This project demonstrates practical application of:
- **Computer Peripherals**: Sensor and actuator interfacing
- **Embedded Systems**: Real-time microcontroller programming
- **Digital Electronics**: ADC, PWM, and digital I/O
- **Safety Engineering**: Critical system design principles

### Extended Learning
- **IoT Integration**: Add WiFi module for remote monitoring
- **Data Logging**: SD card storage for historical analysis
- **Mobile Alerts**: SMS notifications via GSM module
- **Machine Learning**: Pattern recognition for predictive maintenance

## 🚨 Safety Considerations

### ⚠️ Important Warnings
- **Never test with actual gas leaks**
- **Use controlled testing environment**
- **Ensure proper ventilation during testing**
- **Have fire safety equipment nearby**
- **Follow electrical safety protocols**

### 🔒 Safety Features
- Fail-safe design principles
- Multiple redundant safety mechanisms
- Clear emergency procedures
- Automatic system shutdown capabilities

## 🛠️ Troubleshooting

| Issue | Possible Cause | Solution |
|-------|---------------|----------|
| No sensor reading | Wiring error | Check A0 connection |
| False alarms | Sensor contamination | Clean sensor element |
| LCD not working | I2C connection | Verify SDA/SCL pins |
| Servo not moving | Power insufficient | Check 5V supply |

## 📚 References & Resources

### Academic References
- Arduino Official Documentation
- MQ-2 Sensor Datasheet
- LPG Safety Standards (NFPA 58)
- Embedded Systems Design Principles

### Extended Reading
- Gas Detection Technology
- Safety-Critical System Design
- Microcontroller Applications
- Sensor Calibration Techniques

## 👨‍🎓 Project Credits

**Student**: Masudur Sourav  
**Course**: Computer Peripherals  
**Academic Year**: 3rd Year, 1st Semester  
**Institution**: Mawlana Bhashani Science and Technology University

### 🎯 Project Assessment Criteria
- **Technical Implementation**: Circuit design and code quality
- **Safety Features**: Comprehensive protection mechanisms  
- **Documentation**: Clear project documentation
- **Testing**: Thorough validation procedures
- **Innovation**: Creative problem-solving approaches

## 📄 License

This project is developed for educational purposes as part of university coursework. Code and documentation are available for academic reference and learning.

---

### 🏆 Academic Achievement
This project demonstrates practical application of embedded systems concepts in real-world safety applications, combining theoretical knowledge with hands-on engineering skills essential for computer peripherals and embedded systems development.

**⭐ Project Status**: Completed Successfully  
**📊 Grade**: 4 out of 4
