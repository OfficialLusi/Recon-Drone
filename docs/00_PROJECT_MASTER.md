# Project Master Document

| Field | Value |
| --- | --- |
| Project | Recon Drone — Embedded & Robotics |
| Document version | 0.9 |
| Project phase | Requirements definition |
| Last updated | 2026-11-23 |

This document is the authoritative record of project requirements, approved decisions, assumptions, and open issues.

**Decision rule:** a proposed design is not approved until its status is explicitly recorded as approved.

Requirement IDs were normalized in version 0.1 to resolve duplicates in the initial design notes. IDs should remain stable from this point onward.

## 1. Project scope

Design and build a compact unmanned ground vehicle (UGV) inspired by the standard reconnaissance drone in *Rainbow Six Siege*.

The vehicle will use two side-mounted drive wheels, carry its own battery, accept remote manual commands, and transmit live camera footage. FPV operation—driving using the video feed without direct line of sight—is a mandatory capability.

The advanced final version shall include a controlled jump. Autonomous navigation is outside the initial scope and may be considered later.

The project also provides practical experience in embedded C/C++, electronics, communications, motor control, mechanical design, integration, and testing.

## 2. Development milestones

| ID | Milestone | Status |
| --- | --- | --- |
| M0 | ESP32-based bench experiments: digital I/O, PWM, motor control, and communication | Planned |
| M1 | ESP32-based manual rover: forward/reverse movement, rotation, wireless control, and failsafe stop; initially tested in direct view, without camera hardware | Planned |
| M2 | Extend the working manual rover with camera and supporting video electronics; enable live video and driving through the video feed | Planned |
| M3 | Mechanical replica: compact chassis with two side-mounted wheels and a recognizable game-inspired design | Planned |
| M4 | Jump mechanism: controlled takeoff and continued operation after landing | Planned; advanced phase |

Milestones define an implementation sequence, not a reduction in final project requirements.

### Initial implementation approach

- Use an ESP32-family microcontroller as the movement controller for M0/M1. Select the exact ESP32 variant and development board after evaluating I/O, motor-control peripherals, firmware tooling, physical size, and expansion needs.
- Build and validate the powered, remotely operated two-wheel rover before integrating any camera hardware.
- Keep locomotion and safety logic on the movement controller when video is added in M2, rather than requiring a controller replacement.
- Introduce the camera and its supporting video electronics in M2. Video processing and transmission may be implemented by a separate module or another suitable arrangement; neither the topology nor the wireless protocol is approved yet.
- Reserve a practical integration path for later video hardware (power budget, physical space, and optional data interface). This is a design consideration, not a requirement to select video components during M1.
- Bench experiments may use a wired programming/debug interface. M1 must still meet the approved wireless manual-control and onboard-battery requirements.

### Current progress

**Completed**

- General product scope established.
- Manual remote control and FPV operation confirmed as requirements.
- Indoor and outdoor use confirmed.
- Controlled jumping assigned to the advanced phase.

**Pending**

- Define measurable performance thresholds, operator input characteristics, acceleration-ramp timing, and safe direction-reversal thresholds.
- Select the exact ESP32 development board for the M0/M1 motion controller and choose an initial wireless command path.
- Keep video architecture selection for M2, after the manual rover is operational.
- Select and validate hardware.
- Build the first bench prototype.

The initial architecture direction (ESP32-family movement controller first; camera and video electronics later) has been approved. The exact controller board, radio protocol, motor hardware, and video architecture have not been selected. No physical prototype has been completed.

## 3. Approved functional requirements

