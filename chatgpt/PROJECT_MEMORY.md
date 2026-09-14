# Codename Expanse – Project Memory

## Purpose

This file provides durable cross-session continuity for ChatGPT concept work. It exists because product-level ChatGPT memory may be unavailable or disabled for this project.

It is **not** a replacement for normative project documentation. Approved documents under `docs/vision/**`, `docs/concepts/**`, `docs/architecture/**` and approved ADRs remain authoritative according to the repository source hierarchy.

Use this file for:
- active concept-session continuity;
- important user intent that has not yet been promoted into a normative concept;
- cross-cutting design premises that future sessions must not lose;
- the current design focus and next unresolved decisions.

Do not use this file to silently override an approved concept. When a remembered decision becomes normative, move or duplicate it into the correct concept document and keep this file as a concise continuity summary.

## Session startup rule

At the start of every new concept-design session, read this file after `chatgpt/PROJECT_INSTRUCTIONS.md` and before the detailed Concept Writer context/workflow. Then load the current vision, concept index and all relevant approved concepts as usual.

If this file conflicts with an approved concept, the approved concept wins. Surface the conflict instead of silently choosing the memory entry.

## Current project continuity

### Approved foundations

- `docs/concepts/flight-physics.md` is approved and defines the authoritative physical movement model.
- Flight Physics uses Newtonian inertial translation and rotation, real gravity from celestial bodies to dynamic objects, prescribed celestial/station trajectories, no artificial linear/angular speed caps, and physically valid projectile/debris motion.
- Autopilot and Flight Assist must operate through the same physical rules rather than replacing them.

### Active concept focus

Current concept work is on **Flight Assist & Autopilot**.

Flight Assist direction established in the current design session:
- rotational input release is actively stabilized to zero angular velocity;
- normal Flight Assist does not cancel gravity globally;
- a separate Position Hold / Station-Keeping function may compensate gravity if physically possible;
- one global Flight Assist switch controls the baseline assist state;
- Flight Assist preserves a gravity-evolving reference trajectory rather than a fixed global velocity vector;
- forward thrust updates the reference movement continuously;
- lateral/reverse inputs are temporary maneuver offsets and the assist returns to the prior reference trajectory after release;
- when Flight Assist is re-enabled, the current physical movement becomes the new reference;
- braking is an explicit assist command and may rotate the ship to use stronger forward thrust, then restore the prior orientation;
- direct player input always overrides assist behavior;
- Flight Assist never intentionally exceeds safe structural limits;
- Position Hold can be global or relative to a selected reference object;
- relative Position Hold follows moving targets while physically and structurally possible;
- if a reference target is lost or following becomes unsafe/impossible, the system falls back to controlled free flight and warns the player.

Autopilot direction established in the current design session:
- targets may be stations, ships, celestial bodies or free coordinates;
- moving targets are intercepted at predicted future states rather than their current position;
- gravity is part of trajectory planning;
- trajectories are continuously replanned when relevant conditions change;
- manual flight input immediately cancels Autopilot;
- impossible or unsafe maneuvers are rejected/aborted with a clear reason;
- supported route profiles include Fast, Efficient, Safe and Stealth;
- profile changes during flight trigger replanning;
- dynamic collision hazards are included in routing, with larger margins for safer profiles;
- celestial bodies are not collision obstacles and their projected visual footprint may be crossed;
- rendezvous with stations/ships ends with matched relative velocity and Relative Position Hold;
- a free-coordinate target ends at the target coordinate with global velocity reduced to zero;
- selecting a planet/celestial body means planning an arrival into its defined standard orbit;
- standard planet arrival uses a body-specific standard orbit height and a fixed prograde direction;
- after successful orbit insertion Autopilot ends and the orbit continues physically, without artificial orbit hold;
- third-body gravity may perturb the orbit later;
- direct station targets in planetary orbit are intercepted directly without requiring an intermediate standard planetary orbit;
- Efficient minimizes required thrust / delta-v and favors coasting and favorable gravity trajectories;
- Autopilot may deliberately use gravity assists; Fast uses them only when they reduce travel time, while Safe avoids aggressive close approaches;
- when a sudden collision risk appears, Autopilot may immediately fly a safe avoidance maneuver and then replan;
- if damage changes available thrust or maneuver authority, Autopilot replans using the new capability and aborts only if the target can no longer be reached safely;
- if the navigation target becomes invalid, Autopilot aborts in a controlled manner and hands the current motion state back to Flight Assist rather than continuing toward a stale position;
- incoming hostile fire does not automatically cancel Autopilot; the player decides whether to take manual control;
- Autopilot collision avoidance covers navigational hazards such as ships, asteroids and debris, but does not actively dodge weapon projectiles;
- Autopilot does not fire weapons or activate defensive modules; combat automation is owned by separate systems;
- Autopilot may remain active during combat as long as the player does not manually take over and the planned route remains viable;
- before activation, the planned route exposes at least expected travel time, selected profile, major thrust/coasting phases and known route risks so the player can make an informed choice.

### Detection / propulsion signature premise

A critical cross-cutting gameplay premise has been established and must be preserved for later Sensor/Detection, Travel and Autopilot concepts:

- **Active propulsion produces detectable signatures.** Acceleration, braking and other thrust events can reveal a ship to suitable detectors/sensors.
- Coasting without active propulsion can therefore be strategically valuable because it reduces or avoids propulsion-generated detection signatures.
- A time-optimal transfer may spend much of the journey thrusting (for example, a high-thrust accelerate-then-brake profile), making it comparatively easy to detect.
- A player may intentionally accept a much longer travel time in order to coast for most or all of a route and minimize detectability.
- This trade-off is a deliberate gameplay axis: **travel time vs. propulsion exposure / detectability**.

Stealth Autopilot profile decisions:
- Stealth primarily minimizes the duration and intensity of active propulsion signatures, even when this substantially increases travel time.
- Stealth may use long ballistic/coasting phases and only short necessary corrections.
- Stealth plans braking so that large, easily detected braking burns near the destination are avoided where possible.
- If current momentum and gravity permit a fully passive transfer to the required destination state, Stealth may choose a completely thrust-free trajectory.
- If positions/ranges of relevant detectors are known, Stealth includes them in route planning.
- Stealth may choose substantial detours when they reduce propulsion exposure within known sensor coverage.
- Stealth does **not** wait for a later, more favorable departure window; when engaged, it plans for immediate departure.
- If no truly low-exposure route exists, Stealth chooses the lowest-exposure feasible route and warns the player about the remaining detection risk.

The exact sensor equations, signature falloff, detector ranges, thermal model and detection thresholds are **not decided here** and belong to later Sensor/Detection concepts.

## Maintenance rule

Update this file whenever a concept session establishes a cross-session decision that is not yet safely captured in an approved normative concept. Keep entries concise and remove stale working notes once the authoritative concept documents make them unnecessary.
