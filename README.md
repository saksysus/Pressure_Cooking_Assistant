# Project² — Projected Interactive Engineering Battlefield

## Final Project README

> **Hackathon:** Skill Lab Practical Hackathon 2026
> **Project type:** Playful, interactive, technology-based experience
> **Repository naming rule:** Rename the fork to `SKILLLAB_PROR-2026-TeamName`.
> **Documentation rule:** Complete every section; write `Not applicable` with an explanation where necessary.

## 1. Team Identity

### 1.1 Studio / Group Name

`Project²`

### 1.2 Team Members

| Name | Primary role | Secondary role | Strengths |
|---|---|---|---|
| Gopalakrishnan | Software, electronics | Documentation | Systems thinking, communication |
| KAder Shaikh | Electronics, fabrication | Software | Hardware integration, fabrication |

### 1.3 Project Title

**Project²: Projected Interactive Engineering Battlefield**

### 1.4 One-Line Pitch

An interactive projected battlefield where a physical, Wi-Fi-controlled vehicle turns engineering learning into a playable challenge.

## Executive Summary

| Area | Summary |
|---|---|
| Problem | Engineering concepts can be difficult to understand when they are presented only as abstract diagrams or screen simulations. |
| Deterministic solution | A camera-tracked vehicle, laptop game loop, projector, and ESP32 execute a repeatable sensing → validation → command → actuation loop with a safe motor timeout. |
| Key quantifiable impact | The final submission must report command latency, tracking update rate/error, timeout duration, MCU utilization, and mission completion rate in [Results and Performance Metrics](#175-results-and-performance-metrics). |

### 1.5 Expanded Project Idea

Project² combines projection mapping, camera-based tracking, and a small motorized vehicle. A player navigates the vehicle through a projected environment while the laptop handles the game world and the ESP32 handles real-time motion. The experience makes engineering concepts tangible through movement, feedback, obstacles, and repeated problem-solving.

## 2. Philosophy Fit

### 2.1 Experience, Not Social Problem

This project is intentionally a playful interactive experience rather than a solution to a large social problem. Its goal is to make engineering exploration engaging, physical, and memorable.

## 3. Inspiration

### 3.1 References

| Source | Contribution |
|---|---|
| Projection-mapping interactive experiences | Inspired the combination of projected visuals and physical interaction. |
| PUBG-style battlefield games | Inspired the obstacle, mission, and progression structure. |
| Camera-tracked robotics projects | Inspired marker-based position tracking and feedback. |

### 3.2 Original Twist

The project connects a projected digital battlefield to a real moving vehicle. The player does not only control a screen avatar: the physical machine, its motors, the projection, and the camera-tracking loop all participate in the experience.

## 4. Project Intent

### 4.1 User Journey

1. The user starts the laptop game and places the vehicle in the marked play area.
2. The camera detects the vehicle marker and the projected battlefield appears.
3. The user sends movement commands through the game interface.
4. The ESP32 drives the motors while the camera updates the vehicle position.
5. The game checks boundaries, obstacles, and objectives, then provides projected feedback.
6. The user completes or restarts the mission and iterates on their strategy.

## 5. Definition of Success

### 5.1 Definition of “Usable”

The system is usable when a new player can start a session, control the vehicle, see the projected environment, understand the objective, and recover safely when communication or tracking stops.

### 5.2 Minimum Usable Version

The minimum version is a stable ESP32-controlled two-motor vehicle, a laptop control interface, a camera-tracked play area, and a projected obstacle course with one completable objective.

### 5.3 Stretch Features

- Multiple levels and mission types
- Collision feedback and scoring
- More accurate projection calibration
- Wireless telemetry and replay
- Additional vehicles or cooperative play

## 6. System Overview

### 6.1 Project Type

- [x] Electronics-based
- [ ] Mechanical-only
- [x] Sensor-based
- [x] App-connected
- [x] Motorized
- [ ] Sound-based
- [x] Light/projection-based
- [x] Screen/UI-based
- [x] Fabricated structure
- [x] Game-logic-based
- [x] Installation
- [ ] FPGA-based

### 6.2 High-Level System Description

The camera observes the physical vehicle and the laptop converts its position into game coordinates. The laptop renders the projected battlefield and sends movement commands over Wi-Fi. The ESP32 translates those commands into PWM motor control. A command timeout stops the motors so loss of communication fails safely.

### 6.3 Input / Output Map

| System part | Type | Function |
|---|---|---|
| Camera | Input/sensing | Detects the vehicle marker and pose |
| Laptop game | Processing/UI | Tracks state, renders projection, sends commands |
| ESP32 | MCU/PS processing | Receives commands and controls motor outputs |
| L298N | Actuation driver | Provides bidirectional motor drive |
| Two BO motors | Actuation | Move the vehicle |
| Projector | Output | Displays the battlefield, obstacles, and feedback |

## 7. Sketches and Visual Planning

### 7.1 Concept Sketch

Replace this line with the uploaded concept sketch:

`[Missing asset: ./images/concept-sketch.png]`

### 7.2 Labeled Build Sketch

Replace this line with a labeled build sketch showing structure, electronics, user touch points, moving parts, and outputs:

`[Missing asset: ./images/labeled-build-sketch.png]`

### 7.3 Approximate Dimensions

| Dimension | Current value |
|---|---:|
| Length | 16 cm |
| Width | 16 cm |
| Height | 8 cm |
| Estimated weight | 400 g |

## 8. Electronics Planning

### 8.0 Hardware Setup

Mount the two motor-and-wheel assemblies to the vehicle chassis, connect both motors to the L298N output terminals, connect the L298N control inputs to the documented ESP32 pins, and route regulated power from the buck converter to the ESP32. Place the camera so the full marked play area is visible and align the projector with the same area. Verify common ground, polarity, and an emergency motor stop before testing.

### 8.1 Electronics Used

| Component | Quantity | Purpose |
|---|---:|---|
| ESP32, 38-pin | 1 | Wi-Fi command receiver and motor controller |
| L298N motor driver | 1 | Bidirectional drive and PWM speed control |
| BO motor and wheel assemblies | 2 | Vehicle propulsion |
| Buck converter | 1 | Regulated ESP32 supply |
| Li-ion battery pack and holder | 1 | Portable power |
| Laptop | 1 | Game logic, camera processing, and projection |
| Camera | 1 | Vehicle tracking |
| Projector | 1 | Battlefield display |

### 8.2 Hardware-Software Co-Design Breakdown

| Layer | Responsibility | Implementation | Verification evidence |
|---|---|---|---|
| FPGA / PL | Hardware acceleration or programmable logic | Not applicable; no FPGA source or board is present in this repository | Mark not applicable in the final submission |
| MCU / PS | Command parsing, timeout safety, PWM, direction control | ESP32 firmware (source not yet present) | Firmware flash log and motor test |
| Sensing | Vehicle pose and position | Camera plus marker detection on the laptop | Tracking screenshot/video and measured error |
| Actuation | Physical movement and visual feedback | L298N, two BO motors, projector | GPS-tagged hardware photos and movement test |

### 8.3 Wiring Plan

The ESP32 uses GPIO 18, 19, 22, and 23 for motor direction signals IN1–IN4, and GPIO 25 and 26 for ENA/ENB PWM speed control. The motor driver is powered from the battery pack; the ESP32 is supplied through the buck converter. All grounds must be common. The laptop connects the camera and projector and communicates with the ESP32 over Wi-Fi.

### 8.4 Circuit Diagram

`[Missing asset: ./images/circuit-diagram.png]`

### 8.5 Pinout Configuration

| ESP32 pin | Signal | Connected component | Purpose |
|---:|---|---|---|
| GPIO 18 | IN1 | L298N | Left motor direction |
| GPIO 19 | IN2 | L298N | Left motor direction |
| GPIO 22 | IN3 | L298N | Right motor direction |
| GPIO 23 | IN4 | L298N | Right motor direction |
| GPIO 25 | ENA | L298N | Left motor PWM |
| GPIO 26 | ENB | L298N | Right motor PWM |
| GND | Ground | Battery, driver, ESP32 | Common reference |

Board reference image:

<p align="center">
  <img src="./images/Shrike-9-1-768x628.png" width="400" alt="Shrike board reference; upload the missing image before submission">
</p>

## 9. Power Plan

| Question | Response |
|---|---|
| Power source | Li-ion battery pack |
| Motor voltage | Approximately 6–8.4 V through the motor driver |
| MCU voltage | Regulated 5 V through the buck converter |
| Current concern | Motor startup current can cause voltage drops and Wi-Fi instability |
| Safety | Protect against shorts and over-discharge; secure all wiring before operation |

## 10. Software Planning

### 10.1 Software Tools

| Tool/platform | Purpose |
|---|---|
| MicroPython or Arduino-compatible ESP32 firmware | Motor control and Wi-Fi endpoint |
| Python, Pygame, and OpenCV | Game logic, marker tracking, and projection |
| CAD/fabrication tools | Vehicle and enclosure design |

### 10.2 Software Logic

The firmware initializes GPIO and PWM, starts Wi-Fi, accepts movement commands, and stops the motors after a short command timeout. The laptop captures camera frames, detects the marker, maps the pose into game coordinates, evaluates obstacles, renders the projection, and sends permitted commands. A reset returns the vehicle and game state to a known starting condition.

### 10.3 Step-by-Step Methodology and Algorithm Execution Flow

1. Initialize camera, projection, game state, Wi-Fi, GPIO, and PWM.
2. Capture a camera frame and detect the vehicle marker.
3. Convert marker position and orientation into play-area coordinates.
4. Read player input and validate the requested move against boundaries and obstacles.
5. Send the allowed command to the ESP32.
6. Set motor direction and PWM duty cycle.
7. Refresh the projected scene and record the current state.
8. Stop motors on timeout, invalid state, emergency reset, or loss of communication.
9. Repeat until the mission is complete or restarted.

## Repository Directory Tree

```text
.
├── Instructions.md
├── README.md
├── code_files/
│   └── readme
├── docs/
│   └── .gitkeep
└── images/
    └── .gitkeep
```

## Prerequisites and Build / Flash Instructions

The current checkout contains documentation only; implementation files and dependency manifests are still required. Before the final submission, add the ESP32 firmware and laptop application to `code_files/`, then follow the reproducible guide in [`code_files/readme`](./code_files/readme). Required prerequisites are an ESP32 toolchain, USB serial access, Python with the recorded tracking/game dependencies, a camera, and a projector.

## 11. Bill of Materials

### 11.1 Full BOM

| Item | Qty | In kit? | Buy? | Estimated cost | Specification | Rationale |
|---|---:|---|---|---:|---|---|
| ESP32 | 1 | Yes | No | 0 | 38-pin board | Wi-Fi MCU and PWM |
| L298N | 1 | Yes | No | 0 | Dual H-bridge | Drives both motors |
| BO motors and wheels | 2 | No | Yes | 150 | 6 cm wheels | Continuous vehicle motion |
| Buck converter | 1 | No | Yes | 75 | Adjustable regulator | Stable MCU supply |
| Li-ion battery pack/holder | 1 | No | Yes | 200 | Protected pack preferred | Portable power |
| Projector | 1 | Shared | No | 0 | External display | Projects game world |
| Camera | 1 | Shared | No | 0 | Webcam or phone | Marker tracking |

### 11.2 Material Justification

DC motors provide continuous rotation for a small vehicle and are simpler for differential drive than steppers. The L298N supplies bidirectional control and PWM speed control. Camera tracking avoids requiring the ESP32 to estimate its own global position.

### 11.3 Items You Chose

| Item | Why needed | Procurement/status |
|---|---|---|
| BO motors and wheels | Vehicle drive | Report final vendor and receipt status |
| Buck converter | Stable ESP32 supply | Report final vendor and receipt status |
| Li-ion battery pack | Portable power | Report chemistry, protection, and receipt status |

### 11.4 Budget Summary

| Budget item | Estimated cost |
|---|---:|
| Electronics | 400 |
| Mechanical parts | 200 |
| Fabrication materials | 0 (available on campus) |
| Purchased extras | 0 |
| Contingency | 300 |
| **Total** | **900** |

### 11.5 Budget Reflection

The design minimizes cost by using shared laptop, camera, and projector equipment. If the budget is reduced, retain the ESP32, driver, motors, and safe power regulation first; simplify the enclosure and projection environment before removing safety-critical hardware.

## 12. Planning the Work

### 12.1 Team Working Agreement

Divide hardware, software, fabrication, testing, and documentation into owned tasks. Review the build after each two-hour block, record failures as well as successes, and commit incremental progress rather than waiting until the final hour.

### 12.2 Task Breakdown

| Task | Owner | Dependency | Status |
|---|---|---|---|
| Finalize interaction and play area | Both | None | Complete |
| Assemble vehicle and motor driver | KAder Shaikh | BOM | Report final status |
| Implement firmware | Gopalakrishnan | Wiring | Source missing |
| Implement tracking and game loop | Gopalakrishnan | Camera setup | Source missing |
| Integrate and test | Both | Hardware and software | Report final status |
| Capture evidence and finalize README | Both | Working prototype | In progress |

### 12.3 Responsibility Split

| Area | Main owner | Support owner |
|---|---|---|
| Concept | Gopalakrishnan | KAder Shaikh |
| Electronics | KAder Shaikh | Gopalakrishnan |
| Coding | Gopalakrishnan | KAder Shaikh |
| Mechanical build | KAder Shaikh | Gopalakrishnan |
| Testing | Both | — |
| Documentation | Gopalakrishnan | KAder Shaikh |

## 13. 2-Hour Milestones

### 13.1 8-Hour Plan

| Block | Deliverable |
|---|---|
| Hours 0–2 | Finalize concept, sketch, BOM, and feasibility test |
| Hours 2–4 | Test electronics, build vehicle, and begin software |
| Hours 4–6 | Integrate camera, game loop, projection, and vehicle |
| Hours 6–8 | Playtest, fix failures, capture evidence, and complete documentation |

### 13.2 Update Log

| Date/block | Planned goal | Actual result | Change | Next step |
|---|---|---|---|---|
| TBD | Complete after each work block | TBD | TBD | TBD |

## 14. Risks and Unknowns

### 14.1 Risk Register

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Wi-Fi instability | Medium | High | Stable power, short command timeout, safe stop |
| Motor noise or voltage drop | Medium | High | Separate regulated supply path and common ground |
| Marker occlusion | Medium | Medium | Improve lighting, marker placement, and camera angle |
| Projection misalignment | Medium | Medium | Calibrate play-area corners before each demo |
| Loose wiring | Low | High | Strain relief and preflight inspection |

### 14.2 Biggest Unknown Right Now

The repository does not contain the firmware, tracking code, measured performance logs, or final evidence photos. These must be added and verified before the final commit.

## 15. Testing

### 15.1 Technical Testing Plan

| What needs testing | Method | Success condition |
|---|---|---|
| Wi-Fi command path | Send each movement endpoint repeatedly | Correct motor response with no unsafe stale motion |
| Motor direction/PWM | Test each channel independently | Direction and speed match the command |
| Timeout safety | Stop sending commands | Motors stop within the documented timeout |
| Marker tracking | Move vehicle through the full area | Position remains within the documented error |
| Collision logic | Approach each obstacle | Invalid move is blocked or reported |
| Projection alignment | Compare projected and physical landmarks | All play-area boundaries are usable |

### 15.2 Testing and Debugging Log

| Date | Problem | Type | Action | Result | Next action |
|---|---|---|---|---|---|
| TBD | Add one row per test | TBD | TBD | TBD | TBD |

### 15.3 Playtesting Notes

| Tester | Action | Confusion | Enjoyment | Change |
|---|---|---|---|---|
| TBD | TBD | TBD | TBD | TBD |

## 16. Build Documentation

### 16.1 Fabrication Process

Document CAD or sketching, cutting, assembly, fastening, wiring, surface finishing, projection setup, and revisions. Keep the vehicle modular so electronics can be replaced without damaging the structure.

### 16.2 Build Photos

Add dated photos for the concept, wiring, vehicle, tracking setup, testing, and final build. Use repository-relative links only after uploading the files to `images/`.

## 17. Final Outcome

### 17.1 Final Description

Project² is a projected, camera-tracked battlefield in which a physical Wi-Fi-controlled vehicle completes a visual mission. The final description must be updated after the last integrated test.

### 17.2 What Works Well

Report verified strengths with evidence, such as repeatable motor control, clear projection, reliable tracking, or successful first-time user completion.

### 17.3 What Still Needs Improvement

Report observed limitations, measured where possible: tracking error, response latency, projection calibration, battery life, or mechanical stability.

### 17.4 What Changed From the Original Plan

The design moved from local position estimation toward camera-based tracking, allowing the vehicle to be controlled by a simpler differential-drive platform while the laptop maintains global game state.

### 17.5 Results and Performance Metrics

| Metric | Measured result | Target/method |
|---|---|---|
| Command-to-motor latency | TBD | Measure from laptop request to motor response |
| Tracking update rate | TBD | Record camera/game loop frequency |
| Position error | TBD | Compare detected pose with marked reference points |
| Command timeout | TBD | Measure stop time after communication loss |
| MCU resource utilization | TBD | Record firmware memory/CPU usage |
| Mission completion rate | TBD | Test with at least three runs |

### 17.6 GPS-Tagged Hardware Verification Photos

Upload GPS-tagged photos to `images/` and replace the missing links below. Do not claim GPS verification unless the metadata has been checked.

| Photo 1 | Photo 2 |
|---|---|
| `[Missing: ./images/gps-hardware-front.jpg]` | `[Missing: ./images/gps-hardware-rear.jpg]` |
| `[Missing: ./images/gps-test-setup.jpg]` | `[Missing: ./images/gps-final-demo.jpg]` |

## 18. Reflection

### 18.1 Team Reflection

Complete after the final review: what worked in the collaboration, what slowed the team down, and how the work was divided.

### 18.2 Technical Reflection

Complete after testing: lessons about Wi-Fi control, PWM, camera tracking, projection, power, and integration.

### 18.3 Design Reflection

Complete after playtesting: lessons about clarity, delight, physical interaction, accessibility, and iteration.

### 18.4 If You Had One More Hour

Prioritize measured calibration, a safer enclosure, clearer onboarding, and one additional playable mission.

## 19. Final Submission Checklist

- [ ] Repository renamed using the required team format
- [x] Mandatory README headings retained
- [x] Team identity and project intent documented
- [x] Architecture, BOM, pinout, power, and methodology documented
- [ ] Source files uploaded to `code_files/`
- [ ] Firmware and tracking instructions verified on a clean machine
- [ ] Concept, circuit, build, and flowchart images uploaded
- [ ] GPS-tagged hardware verification photos uploaded
- [ ] Measured latency, tracking, and resource metrics added
- [ ] Testing, playtesting, update log, and reflection completed
- [ ] Placeholder and broken links removed
