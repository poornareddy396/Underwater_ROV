# Underwater Search & Rescue ROV

> **A tethered underwater robotic platform for search, visual inspection, and assisted recovery in low-visibility environments.**

A multidisciplinary prototype integrating **mechanical design, embedded control, underwater propulsion, variable buoyancy, live video, and computer vision**. The current BTP cycle focuses on turning the earlier bench-tested platform into a more reliable, water-ready system by addressing the mechanical sealing and system-level thermal limitations identified during testing.

---

## Overview

Underwater search and recovery is challenging because of light attenuation, turbidity, hydrostatic pressure, and limited visibility. The project develops a compact ROV that keeps the operator in the loop while providing controlled underwater motion, live video, and machine-learning-assisted detection.

The system uses a **Raspberry Pi 5** for high-level communication, video handling and software, while an **STM32F4 BlackPill** handles timing-sensitive actuator control.

![Final assembled underwater bot](mechanical/iteration_2/final_assembled_bot.png)

---

## Key Features

- Tethered operator-controlled ROV
- Raspberry Pi 5 + STM32F4 dual-controller architecture
- Twin BLDC thrusters with ESC-based control
- Lead-screw / syringe mechanism for depth control
- On-board low-light camera
- Web-based control and live video interface
- YOLOv8-based lightweight detection pipeline
- Iterative mechanical sealing and underwater validation
- Modular construction for further field testing

---

## System Architecture

The operator communicates with the robot through a tethered ground station. The Raspberry Pi handles high-level communication, camera streaming and software, while the STM32 provides real-time actuator control.

![System connection diagram](schematics/overall_system_connection_diagram.png)

The software and electronics architecture was retained from the earlier prototype while the current work concentrated on reliability and deployment constraints.

![Communication and connection flow](schematics/communication_connection_flow.png)

---

# Mechanical Design Evolution

A major part of this BTP cycle was identifying why the previous mechanical enclosure could not survive underwater operation and replacing the sealing concept rather than repeatedly modifying the same design.

## 1. Failure Analysis — Previous Prototype

The first-generation enclosure used **3D-printed ABS end caps with an O-ring-based sealing arrangement**. During pool testing, water entered through the printed material/infill regions and through the interface between the end cap and acrylic tube.

A second limitation was observed at the system level: running YOLOv8 directly on the Raspberry Pi inside the sealed enclosure produced a significant thermal load, causing the enclosed system to overheat and shut down.

These tests established two separate design requirements:

1. The enclosure required a more uniform, pressure-resistant sealing method.
2. Heavy ML computation should not be treated as an on-board thermal load inside the sealed volume.

---

## 2. Mechanical Design Iteration 1 — “Bottle-Cap” Threaded Seal

The first redesign attempted to solve the leakage problem using a **threaded bottle-cap style enclosure**. Two threaded components were fixed to the acrylic tube and complementary caps were used to close the ends.

The design was strengthened using:

- 100% infill for the printed components
- RTV silicone at the acrylic/printed interface
- PTFE/Teflon tape on the threads
- Custom two-part silicone gaskets
- Grease as a secondary moisture barrier

Despite these measures, underwater testing still showed leakage through the threaded region.

![Iteration 1 pool test](mechanical/iteration_1/iteration_1_pool_test.jpg)

### Why Iteration 1 failed

The main problem was the **threaded pressure-sealing interface**. 3D-printed threads contain small dimensional and layer-level irregularities, making it difficult to maintain a continuous sealing surface under external hydrostatic pressure. The combination of thread gaps and prolonged submersion ultimately allowed water ingress.

The internal fill test initially appeared successful, but the external submerged test exposed the pressure-dependent leakage that the internal test could not reproduce.

**Design decision:** instead of improving the threads further, the sealing principle itself was changed.

---

## 3. Mechanical Design Iteration 2 — Through-Rod Compression Seal

The final mechanical approach moved to a **flat-face compression gasket**, similar in principle to a flanged pressure-vessel joint.

The threaded 3D-printed end caps were removed and replaced by:

- 8 mm laser-cut circular acrylic end plates
- Custom two-part silicone gasket seated in machined cavities
- Polished acrylic tube edges for improved gasket contact
- Six M8 threaded steel rods running along the tube
- Uniform clamping force applied through nuts/wedges

![Through-rod compression assembly](mechanical/iteration_2/through_rod_compression_assembly.jpg)

The design creates a distributed axial clamping force instead of depending on the dimensional accuracy of printed threads.

![Final compression assembly](mechanical/iteration_2/final_assembled_bot.png)

