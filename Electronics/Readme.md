# Electronics & Power Documentation

## Overview
Powering a robot with Raspberry Pi, multiple microcontrollers, and numerous servos requires a specialized and carefully structured power distribution system. The team designed this system from the ground up to ensure safety and stability.

## Architecture & Components

### 1. Power Distribution Circuit
- **Veroboard Setup:** The team hand-soldered a custom veroboard circuit to manage power connections. Strict wiring practices were maintained, as one wrong connection could fry critical components.
- **Voltage Management:** 
  - A series battery setup provides the high voltage necessary for the DC drive motors.
  - **Buck Converters** are utilized to safely step down voltages to appropriate operating levels for the microcontrollers and the 5V servo motors.

### 2. Safety & Protections
- **Deadman Switch Implementation:** The hardware limits were paired with a software safeguard where the Drive ESP32 automatically cuts motor power if connection with the remote control is lost.
- **Circuit Integrity:** Multiple verification tests were conducted before fully integrating the computing units (Raspberry Pi & ESPs) into the power grid.

### 3. Motor Hardware
- **Drive Motors:** 2 DC motors driven by an H-bridge motor driver, utilizing 4 PWM pins for direction and differential steering control.
- **Servos:** High-torque/micro servos distributed for:
  - 1 Eye panning servo
  - 1 Jaw articulation servo
  - 5 Finger servos for hand gestures