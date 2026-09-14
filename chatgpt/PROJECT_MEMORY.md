# Codename Expanse – Project Memory

## Purpose

This file provides durable cross-session continuity for **cross-topic design premises** that may become relevant in future concept sessions.

It is **not** a replacement for normative project documentation. Approved documents under `docs/vision/**`, `docs/concepts/**`, `docs/architecture/**` and approved ADRs remain authoritative according to the repository source hierarchy.

## Memory scope rule

Store only decisions that are likely to matter in a **different future concept topic** and that could otherwise be lost between sessions.

Do **not** store:
- detailed decisions from the concept currently being worked on;
- active-session progress or question state;
- information already safely captured in the current concept document;
- temporary implementation or discussion notes.

Current-topic decisions belong in the active concept document and conversation. If a remembered cross-topic premise later becomes normative in its owning concept, prefer the normative concept and remove stale duplication here when practical.

## Session startup rule

At the start of every new concept-design session, read this file after `chatgpt/PROJECT_INSTRUCTIONS.md` and before the detailed Concept Writer context/workflow. Then load the current vision, concept index and all relevant approved concepts as usual.

If this file conflicts with an approved concept, the approved concept wins. Surface the conflict instead of silently choosing the memory entry.

## Cross-topic design premises

### Propulsion signatures and detection

This premise originated during flight/autopilot design but is intentionally retained because it directly affects later **Sensor/Detection, Travel, Combat, Stealth and AI** concepts:

- **Active propulsion produces detectable signatures.** Acceleration, braking and other thrust events can reveal a ship to suitable detectors/sensors.
- Coasting without active propulsion can therefore be strategically valuable because it reduces or avoids propulsion-generated detection signatures.
- A time-optimal transfer may spend much of the journey thrusting and can therefore be comparatively easy to detect.
- A player may intentionally accept substantially longer travel time in order to coast for most or all of a route and reduce detectability.
- The intended systemic trade-off is **travel time vs. propulsion exposure / detectability**.
- Exact sensor equations, signature falloff, detector ranges, thermal behaviour and detection thresholds are not defined here and belong to the future Sensor/Detection concept.

### Ship heat, thermal management and thermal signatures

This premise originated during celestial-body design but is intentionally retained because it directly affects later **Ships, Modules, Weapons, Propulsion, Thermal Management, Sensors/Detection and Stealth** concepts:

- Ships accumulate internal heat from high-energy activity such as sustained or overloaded propulsion and laser-weapon use.
- Ships have a baseline passive rate at which excess heat can be rejected to space.
- Ship/module choices may improve passive heat rejection.
- Active heat-ejection systems may deliberately remove stored heat more quickly.
- Excessive thermal load can overheat ship systems and eventually cause damage; the exact thresholds and damage model belong to later owning concepts.
- Proximity to strong stellar radiation can add external thermal load and may cause warnings, system problems, overheating or hull/system damage when a ship approaches a star too closely.
- **Heat is also a sensor-relevant signature.** Thermal management therefore serves both survivability/performance and stealth.
- A stealth-oriented ship should be able to manage, store and/or reject heat in ways that reduce detectable thermal exposure, with trade-offs defined by later Thermal and Sensor/Detection concepts.
- Exact heat equations, capacities, dissipation rates, heat-ejector mechanics, signature equations and sensor thresholds are intentionally deferred to their owning future concepts.

## Maintenance rule

Add an entry only when a decision from the current discussion has clear relevance to a **different future topic**. Keep entries concise and topic-agnostic. Do not use this file as a running session log.