| ID | Requirement | Earliest milestone |
| --- | --- | --- |
| RF-01 | The robot shall move forward. | M1 |
| RF-02 | The robot shall move backward. | M1 |
| RF-03 | The robot shall rotate in place in both directions. | M1 |
| RF-04 | The robot shall receive operator commands over a wireless link, with no physical control cable. | M1 |
| RF-05 | The robot shall capture images through an onboard camera. | M2 |
| RF-06 | The robot shall transmit live images to the operator. | M2 |
| RF-07 | The robot shall operate from an onboard battery. | M1 |
| RF-08 | The robot shall stop its motors when valid commands are lost or expire, within a safety timeout yet to be specified. | M1 |
| RF-09 | The advanced final version shall perform a controlled jump. | M4 |
| RF-10 | Normal operation shall be manually controlled; movement is initiated by operator commands. | M1 |
| RF-11 | The robot shall support FPV driving using the camera feed without direct visual contact. | M2 |
| RF-12 | The robot shall support proportional control of forward/reverse motion and steering, including steering while moving. The operator shall be able to request intermediate drive levels rather than only fixed-speed movement. | M1 |
| RF-13 | The robot shall apply progressive acceleration when increasing the requested drive level, limiting abrupt increases in motor drive commands during normal operation. The ramp rate shall be defined and validated later. | M1 |
| RF-14 | When the operator releases the movement controls to neutral (zero throttle and zero steering), the robot shall immediately command zero drive output, bypassing any normal motion ramp. | M1 |
| RF-15 | When the operator reduces a nonzero throttle request without changing direction, the firmware shall apply the lower drive request without a software deceleration ramp. The resulting change in wheel speed is determined by the physical system. | M1 |
| RF-16 | The robot shall prevent immediate reversal of motor drive direction while the corresponding wheel is rotating above a defined speed threshold. Reverse acceleration shall begin only after the required safe reversal condition has been met. | M1 |

The automatic safety stop required by RF-08 is compatible with the manual-operation requirement in RF-10. It is not autonomous navigation.

### Candidate functionality not yet approved

- Battery status and radio-link telemetry.
- Autonomous paths and obstacle avoidance, which are potential later extensions.

These items must not be treated as mandatory requirements without further discussion.

## 4. Mechanical and physical requirements

| ID | Description | Status |
| --- | --- | --- |
| RM-01 | Compact, portable body | Objective confirmed; dimensions pending |
| RM-02 | Two side-mounted drive wheels | Approved |
| RM-03 | Camera integrated into the body | Approved |
| RM-04 | Electronics and battery carried onboard | Approved |
| RM-05 | Final appearance recognizably inspired by the game's drone | Approved; visual fidelity pending |
| RM-06 | Chassis protection for components during intended use | To be specified |

**Open mechanical issue:** two side-mounted wheels alone do not necessarily provide static stability. Chassis geometry, a possible additional contact point, and behavior during jumping and landing require evaluation.

## 5. Operating environment

| Topic | Current definition | Status |
| --- | --- | --- |
| Use locations | Indoor and outdoor environments | Approved |
| Initial terrain | Mostly regular surfaces with small irregularities | Working assumption; not a blocking constraint |
| Rough ground, gravel, and grass | Outside the initial target; may be evaluated later | Open |
| Water, rain, dust, and adverse weather | Environmental resistance not specified; do not assume the enclosure is weatherproof | Open |
| Initial testing | Manual, direct line-of-sight operation in a controlled area | Approved approach |
| Final driving mode | FPV must be supported | Approved |

## 6. Performance targets under discussion

**The figures below are preliminary suggestions, not approved specifications.** They will require confirmation and testing.

| Metric | Preliminary target | Status |
| --- | --- | --- |
| Runtime | At least 15 minutes | Not approved |
| Control range | At least 10 m | Not approved |
| Video resolution | At least 640 × 480 | Not approved |
| Video frame rate | At least 15 fps | Not approved |
| Video latency | Below 300 ms | Not approved |
| Maximum command-loss stopping time | 500 ms | Not approved |
| Acceleration ramp duration or maximum drive-command slew rate | To be defined | Open |
| Safe wheel-speed threshold for motor reversal | To be defined | Open |
| Maximum ground speed | To be defined | Open |
| Overall dimensions and mass | To be defined | Open |
| Jump height and repeatability | To be defined | Open |

