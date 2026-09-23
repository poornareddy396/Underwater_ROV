# Underwater Search and Rescue Robot

<p align="center">
  <img src="media/images/final_bot.jpg" width="750">
</p>

<h2 align="center">
  Development of an Underwater Search and Rescue Robot
</h2>

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

The robot combines mechanical engineering, embedded systems, electronics,
computer vision, communication and underwater robotics into a single
integrated platform.

The system provides:

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

The repository contains the complete engineering workflow including mechanical
design, CAD models, electronics, firmware, software, computer vision,
experiments, testing, results and documentation.

---

# Project Motivation

Underwater environments are challenging for search and inspection operations
because of:

- Poor visibility
- Light attenuation
- Turbidity
- Variable depth
- Difficult underwater navigation
- Limited communication
- Difficult manual inspection
- Risk to human divers

Manual underwater search operations can become difficult when visibility is
poor or when the search area is large.

The objective of this project is to develop a remotely operated underwater
robot that can assist in such operations by providing:

1. Remote underwater movement
2. Controlled depth adjustment
3. Live underwater video
4. Real-time object detection
5. Remote actuator control
6. A modular platform for future sensing and autonomy

---

# Objectives

The major objectives of the project are:

- Design and fabricate an underwater robotic platform.
- Develop a reliable mechanical structure for underwater operation.
- Implement underwater propulsion using BLDC motors.
- Develop controlled vertical movement using variable buoyancy.
- Implement a stepper motor and lead-screw based syringe mechanism.
- Develop STM32 firmware for real-time actuator control.
- Integrate a Raspberry Pi 5 for high-level processing.
- Implement a web-based control interface.
- Establish reliable Raspberry Pi–STM32 communication.
- Integrate a low-light underwater camera.
- Implement YOLOv8 based human detection.
- Optimize computer vision inference for edge hardware.
- Develop and test the power architecture.
- Develop waterproofing and sealing techniques.
- Test individual subsystems and the complete robotic platform.

---

# System Architecture

The complete system follows a hierarchical control architecture.

```text
                         GROUND STATION
                              │
                              │
                           Laptop
                              │
                              │ Ethernet
                              │ Tether
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
                               │ USB CDC
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
                           │        │
                    ┌──────▼───┐ ┌──▼──────────┐
                    │ ESCs     │ │ A4988       │
                    │          │ │ Stepper     │
                    └────┬─────┘ └─────┬───────┘
                         │             │
                    ┌────▼─────┐       │
                    │   BLDC   │       ▼
                    │  Motors  │  Lead Screw
                    └──────────┘       │
                                       ▼
                                Syringe Mechanism
                                       │
                                       ▼
                                Buoyancy Control
