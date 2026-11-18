# Recon Drone — Embedded & Robotics

A hobby robotics project to design and build a small, two-wheeled ground reconnaissance robot inspired by the standard drone in *Tom Clancy's Rainbow Six Siege*.

**Project status:** requirements definition. No final hardware platform, wireless protocol, or components have been selected.

## Objectives

The robot shall:

- Move forward and backward, and rotate in place in both directions.
- Receive manual control commands over a wireless link.
- Capture and transmit live video.
- Support first-person-view (FPV) operation without direct visual contact.
- Operate from an onboard battery.
- Use a compact chassis with two side-mounted drive wheels.
- Perform a controlled jump in the advanced version.

The project also serves as a practical introduction to embedded programming, electronics, motor control, wireless communication, mechanical design, and system testing.

## Development milestones

| Milestone | Scope |
| --- | --- |
| M0 — Bench tests | GPIO, PWM, motor control, and communication experiments |
| M1 — Manual rover | Remote movement control, initial line-of-sight testing, and failsafe stop |
| M2 — FPV rover | Onboard camera, live video, and video-based driving |
| M3 — Mechanical replica | Compact two-wheel chassis based on the game's drone |
| M4 — Jump mechanism | Controlled jump and recovery after landing |

Autonomous navigation and obstacle avoidance are potential future extensions, not requirements for the initial complete version.

## Project documentation

- [Project master document](docs/00_PROJECT_MASTER.md): approved requirements, assumptions, open decisions, and development status.
- [Repository working instructions](AGENTS.md): engineering and documentation rules for work in this repository.

Design notes, decision records, hardware documentation, firmware, and tests will be added as the project develops.

## Decision management

A proposed solution is not an approved decision.

The files in this repository are the authoritative project record. Discussions may lead to new proposals, but approved decisions must be recorded in version-controlled documentation.

## Current status

- [x] General project scope defined.
- [x] Manual control and FPV operation confirmed.
- [x] Indoor and outdoor use confirmed.
- [ ] Complete movement-control and measurable performance requirements.
- [ ] Evaluate system architecture and communication options.
- [ ] Build and test the first prototype.

## Safety and intended use

The robot is intended for hobby use in controlled environments. Tests must account for loss of control, moving components, battery safety, and the privacy of people who may appear in camera footage.

## Attribution

*Tom Clancy's Rainbow Six Siege* is a Ubisoft title. This is an independent, unofficial hobby project.