These values should be refined after the use cases, interface requirements, and system constraints have been agreed.

## 7. Open technical decisions

| Topic | Status |
| --- | --- |
| Main controller | ESP32 family approved as the starting movement-control platform for M0/M1 and retained for motion control in M2. Specific chip and board remain open; ESP32-S3-DevKitC-1 is a candidate, not a final selection. |
| Command radio | Not selected. Wi-Fi, ESP-NOW, RC radio systems, and other options remain candidates. |
| Video transmission | Deferred until M2. Camera hardware, video processing, and transmission remain open; video and command communication may share a link or use separate links. |
| Operator interface | Not selected. PC, smartphone, gamepad, RC transmitter, or a combination remain possible. |
| Motor drive method | PWM-based modulation is the selected initial approach for variable motor output; the exact driver topology and control electronics remain open. |
| Direction-reversal feedback | Motor reversal is gated by a safe wheel-speed condition (RF-16). Encoder feedback, back-EMF estimation, current-based estimation, and timing models remain candidates; none is selected. |
| Motors, drivers, and wheels | Pending mechanical and performance requirements. |
| Camera and video processing | Pending latency, size, power, and image-quality requirements. |
| Battery and power regulation | Pending a power budget. |
| Chassis material and construction | Not selected. |
| Jump actuator and mechanism | To be developed in the advanced phase. |

**Architecture principle:** the wireless protocol is an implementation decision, not a functional requirement. The motor-control logic should not depend directly on the selected communication transport.

**Motion ramp design note:** RF-13 applies to increases in the normal commanded motor drive level, including startup. Its implementation may adjust PWM duty cycle gradually. It does not by itself guarantee a fixed physical acceleration under different loads. RF-14 requires an immediate transition of the drive command to neutral when all movement controls are released; this does not guarantee that the moving robot stops physically at that instant. The choice between active electronic braking and coasting remains open and depends on the motor and driver architecture. Under RF-15, a lower nonzero throttle request is applied without an explicit software deceleration ramp. A reduction in PWM duty cycle does not imply a proportional reduction in wheel speed; the speed response also depends on motor back-EMF, driver freewheeling/braking behavior, load, traction, and terrain. Under RF-16, a direction reversal must wait for a safe wheel-speed condition. The measurement or estimation method, speed threshold, stopping strategy, timeout, and behavior when feedback is unavailable remain to be specified. A safety stop required by RF-08 must also bypass the normal acceleration ramp; physical stopping distance and time must be tested.

**PWM design note:** PWM is the planned actuator-control technique, not the functional requirement itself. Changing PWM duty cycle controls the effective electrical drive delivered through a suitable motor driver; it does not by itself guarantee a particular wheel speed under varying load. Closed-loop speed regulation, feedback sensors, PWM frequency, resolution, and motor driver selection are not yet specified. PWM shall not be used to power a motor directly from a microcontroller GPIO.

## 8. Planned acceptance tests

| ID | Test |
| --- | --- |
| TV-01 | Execute forward, reverse, rotation in both directions, and stop under manual control. |
| TV-02 | Receive control commands without a cable between the operator and robot. |
| TV-03 | Stop the motors after command loss within the subsequently approved timeout. |
| TV-04 | Navigate a simple test course using only the live video feed, in a controlled and safe area. |
| TV-05 | Operate from the onboard battery for the subsequently approved minimum runtime. |
| TV-06 | In the advanced version, perform a jump and remain operational after landing. |
| TV-07 | Verify that neutral, intermediate, and full-range operator movement/steering commands produce appropriately varied drive commands; confirm PWM outputs at the motor-driver interface during bench testing. |
| TV-08 | Apply a step increase in requested drive from rest and between intermediate levels; measure a progressive rise in commanded motor drive instead of a single abrupt step. Verify separately that a simulated command-loss safety stop is not delayed by the acceleration ramp. |
| TV-09 | During movement, release all movement controls to neutral and verify that the firmware immediately commands neutral motor output without a deceleration ramp. Measure physical stopping behavior separately once the motor driver and chassis are available. |
| TV-10 | Reduce a nonzero throttle request while maintaining direction (e.g., from 100% to 40%) and verify that the firmware updates the requested motor drive without a software deceleration ramp. Measure actual wheel speed separately during hardware testing. |
| TV-11 | Request reversal while a wheel is rotating above the agreed safe threshold; verify that opposite-direction drive is inhibited until the safe wheel-speed condition is met. Define measurement method and pass/fail thresholds before testing. |

