# Project Master Document

| Field | Value |
| --- | --- |
| Project | Recon Drone — Embedded & Robotics |
| Document version | 0.2 |
| Project phase | Requirements definition |
| Last updated | 2026-11-18 |

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
| M0 | Bench experiments: digital I/O, PWM, motor control, and communication | Planned |
| M1 | Manual rover: forward/reverse movement, rotation, wireless control, and failsafe stop; initially tested in direct view | Planned |
| M2 | FPV rover: onboard camera, live video, and driving through the video feed | Planned |
| M3 | Mechanical replica: compact chassis with two side-mounted wheels and a recognizable game-inspired design | Planned |
| M4 | Jump mechanism: controlled takeoff and continued operation after landing | Planned; advanced phase |

Milestones define an implementation sequence, not a reduction in final project requirements.

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

The automatic safety stop required by RF-08 is compatible with the manual-operation requirement in RF-10. It is not autonomous navigation.

### Candidate functionality not yet approved

- Proportional throttle and steering instead of fixed-speed commands.
- Curved paths during forward or reverse movement.
- Acceleration and deceleration ramps.
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
| Maximum ground speed | To be defined | Open |
| Overall dimensions and mass | To be defined | Open |
| Jump height and repeatability | To be defined | Open |

These values should be refined after the use cases, interface requirements, and system constraints have been agreed.

## 7. Open technical decisions

| Topic | Status |
| --- | --- |
| Main controller | Not selected. ESP32-S3 was discussed as a learning platform, not adopted as the final controller. |
| Command radio | Not selected. Wi-Fi, ESP-NOW, RC radio systems, and other options remain candidates. |
| Video transmission | Not selected. Video and control may share a link or use separate links. |
| Operator interface | Not selected. PC, smartphone, gamepad, RC transmitter, or a combination remain possible. |
| Motors, drivers, and wheels | Pending mechanical and performance requirements. |
| Camera and video processing | Pending latency, size, power, and image-quality requirements. |
| Battery and power regulation | Pending a power budget. |
| Chassis material and construction | Not selected. |
| Jump actuator and mechanism | To be developed in the advanced phase. |

**Architecture principle:** the wireless protocol is an implementation decision, not a functional requirement. The motor-control logic should not depend directly on the selected communication transport.

## 8. Planned acceptance tests

| ID | Test |
| --- | --- |
| TV-01 | Execute forward, reverse, rotation in both directions, and stop under manual control. |
| TV-02 | Receive control commands without a cable between the operator and robot. |
| TV-03 | Stop the motors after command loss within the subsequently approved timeout. |
| TV-04 | Navigate a simple test course using only the live video feed, in a controlled and safe area. |
| TV-05 | Operate from the onboard battery for the subsequently approved minimum runtime. |
| TV-06 | In the advanced version, perform a jump and remain operational after landing. |

Detailed test procedures and pass/fail thresholds will be added after the corresponding requirements are finalized.

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

## 10. Next decisions

1. Define the movement input model: fixed-speed/digital commands or proportional control.
2. Agree on measurable minimum performance for FPV, control response, and runtime.
3. Compare candidate architectures against those requirements before selecting components.

## Document maintenance

- Update this document when a decision is approved or a requirement changes.
- Keep approved requirements separate from unresolved design proposals.
- Use ADRs for significant architectural choices when multiple approaches have meaningful trade-offs.
- Write all project documentation in English, using concise and neutral technical language.
