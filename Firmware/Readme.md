# Firmware Documentation

## Overview
The hardware intelligence of the BCPSC Robot is distributed across three microcontrollers. This separated architecture ensures that no single board gets bottlenecked while handling communications, motors, and physical articulation. 

**Lead Integrator:** Jotirmoy Bhowmik

## Microcontroller Roles

### 1. The Main Master Controller (ESP32)
- **Function:** Manages expressive systems (eye and jaw servos).
- **Communication:** Processes serial JSON commands from the Raspberry Pi and converts them to hardware actions.
- **Networking:** Operates in both AP (Access Point) and STA (Station) WiFi modes. It connects to the broader network while hosting a local network for the hand controller.
- **Physical Models:** 
  - **Eyes:** Uses an Exponential Moving Average algorithm for natural gaze sweeping and microsaccades.
  - **Jaw:** Operates using a physics-based motion model with velocity accumulation and damping for realistic speech articulation.

### 2. Hand Gesture Controller (ESP8266)
- **Function:** Dedicated solely to driving the five finger servos (thumb, index, middle, ring, little finger).
- **Communication:** Runs a REST API on port 80 with a static IP address to receive WiFi HTTP commands from the Main ESP32.
- **Capabilities:** Moves individual fingers to precise, calibrated angles to execute over 20 programmed hand gestures.

### 3. Drive System Controller (ESP32)
- **Function:** Controls the robot's wheeled base movement.
- **Communication:** Broadcasts its own WiFi Access Point and hosts a browser-based dual-joystick interface.
- **Motor Control:** Uses PWM for a differential drive setup over two DC motors via H-bridge drivers.

## Challenges & Solutions
1. **Hardware Race Conditions:** Conflicts occurred between the serial interface and the web interface on the microcontrollers. **Solution:** Implemented a 100-millisecond lockout window after every serial command, giving the hardware time to settle before accepting further instructions.
2. **Safety Control:** Preventing the robot from driving autonomously or running away if the controller disconnects. **Solution:** Integrated a software deadman switch that instantly cuts motor power if the wireless connection drops for more than 500 milliseconds.

## Learnings
- **Hardware-Software Boundaries:** Discovered that the boundary between a microcontroller and software requires careful protocol design. Learned that a PWM value on a screen directly corresponds to a real physical force on a wheel, which requires extensive calibration and iteration to get right.

## Branches Reference
- `express`: Expressive controllers (Master ESP32 and Hand ESP8266).
- `movement`: Codebase for the drive system controller.