Detailed test procedures and pass/fail thresholds will be added after the corresponding requirements are finalized.

### Intended use and safety constraints

The robot is intended for hobby development and operation in controlled environments. The implementation and test plan must address:

- Safe behavior when remote commands stop arriving.
- Moving components and pinch points, particularly in the future jump mechanism.
- Suitable electrical protection and battery charging practices.
- Privacy of people who may be recorded by the camera.
- Applicable radio requirements for the selected communication hardware.

These constraints do not replace detailed hazard analysis or test procedures, which will be developed with the relevant subsystems.

## 9. Decision log

| Date | Decision or conclusion | Status |
| --- | --- | --- |
| 2026-11 | Build a two-wheeled ground robot inspired by the standard game drone. | Approved |
| 2026-11 | Require forward/reverse movement, rotation in place, and remote operation. | Approved |
| 2026-11 | Require onboard camera, live video, and FPV operation in the final system. | Approved |
| 2026-11 | Use manual driving; consider autonomous operation only as a later extension. | Approved |
| 2026-11 | Target both indoor and outdoor environments. | Approved |
| 2026-11 | Use surfaces with minor irregularities as the initial mechanical reference, without making this a blocking constraint. | Provisional |
| 2026-11 | Include controlled jumping in the advanced final version. | Approved |
| 2026-11 | Do not commit to Wi-Fi or ESP32-S3 as final design choices yet. | Open |
| 2026-11-23 | Require proportional operator control of movement and steering (RF-12). | Approved |
| 2026-11-23 | Use PWM-based motor drive as the initial control approach; specific motors and drivers remain to be selected. | Approved technical approach |
| 2026-11-23 | Require progressive acceleration for normal increases in motor drive command (RF-13), with ramp parameters to be defined. | Approved |
| 2026-11-23 | Releasing movement controls to neutral shall command an immediate stop without a deceleration ramp (RF-14); electronic braking method remains undecided. | Approved |
| 2026-11-23 | Reducing a nonzero throttle request in the same direction shall update the drive command without software deceleration ramp (RF-15). | Approved |
| 2026-11-23 | Require controlled motor direction reversal conditioned on wheel speed (RF-16). Encoder or sensorless estimation is not yet selected. | Approved |
| 2026-11-23 | Implement motion control first on an ESP32-family MCU (M0/M1); add camera and video electronics only after the manually controlled rover works (M2), retaining the movement controller. Exact ESP32 board and video architecture remain open. | Approved implementation sequence |

## 10. Next decisions

1. Select a specific ESP32 development board for M0/M1 based on available GPIO, PWM peripherals, potential encoder inputs, debugging interfaces, and anticipated expansion.
2. Select the M1 command-link architecture and a minimal operator input method, without yet selecting the M2 video display or transmission technology.
3. Plan the motor driver, power supply, and the first bench tests; refine acceleration-ramp parameters and safe direction-reversal implementation.
4. Revisit camera, video performance, and FPV architecture after the manual rover is functional.

## 11. Attribution

*Tom Clancy's Rainbow Six Siege* is a Ubisoft title. Recon Drone is an independent, unofficial hobby project.

## Document maintenance

- Update this document when a decision is approved or a requirement changes.
- Keep approved requirements separate from unresolved design proposals.
- Use ADRs for significant architectural choices when multiple approaches have meaningful trade-offs.
- Write all project documentation in English, using concise and neutral technical language.
