# Electronics & Power Documentation

## Overview
Powering a robot with a Raspberry Pi, multiple microcontrollers, and numerous servos requires a specialized and carefully structured power distribution system. 

**Lead Electronics Designer:** Naif Bin Nasim

## Architecture & Components

### 1. Power Distribution Circuit
- **Veroboard Setup:** A custom veroboard circuit was designed and hand-soldered to centralize and organize all power connections.
- **Voltage Management:** 
  - A series battery setup provides the high voltage necessary for the heavy DC drive motors.
  - **Buck Converters** safely step down voltages to the 5V and 3.3V operating levels required for the microcontrollers and servos.

### 2. Motor Hardware
- **Drive Motors:** 2 DC motors driven by an H-bridge motor driver, utilizing 4 PWM pins for direction and differential steering control.
- **Servos:** High-torque/micro servos distributed for:
  - 1 Eye panning servo
  - 1 Jaw articulation servo
  - 5 Finger servos for hand gestures

## Challenges & Solutions
1. **Power Safety:** Designing a safe power distribution system where a single wiring error could fry the entire circuit. **Solution:** The veroboard circuit was built with highly organized, verified wiring. Strict testing phases were introduced to identify and correct connection mistakes *before* powering the full, integrated circuit.

## Learnings
- **Electronics & Power Distribution:** Acquired practical skills in reading and designing power circuits, soldering veroboards from scratch, and organizing a multi-component wiring system safely.
- **Fault Diagnosis:** Learned how to safely isolate and diagnose hardware faults when dealing with varying voltage and current requirements simultaneously.

## Future Improvements
- **Battery Management System (BMS):** Integration of a BMS to monitor cell voltage, estimate remaining runtime, and communicate charge levels to the software layer to alert operators before power becomes critically low.
- **Hot-Swappable Configuration:** Designing the power grid to allow depleted battery packs to be replaced on-the-fly without powering down the entire robot (crucial for lengthy exhibitions).
- **Energy Optimization:** Exploring higher energy-density batteries and optimizing the power draw of the servo and motor systems.