# Firmware Documentation

## Overview
The hardware intelligence of the BCPSC Robot is distributed across three microcontrollers. This separated architecture ensures that no single board gets bottlenecked while handling communications, motors, and physical articulation. 

## Microcontroller Roles

### 1. The Main Master Controller (ESP32)
- **Function:** Manages expressive systems (eye and jaw servos).
- **Communication:** Processes serial JSON commands coming from the Raspberry Pi and converts them to hardware actions.
- **Networking:** Operates in both AP (Access Point) and STA (Station) WiFi modes to serve as a bridge. It connects to the broader network while hosting a local network for the hand controller.
- **Safety:** Implements a 100-millisecond lockout window after processing serial commands to avoid race conditions and interface conflicts.
- **Physical Models:** 
  - **Eyes:** Uses an Exponential Moving Average algorithm for natural gaze sweeping and microsaccades.
  - **Jaw:** Operates using a physics-based motion model with velocity accumulation and damping for realistic speech articulation.

### 2. Hand Gesture Controller (ESP8266)
- **Function:** Dedicated solely to driving the five finger servos (thumb, index, middle, ring, little finger).
- **Communication:** Runs a REST API on port 80 with a static IP address to receive WiFi HTTP commands from the Main ESP32.
- **Capabilities:** Moves individual fingers to precise, calibrated angles to execute over 20 programmed hand gestures from the library.

### 3. Drive System Controller (ESP32)
- **Function:** Controls the robot's wheeled base movement.
- **Communication:** Broadcasts its own WiFi Access Point and hosts a browser-based dual-joystick interface.
- **Motor Control:** Uses PWM for a differential drive setup over two DC motors (via H-bridge drivers). Turning is achieved by varying PWM speeds between sides.
- **Safety Feature:** Includes a **hardware deadman switch**. If the controller device disconnects for more than 500 milliseconds, all motor power is instantly cut to prevent runaway movement.

## Branches Reference
Check the following branches on the main repository for firmware implementations:
- `express`: Likely relates to the expressive controllers (Master ESP32 and Hand ESP8266).
- `movement`: Contains the codebase for the drive system controller.