# Repository Instructions — Recon Drone

## Project context

Recon Drone — Embedded & Robotics is a hobby project to build a compact, two-wheeled ground reconnaissance robot inspired by the standard drone in *Rainbow Six Siege*.

The project is also a learning exercise in embedded systems and electronics. Explanations should assume introductory experience and build up technical detail as needed.

## Source of truth

1. Read [docs/00_PROJECT_MASTER.md](docs/00_PROJECT_MASTER.md) before proposing architecture changes, selecting components, or implementing features.
2. Treat a decision as approved only when the project master explicitly marks it as approved.
3. Distinguish approved requirements from proposals, working assumptions, and unresolved questions.
4. Report conflicting documentation rather than silently choosing one interpretation.
5. Use the current repository state as the authoritative record. Prior chat messages may be incomplete or outdated.

## Document responsibilities

- **README.md:** short, stable project description and links to primary documentation. Do not add milestones, progress reports, requirement tables, or implementation detail.
- **docs/00_PROJECT_MASTER.md:** project scope, requirements, milestones, current status, assumptions, constraints, acceptance tests, and approved or pending decisions.
- **AGENTS.md:** workflow rules and documentation conventions. Do not duplicate the project requirements.
- **Architecture Decision Records:** the reasoning, alternatives, and consequences behind individual significant design choices.

Keep each piece of information in its designated document; link to that document from elsewhere instead of copying sections.

## Engineering workflow

- Define the requirement and acceptance criteria before selecting an implementation.
- Record design alternatives and relevant trade-offs.
- Prefer small, reproducible experiments with independent tests.
- Keep motor control, command communication, video acquisition, and safety handling as separate concerns.
- Identify dependencies when a change affects multiple subsystems.
- Check electrical, mechanical, and software compatibility before recommending components.
- Explain embedded and electronics concepts directly; do not assume specialist knowledge.

## Safety

- The robot must stop its motors when valid control commands are lost or expire.
- Perform initial motor tests with drive wheels off the ground.
- Do not drive motors directly from microcontroller GPIO pins.
- Use properly protected batteries and compatible chargers.
- Treat the jump mechanism as a separate mechanical and safety design problem.
- Respect privacy and applicable radio regulations.

## Documentation conventions

- Write all repository documentation in **English**.
- Use clear, concise technical language. Avoid emojis, promotional wording, unnecessary enthusiasm, and generic assistant-style prose.
- Use stable requirement identifiers. Document superseded requirements explicitly.
- Record significant architectural decisions as ADRs (Architecture Decision Records) when the alternatives and consequences warrant it.
- Update relevant documentation when a decision is approved.
- Do not present unconfirmed proposals as established design choices.
- Do not commit credentials, access tokens, passwords, personal data, or other secrets.