### Validation

The redesigned enclosure was submerged for **more than 12 minutes continuously with zero observed water ingress** during the reported test.

This was the key mechanical improvement of the current BTP cycle: the sealing problem was addressed by changing from a threaded printed interface to a uniformly compressed gasket joint.

---

## 4. Final Mechanical Integration

The final Fusion 360 model integrates the enclosure, internal structural elements, propulsion arrangement and depth-control mechanism into one platform.

![Final Fusion 360 model](mechanical/iteration_2/fusion_360_final_model.png)

The lead-screw mechanism provides controlled movement of the depth-control assembly and forms part of the retained 3-DOF architecture:

- Forward / backward motion
- Left / right differential thrust
- Depth control through the lead-screw mechanism

![Lead screw mechanism](mechanical/iteration_2/lead_screw_mechanism.png)

The assembled prototype was subsequently taken into pool testing to verify the mechanical and propulsion integration under water.

![Pool testing](mechanical/iteration_2/final_assembled_bot.png)

---

## Electronics & Control

The electronics use a hierarchical architecture:

| Subsystem | Hardware | Main role |
|---|---|---|
| Ground station | Laptop | Operator interface and external ML processing |
| High-level controller | Raspberry Pi 5 | Communication, camera and software |
| Real-time controller | STM32F4 BlackPill | PWM, motor and actuator control |
| Propulsion | BLDC motors + ESCs | Forward/lateral movement |
| Depth control | Stepper + lead screw | Controlled depth adjustment |
| Vision | Low-light camera | Live underwater video |

The electronics and connection architecture from the previous prototype was retained while the mechanical enclosure and compute architecture were improved.

---

## Compute & Vision Architecture

The earlier system attempted to execute the detection pipeline directly on the sealed Raspberry Pi. Testing showed that the resulting thermal load was unsuitable for prolonged operation inside the enclosure.

The current architecture therefore moves heavy inference to the ground station:

```text
Underwater Camera
       │
       ▼
 Raspberry Pi
       │
       │ Ethernet tether
       ▼
 Ground-Station PC
       │
       ▼
 YOLOv8 / NCNN
       │
       ▼
 Detection + Live Video
```

This reduces the computational and thermal burden inside the sealed robot while retaining real-time visual feedback.

---

## Current Status

**Prototype integration and validation stage**

- Mechanical sealing redesign completed
- Through-rod compression enclosure tested successfully
- Zero observed water ingress for >12 minutes in the reported submerged test
- STM32 + Raspberry Pi control architecture re-established
- Stepper / lead-screw depth mechanism bench-tested
- Web-based control interface operational
- Camera and video pipeline integrated
- Ground-station ML offload architecture established
- Pool-level mechanical/propulsion testing performed

The remaining work is focused on complete system integration, feedthrough sealing, internal/external mounting, buoyancy balancing and longer-duration end-to-end testing.

---

## Next Steps

- Seal and validate Ethernet, motor and syringe feedthroughs
- Finalize internal and external component mounts
- Complete ground-station YOLO processing pipeline
- Finalize dedicated Raspberry Pi power delivery
- Balance the center of gravity and buoyancy
- Perform extended tests in turbid water
- Evaluate long-duration thermal and waterproofing performance

---

## Repository Structure

```text
Underwater_ROV/
├── mechanical/
│   ├── iteration_1/
│   ├── iteration_2/
│   └── README.md
├── schematics/
│   ├── schematics_and_components.pdf
│   ├── hand_drawn_electrical_wiring.png
│   ├── overall_system_connection_diagram.png
│   └── communication_connection_flow.png
├── firmware/
│   └── stm32/
├── software/
│   └── raspberry_pi/
├── scripts/
├── README.md
├── LICENSE
└── CHANGELOG.md
```

---

## Technology Stack

**Embedded:** STM32F4 · STM32CubeIDE · C · PWM · GPIO  
**Compute:** Raspberry Pi 5 · Python · NCNN  
**Vision:** YOLOv8n · OpenCV · Camera  
**Mechanical:** Fusion 360 · Acrylic · 3D Printing · Laser-cut acrylic  
**Propulsion:** BLDC motors · ESCs · Stepper motor  
**Communication:** Ethernet tether · USB CDC

---

## Project Context

**B.Tech Project — Electrical Engineering, IIT Indore**

The project combines mechanical engineering, embedded systems, electronics, communication, and computer vision to develop a practical underwater search-and-rescue platform.

---

## License

See [`LICENSE`](LICENSE) for licensing information.
