# Underwater Search and Rescue Robot

<p align="center">
  <img src="media/images/final_bot/final_bot.jpg" width="750" alt="Final underwater robot">
</p>

<h2 align="center">Development of an Underwater Search and Rescue Robot</h2>

<p align="center">
  Cost-Effective Underwater Robotic Platform for Remote Navigation,
  Depth Control and Human Detection
</p>

<p align="center">

![Status](https://img.shields.io/badge/Status-Research%20Prototype-blue)
![Platform](https://img.shields.io/badge/Platform-Underwater%20ROV-0077B6)
![MCU](https://img.shields.io/badge/MCU-STM32F4-green)
![SBC](https://img.shields.io/badge/SBC-Raspberry%20Pi%205-red)
![Vision](https://img.shields.io/badge/Vision-YOLOv8-orange)
![CAD](https://img.shields.io/badge/CAD-Fusion%20360-yellow)
![Firmware](https://img.shields.io/badge/Firmware-STM32%20HAL-lightgrey)

</p>

---

## Overview

This repository contains the complete design, development, implementation and
testing of a cost-effective underwater robotic system intended to assist in
search and recovery operations in low-visibility aquatic environments.

The system combines mechanical engineering, embedded systems, electronics,
computer vision, communication and underwater robotics into a single
integrated platform.

### Major capabilities

- Underwater propulsion using BLDC motors
- Electronic speed controller based motor control
- Variable buoyancy based depth control
- Stepper motor driven lead-screw mechanism
- STM32 based low-level real-time control
- Raspberry Pi 5 based high-level processing
- Low-light underwater imaging
- YOLOv8 based human detection
- NCNN optimized inference
- Ethernet-based tethered communication
- USB-CDC communication between Raspberry Pi and STM32
- Web-based robot control
- LED based underwater illumination
- Limit-switch based mechanical protection
- Custom mechanical and waterproofing system

The repository is organized around the complete engineering workflow:
mechanical design, CAD, electronics, firmware, software, computer vision,
experiments, testing, results and documentation.

---

# Project Motivation

Underwater environments are challenging for search and inspection operations
because of poor visibility, light attenuation, turbidity, variable depth,
difficult navigation and limited communication.

The objective is to develop a remotely operated underwater robot that can
assist underwater search operations by providing remote movement, controlled
depth adjustment, live video, real-time detection and operator control.

---

# Objectives

- Design and fabricate an underwater robotic platform.
- Develop a reliable mechanical structure for underwater operation.
- Implement underwater propulsion using BLDC motors.
- Implement controlled vertical movement using variable buoyancy.
- Develop a stepper motor and lead-screw based syringe mechanism.
- Develop STM32 firmware for real-time actuator control.
- Integrate a Raspberry Pi 5 for high-level processing.
- Implement a web-based control interface.
- Establish Raspberry Pi–STM32 communication.
- Integrate a low-light underwater camera.
- Implement YOLOv8 based human detection.
- Optimize computer vision inference for edge hardware.
- Develop and test the power architecture.
- Develop waterproofing and sealing techniques.
- Test individual subsystems and the complete robotic platform.

---

# System Architecture

```text
                         GROUND STATION
                              │
                           Laptop
                              │
                       Ethernet Tether
                              │
                              ▼
                    ┌─────────────────────┐
                    │    Raspberry Pi 5   │
                    │                     │
                    │  Web Interface      │
                    │  Camera Processing  │
                    │  YOLOv8 / NCNN      │
                    │  Command Handling   │
                    │  Video Streaming    │
                    └──────────┬──────────┘
                               │
                              USB
                               │
                            USB-CDC
                               │
                               ▼
                    ┌─────────────────────┐
                    │      STM32F4        │
                    │                     │
                    │  PWM Generation     │
                    │  BLDC Control       │
                    │  Stepper Control    │
                    │  LED Control        │
                    │  Limit Switches     │
                    │  Command Parsing   │
                    └──────┬────────┬─────┘
                           │        │
                    ┌──────▼───┐ ┌──▼──────────┐
                    │   ESCs   │ │ A4988       │
                    │          │ │ Stepper     │
                    └────┬─────┘ └─────┬───────┘
                         │              │
                    ┌────▼─────┐       ▼
                    │   BLDC   │  Lead Screw
                    │  Motors  │       │
                    └──────────┘       ▼
                                Syringe Mechanism
                                       │
                                       ▼
                                Buoyancy Control
```

---

# Complete System Workflow

```text
                    ┌──────────────────┐
                    │     Operator     │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │   Web Interface  │
                    └────────┬─────────┘
                             │
                  ┌──────────┴──────────┐
                  │                     │
                  ▼                     ▼
             Control Data          Video Stream
                  │                     │
                  ▼                     │
          ┌───────────────┐             │
          │ Raspberry Pi  │◄────────────┘
          └───────┬───────┘
                  │
               USB-CDC
                  │
                  ▼
          ┌───────────────┐
          │    STM32      │
          └───────┬───────┘
                  │
       ┌──────────┼───────────┐
       │          │           │
       ▼          ▼           ▼
     BLDC      Stepper      LEDs
     ESCs      A4988
       │          │
       ▼          ▼
   Propulsion   Depth
                Control
```

---

# Mechanical System

The mechanical system houses the electronics, propulsion components, camera
and variable buoyancy mechanism.

The design includes:

- Main underwater body
- Custom end caps
- Internal mounting structures
- 3D-printed components
- Lead-screw mechanism
- Syringe-based buoyancy mechanism
- Camera mounting
- Motor mounting
- Waterproofing and sealing

The documented prototype uses a transparent acrylic body approximately 60 cm
long and 5 inches in diameter. Custom 3D-printed end caps were developed to
match the body dimensions.

Mechanical files are organized under:

```text
mechanical/
```

---

# CAD Design

The mechanical components are designed using Autodesk Fusion 360.

CAD work includes:

- Main body
- End caps
- Internal mounting plates
- Motor mounts
- Camera mounting
- Lead-screw assembly
- Syringe mechanism
- Guide structures
- Component mounting systems

```text
mechanical/
├── cad/
├── drawings/
├── stl/
└── waterproofing/
```

---

# Lead-Screw Depth Control

The variable buoyancy system uses a stepper motor coupled to a lead screw.

```text
             Stepper Motor
                   │
                   ▼
             Lead Screw
                   │
                   ▼
          Linear Displacement
                   │
                   ▼
             Syringe Plunger
                   │
                   ▼
          Water Volume Change
                   │
                   ▼
            Buoyancy Change
                   │
                   ▼
             Depth Control
```

The mechanism provides controlled linear motion and uses limit switches to
restrict travel.

---

# Propulsion System

The robot uses BLDC motors with electronic speed controllers.

```text
STM32 Timer
     │
     │ PWM
     ▼
    ESC
     │
     ▼
 BLDC Motor
     │
     ▼
Propulsion
```

Testing includes ESC initialization, PWM calibration, low-speed operation,
direction control, speed control and current measurement.

---

# STM32 Embedded System

The STM32F4/F411 microcontroller performs low-level real-time control.

### Responsibilities

- BLDC ESC PWM generation
- Motor speed and direction control
- Stepper motor control
- LED control
- Limit switch monitoring
- Interrupt handling
- Command parsing
- USB-CDC communication

The firmware is developed using STM32CubeIDE and STM32 HAL.

```text
                    STM32
                      │
       ┌──────────────┼──────────────┐
       │              │              │
       ▼              ▼              ▼
   BLDC ESC       Stepper/A4988     LEDs
       │              │
       ▼              ▼
    Motors        Lead Screw
```

---

# Stepper Motor Control

The stepper motor is controlled through an A4988 driver.

```text
STM32
 │
 ├── STEP ──────► A4988
 ├── DIR  ──────► A4988
 └── ENABLE ────► A4988
                     │
                     ▼
                Stepper Motor
                     │
                     ▼
                  Lead Screw
```

Limit switches provide mechanical travel protection.

---

# Raspberry Pi 5

The Raspberry Pi 5 performs high-level processing and system integration.

Responsibilities include:

- Web server
- User interface
- Camera interface
- Live video streaming
- Computer vision inference
- YOLOv8 / NCNN
- Command generation
- STM32 communication
- System startup

---

# Web Control Interface

The web interface provides controls for:

- Forward
- Backward
- Left
- Right
- Up
- Down
- Start
- Stop
- LED ON/OFF
- Speed adjustment
- Human detection enable/disable

The interface also displays the live camera feed.

---

# Communication Architecture

```text
Laptop
   │
   │ Ethernet
   ▼
Raspberry Pi 5
   │
   │ USB CDC
   ▼
STM32
   │
   ├──► ESCs
   ├──► Stepper Driver
   ├──► LEDs
   └──► Other Actuators
```

A tethered Ethernet connection is used between the ground station and robot.
USB-CDC is used between the Raspberry Pi and STM32.

---

# Computer Vision

The system uses a low-light camera and YOLOv8 for human detection.

```text
Underwater Camera
       │
       ▼
Frame Capture
       │
       ▼
Image Processing
       │
       ▼
YOLOv8
       │
       ▼
NCNN Optimized Inference
       │
       ▼
Detection Results
       │
       ▼
Operator Interface
```

Initial YOLOv8n testing achieved approximately 6 FPS. Conversion to NCNN
increased the reported inference rate to approximately 12 FPS.

---

# Camera System

The documented system uses a Sony IMX462 based Arducam ultra-low-light
camera for underwater video capture and computer vision.

The camera is used for:

- Live underwater video
- Operator observation
- Human detection
- Computer vision experiments

---

# Underwater Illumination

High-brightness LEDs provide additional illumination in low-light and turbid
water conditions.

```text
STM32
  │
  ▼
LED Control
  │
  ▼
High Brightness LEDs
  │
  ▼
Improved Scene Illumination
```

---

# Power System

The power system is designed around the requirements of:

- BLDC propulsion
- ESCs
- Stepper motor
- Raspberry Pi
- STM32
- Camera
- LEDs
- Supporting electronics

The power analysis covers:

- Battery capacity
- Current requirements
- Voltage requirements
- BMS protection
- Power distribution
- Runtime estimation

```text
                 BATTERY
                    │
                    ▼
                   BMS
                    │
                    ▼
             Power Distribution
                    │
       ┌────────────┼─────────────┐
       │            │             │
       ▼            ▼             ▼
     ESCs         Stepper       Logic
       │           Driver          │
       │             │             ├── Raspberry Pi
       ▼             ▼             ├── STM32
     BLDC         Stepper          ├── Camera
     Motors        Motor            └── LEDs
```

---

# Waterproofing

Waterproofing is a critical part of the underwater system.

The sealing approach includes:

- Custom end caps
- O-ring slots
- Resin sealing
- RTV silicone
- Teflon tape
- Sealed camera window
- Sealed interfaces
- Treated 3D-printed parts

Waterproofing tests are documented under:

```text
experiments/waterproofing/
```

---

# Hardware Components

| Component | Type / Specification | Function |
|---|---|---|
| BLDC Motors | 3670 class propulsion motors | Underwater propulsion |
| ESCs | 150 A / 20 A class | BLDC control |
| STM32F4/F411 | Cortex-M4 | Low-level control |
| Raspberry Pi 5 | Quad-core, 2.4 GHz, 8 GB RAM | High-level processing |
| Stepper Motor | NEMA class | Depth actuation |
| A4988 | Stepper driver | Stepper control |
| Limit Switches | Mechanical | Travel protection |
| LEDs | High brightness | Illumination |
| Li-ion/LiPo Battery | 12 V class | System power |
| BMS | 40 A, 12.6 V | Battery protection |
| Arducam IMX462 | Ultra-low-light camera | Imaging |

---

# Testing and Validation

Testing is divided into subsystem and system-level validation.

## Mechanical Testing

- Dimensional verification
- Assembly testing
- Lead-screw testing
- Syringe actuation
- Mechanical travel
- Structural inspection

## Waterproofing Testing

- Leak testing
- Seal inspection
- End-cap testing
- Cable sealing
- Immersion testing

## Motor Testing

- ESC initialization
- PWM testing
- Low-speed testing
- Direction testing
- Speed testing
- Current measurement

## Depth-Control Testing

- Stepper operation
- Lead-screw movement
- Syringe movement
- Limit-switch operation
- Travel-limit testing

## Communication Testing

- Ethernet connectivity
- USB-CDC communication
- Raspberry Pi–STM32 communication
- Command reception
- Command execution

## Computer Vision Testing

- Camera streaming
- YOLO inference
- Frame rate
- NCNN optimization
- Real-time operation

## System Testing

- Complete hardware integration
- Simultaneous subsystem operation
- Camera streaming
- Web interface
- Depth control
- Human detection
- Power consumption
- Runtime

---

# Experimental Workflow

```text
             Individual Component
                     │
                     ▼
              Subsystem Test
                     │
                     ▼
              Interface Test
                     │
                     ▼
            Multi-Subsystem Test
                     │
                     ▼
             System Integration
                     │
                     ▼
             Controlled Testing
                     │
                     ▼
             Underwater Testing
                     │
                     ▼
              Results Analysis
                     │
                     ▼
               Iteration
```

---

# Results

The integrated prototype demonstrates:

- Web-based control
- Raspberry Pi high-level processing
- STM32 low-level actuator control
- BLDC propulsion
- Stepper-based depth control
- Limit-switch protection
- Live camera feed
- YOLOv8 inference
- NCNN optimized inference
- Raspberry Pi–STM32 communication

The documented computer vision pipeline achieved approximately 6 FPS during
initial YOLOv8n testing and approximately 12 FPS after NCNN optimization.

The documented prototype cost was approximately ₹45,000.

---

# Performance Summary

| Parameter | Value / Implementation |
|---|---|
| Main Controller | Raspberry Pi 5 |
| Low-Level Controller | STM32F4/F411 |
| Communication | Ethernet + USB CDC |
| Camera | Sony IMX462 based Arducam |
| Detection Model | YOLOv8n |
| Optimized Runtime | NCNN |
| Initial Inference | ~6 FPS |
| Optimized Inference | ~12 FPS |
| Main Propulsion | BLDC + ESC |
| Depth Actuation | Stepper + A4988 |
| Depth Mechanism | Lead Screw + Syringe |
| Illumination | High Brightness LEDs |
| Battery Protection | BMS |
| Approx. Prototype Cost | ₹45,000 |

---

# Repository Structure

```text
underwater-search-and-rescue-robot/
│
├── README.md
├── LICENSE
├── .gitignore
├── CHANGELOG.md
│
├── docs/
│   ├── reports/
│   ├── design/
│   │   ├── mechanical/
│   │   ├── electrical/
│   │   └── software/
│   ├── testing/
│   └── literature/
│
├── mechanical/
│   ├── cad/
│   ├── drawings/
│   ├── stl/
│   └── waterproofing/
│
├── electronics/
│   ├── schematics/
│   ├── wiring/
│   ├── pinout/
│   ├── power/
│   └── motor_control/
│
├── firmware/
│   ├── stm32/
│   └── communication_protocol/
│
├── software/
│   ├── raspberry_pi/
│   ├── computer_vision/
│   └── ground_station/
│
├── experiments/
│   ├── motor/
│   ├── depth_control/
│   ├── waterproofing/
│   ├── power/
│   └── communication/
│
├── results/
│   ├── mechanical/
│   ├── electrical/
│   ├── firmware/
│   ├── software/
│   ├── computer_vision/
│   └── system_tests/
│
├── media/
│   ├── images/
│   │   ├── cad/
│   │   ├── fabrication/
│   │   ├── electronics/
│   │   ├── testing/
│   │   ├── final_bot/
│   │   └── report_pages/
│   └── videos/
│
├── data/
│   ├── raw/
│   ├── processed/
│   ├── test_results/
│   └── ml/
│
├── bom/
└── scripts/
```

---

# Project Development Workflow

```text
                    REQUIREMENTS
                         │
                         ▼
                  SYSTEM DESIGN
                         │
          ┌──────────────┼──────────────┐
          │              │              │
          ▼              ▼              ▼
      Mechanical     Electronics     Software
          │              │              │
          ▼              ▼              ▼
        CAD          Wiring/Power    Firmware
          │              │              │
          └──────────────┼──────────────┘
                         │
                         ▼
                     Fabrication
                         │
                         ▼
                      Assembly
                         │
                         ▼
                Subsystem Testing
                         │
                         ▼
                 System Integration
                         │
                         ▼
                 Functional Testing
                         │
                         ▼
                 Underwater Testing
                         │
                         ▼
                  Results Analysis
                         │
                         ▼
                    Iteration
```

---

# Future Work

Future development can focus on:

### Mechanical

- Improved waterproof enclosure
- Higher depth rating
- Improved sealing
- Reduced weight
- Improved buoyancy control
- More compact internal architecture

### Electronics

- Improved power distribution
- Dedicated voltage regulation
- Battery monitoring
- Current monitoring
- Improved thermal management

### Embedded Control

- Closed-loop depth control
- Automatic buoyancy stabilization
- Improved motor control
- Better fault handling
- Hardware safety interlocks

### Communication

- Improved tether architecture
- Floating communication infrastructure
- Extended operating range
- Improved data transmission

### Computer Vision

- Larger underwater datasets
- Underwater image enhancement
- Improved detection robustness
- Better low-light performance
- Additional object classes
- Improved edge inference

### Sensing

Future versions can investigate:

- Imaging sonar
- Acoustic sensors
- Depth sensors
- IMU
- Pressure sensors
- Sensor fusion

### Autonomy

Future development can include:

- Autonomous navigation
- Depth stabilization
- Obstacle avoidance
- Target tracking
- Search-pattern generation
- Semi-autonomous underwater search

---

# Safety

This project involves:

- High-current batteries
- BLDC motors
- Electronic speed controllers
- Rotating mechanical components
- High-current wiring
- Waterproof electrical systems
- Underwater operation

All experiments should be performed using appropriate electrical, mechanical
and laboratory safety procedures.

The prototype is intended for research and development and should not be used
for real-world rescue operations without appropriate validation and operational
safety procedures.

---

# Limitations

The current system has several areas requiring further development:

- Waterproofing reliability
- Long-duration underwater operation
- Raspberry Pi thermal management
- Battery runtime
- Underwater communication
- Visibility in highly turbid water
- Computer vision performance under extreme underwater conditions
- Limited representative training data
- Mechanical reliability at increased depth
- More extensive underwater system-level testing

---

# Documentation

| Resource | Location |
|---|---|
| Final Report | `docs/reports/Final_Report.pdf` |
| Mechanical Design | `mechanical/` |
| Electronics | `electronics/` |
| STM32 Firmware | `firmware/stm32/` |
| Raspberry Pi Software | `software/raspberry_pi/` |
| Computer Vision | `software/computer_vision/` |
| Experiments | `experiments/` |
| Results | `results/` |
| Images | `media/images/` |
| Videos | `media/videos/` |
| Bill of Materials | `bom/` |

---

# References

Detailed references and literature used for the project are documented in:

```text
docs/literature/
```

---

# Acknowledgements

The project was carried out under the guidance of the Department of Electrical
Engineering at Indian Institute of Technology Indore.

The development benefited from laboratory facilities, fabrication resources,
technical support and assistance with mechanical and electronic integration.

---

# License

This repository is intended for academic, educational and research purposes.

Refer to `LICENSE` for applicable terms.

---

<p align="center">

<b>Underwater Search and Rescue Robot</b>

<br>

Department of Electrical Engineering  
Indian Institute of Technology Indore

<br><br>

<i>Design • Build • Test • Improve</i>

</p>
