# Autopilot

**Status:** Review  
**Version:** 0.1  
**Owner:** Concept / Game Design  
**Last Updated:** 2026-09-14

**Related Documents:**
- [Flight Physics](flight-physics.md)
- [Flight Assist](flight-assist.md)
- [Game Vision](../vision/game-vision.md)
- [Prototype Scope](../vision/prototype-scope.md)

## Table of Contents

1. [Purpose](#purpose)
2. [Design Goals](#design-goals)
3. [Scope](#scope)
4. [Out of Scope](#out-of-scope)
5. [Terminology](#terminology)
6. [Player Experience](#player-experience)
7. [Functional Design](#functional-design)
8. [Rules and Invariants](#rules-and-invariants)
9. [Parameters and Initial Values](#parameters-and-initial-values)
10. [States and Transitions](#states-and-transitions)
11. [Interactions With Other Systems](#interactions-with-other-systems)
12. [Player Feedback and Information](#player-feedback-and-information)
13. [Edge Cases](#edge-cases)
14. [Examples](#examples)
15. [Design Decisions and Rationale](#design-decisions-and-rationale)
16. [Rejected or Deferred Alternatives](#rejected-or-deferred-alternatives)
17. [Open Questions](#open-questions)
18. [Acceptance Criteria](#acceptance-criteria)
19. [Change Log](#change-log)

## Purpose

Autopilot plans and executes physically valid travel trajectories through the same simulation defined by [Flight Physics](flight-physics.md). It allows the player to select a destination and a travel profile without manually solving interception, braking, gravity or orbital insertion.

The system must preserve simulation freedom: it does not teleport, switch to simplified travel physics, suppress gravity or grant hidden movement capabilities. It predicts future target states, applies real thrust and torque, reacts to changing conditions and hands local control back to [Flight Assist](flight-assist.md) when autonomous travel ends or is aborted.

## Design Goals

- **G-AP-001:** Make large-scale travel accessible without replacing the physical simulation.
- **G-AP-002:** Plan toward future target states rather than current positions for moving destinations.
- **G-AP-003:** Incorporate gravity and ship capabilities directly into trajectory planning.
- **G-AP-004:** Support materially different travel priorities through Fast, Efficient, Safe and Stealth profiles.
- **G-AP-005:** Keep direct manual control immediately available at all times.
- **G-AP-006:** Replan intelligently when the ship, target or environment changes.
- **G-AP-007:** Distinguish navigation automation from combat automation.
- **G-AP-008:** Give the player enough route information to understand time, thrust/coasting behavior and known risks before committing.

## Scope

This concept owns:

- supported Autopilot destination types;
- prediction of moving target states;
- gravity-aware trajectory planning;
- continuous route replanning;
- travel profiles and their gameplay priorities;
- navigation collision avoidance;
- planet/celestial-body arrival into standard orbit;
- rendezvous arrival at ships and stations;
- free-coordinate arrival behavior;
- manual cancellation and controlled fallback behavior;
- route preview requirements;
- handling of damage, invalid targets and lost routes during autonomous travel.

## Out of Scope

This concept does not define:

- the physical force/gravity model, which is owned by [Flight Physics](flight-physics.md);
- local stabilization and Position Hold control mechanics, which are owned by [Flight Assist](flight-assist.md);
- exact pathfinding/optimization algorithms or numerical solvers;
- exact ship thrust, torque, mass or structural limits;
- the world-generation rules that assign celestial standard-orbit parameters;
- sensor equations, detection ranges, signature falloff or thermal modeling;
- weapon firing, defensive-module activation or combat-evasion AI;
- detailed HUD layout or map presentation.

## Terminology

| Term | Definition |
| --- | --- |
| **Trajectory** | A planned time-dependent sequence of physically valid motion and thrust actions from the current state toward a destination state. |
| **Destination state** | The position, velocity and other arrival conditions required for a destination type. |
| **Rendezvous** | Arrival near a moving ship or station with relative velocity matched and a stable relative-control state established. |
| **Standard orbit** | A body-specific navigation orbit with predefined altitude/radius and fixed prograde direction used for generic celestial-body arrival. |
| **Replanning** | Updating the active trajectory because the ship, target, hazards or selected profile changed materially. |
| **Fast profile** | Default profile that minimizes travel time while remaining within safe structural limits. |
| **Efficient profile** | Profile that minimizes required thrust / delta-v and favors coasting and favorable gravitational transfers. |
| **Safe profile** | Profile that uses larger maneuver and hazard margins and avoids aggressive close approaches. |
| **Stealth profile** | Profile that minimizes duration and intensity of propulsion-generated detectable signatures, accepting longer travel when useful. |
| **Navigation hazard** | A dynamic collidable object or region that the Autopilot should avoid during route execution. Weapon projectiles are not included in this category. |

## Player Experience

The player should be able to select a destination such as a station, another ship, a planet or a free coordinate, inspect a planned route, choose a travel profile and engage Autopilot.

From that point, the ship performs the real accelerations, coasting phases, braking burns, gravity interactions and orientation changes required by the plan. The player can watch the route evolve and may take over instantly through manual flight input.

Travel profiles create meaningful strategic choices. Fast prioritizes arrival time, Efficient minimizes propulsion work, Safe preserves larger margins, and Stealth may deliberately coast for long periods or take detours to reduce propulsion exposure to sensors.

## Functional Design

### Destination types

Autopilot supports at least:

- stations;
- ships;
- celestial bodies;
- free coordinates.

Each destination type owns a distinct arrival state rather than merely a target point.

### Moving-target prediction

Ships and stations are moving targets. Autopilot must plan toward a predicted future state at the intended intercept time rather than flying toward the target's current position.

If the target changes course or the predicted intercept changes materially, Autopilot replans continuously while the target remains valid and safely reachable.

### Gravity-aware planning

Trajectory planning includes gravity from all applicable celestial bodies according to [Flight Physics](flight-physics.md).

Gravity is not merely corrected after the fact. Autopilot may intentionally exploit gravity when doing so improves the selected profile's objective.

Celestial bodies themselves are not physical collision obstacles. Their projected visual footprints may be crossed in accordance with Flight Physics.

### Ship capability and structural safety

Every planned maneuver must respect the ship's current physical thrust/torque capability and safe structural limits.

Fast may use maximum safe performance, but no profile may intentionally command structural overload.

If propulsion damage changes the available capability during flight, Autopilot updates the plan using the new capability. It only aborts if the destination can no longer be reached safely under the active requirements.

### Route preview

Before Autopilot activation, the player must be shown at least:

- selected destination;
- selected travel profile;
- expected travel time;
- major thrust/braking/coasting phases;
- known route risks or limitations.

The preview need not expose implementation-level trajectory math, but it must make materially different profile outcomes understandable before activation.

### Continuous replanning

The active trajectory is not immutable.

Autopilot replans when relevant conditions change, including:

- target movement;
- material ship capability changes;
- new or changing navigation hazards;
- profile changes;
- route feasibility changes.

A material replan does not require confirmation, but the player is informed when expected travel time, risk or route character changes significantly.

### Manual takeover

Any direct manual flight input immediately cancels Autopilot.

Cancellation does not automatically brake or change the ship's motion. The current physical movement state is handed directly to [Flight Assist](flight-assist.md), which adopts it as the local assisted reference state where applicable.

A deliberate manual Autopilot cancel behaves the same way: immediate handoff with no hidden stop maneuver.

### Invalid or impossible route

If no valid trajectory can be found before activation, Autopilot refuses to start and communicates the reason.

If an active route becomes impossible or unsafe, Autopilot performs only the control needed for a controlled termination, hands the current motion state to Flight Assist and communicates the reason. It does not replan indefinitely when no valid route exists.

If a target becomes invalid, destroyed or unavailable, Autopilot does not continue toward stale last-known coordinates unless a separate future gameplay system explicitly requests that behavior.

### Navigation collision avoidance

Autopilot avoids known dynamic navigation hazards such as ships, interactive asteroids and debris.

When a sudden collision risk appears, Autopilot may immediately perform a safe evasive navigation maneuver and then replan toward the original destination.

Safety margins depend on the selected travel profile. Safe uses larger clearances; Fast may accept tighter but still safe clearances.

Autopilot does not treat weapon projectiles as navigation hazards and does not perform automatic combat dodging.

### Combat boundary

Being attacked does not automatically cancel Autopilot.

Autopilot may remain active during combat as long as its navigation route remains viable and the player has not manually taken control.

It does not fire weapons, choose targets or activate defensive modules. Those behaviors belong to separate combat/automation concepts.

### Arrival at ships and stations

Arrival at a ship or station is a rendezvous, not merely position matching.

Autopilot predicts the target's future state, reaches the defined rendezvous distance, matches relative velocity and then transitions to Relative Position Hold under [Flight Assist](flight-assist.md).

A station orbiting a planet is intercepted directly. Autopilot does not first require the ship to enter the planet's generic standard orbit.

### Arrival at a free coordinate

For a free-coordinate destination, Autopilot reaches the selected coordinate and reduces global inertial velocity to zero.

This is the defined arrival state for free-coordinate travel rather than a fly-through state.

### Arrival at a celestial body

Selecting a celestial body as the destination means requesting insertion into that body's standard orbit.

Each applicable celestial body provides a predefined standard-orbit height/radius through the future World/Orbit system. The standard direction is fixed and prograde.

The selected travel profile may change the transfer path and safety margins, but not the final standard-orbit definition.

After successful orbit insertion:

- the ship is physically in the required orbit;
- the ship is oriented tangentially in the direction of orbital travel;
- Autopilot ends;
- no artificial orbit-hold remains active.

The resulting orbit then evolves under normal Flight Physics. Third-body gravity may perturb it over time.

### Fast profile

Fast is the default Autopilot profile.

Its primary objective is minimum travel time while respecting safe structural limits and current ship capability.

It may spend large portions of a transfer actively accelerating and braking when that is time-optimal. A simple unconstrained direct transfer may resemble an accelerate-then-brake trajectory, although gravity, target motion and asymmetric thrust can change the split.

Fast may use gravity assists when they actually reduce travel time.

### Efficient profile

Efficient minimizes required propulsion effort / delta-v rather than travel time.

It favors:

- longer coasting phases;
- preserving useful existing momentum;
- gravitational transfers and assists that reduce required thrust;
- avoiding unnecessary course corrections.

Because normal thrust currently consumes no gameplay fuel resource, Efficient's immediate player value is the selected trajectory style itself and any cross-system consequences of reduced propulsion use. It does not become sensor-aware unless Stealth is selected.

### Safe profile

Safe increases margins rather than merely reducing speed.

It favors:

- larger clearance from dynamic hazards;
- larger reserves against structural-load limits;
- less aggressive maneuvers;
- avoidance of unnecessarily close passes by strong gravitational sources;
- avoidance of dense dynamic-object regions where a lower-risk alternative exists.

### Stealth profile

Active propulsion produces detectable signatures as a cross-system gameplay premise. Stealth therefore optimizes for propulsion exposure rather than travel time or total delta-v alone.

Stealth may:

- use long ballistic/coasting phases;
- use only short necessary correction burns;
- plan braking so that large propulsion events near the destination are reduced where possible;
- choose a fully passive trajectory when current momentum and gravity can satisfy the required destination state without further thrust;
- incorporate the known positions/ranges/risk information of relevant detectors when such information is available;
- take substantial detours when they reduce expected propulsion exposure within known sensor coverage.

Stealth does not wait for a later favorable departure window. Once activated, it plans for immediate departure from the current state.

If no genuinely low-exposure route exists, Stealth chooses the lowest-exposure feasible route and clearly warns the player about the remaining detection risk.

Exact signature generation, sensor detection and exposure scoring are owned by a future Sensor/Detection concept. Autopilot consumes that information; it does not define the sensor model itself.

### Profile changes during flight

The player may change travel profile while Autopilot is active.

A profile change immediately causes replanning from the current physical state according to the newly selected objective.

## Rules and Invariants

1. **C-AP-001:** Autopilot must move the ship only through the physical capabilities and forces defined by [Flight Physics](flight-physics.md).
2. **C-AP-002:** Autopilot supports stations, ships, celestial bodies and free coordinates as destination types.
3. **C-AP-003:** Moving destinations are planned against predicted future states rather than current positions alone.
4. **C-AP-004:** Applicable celestial gravity is included in trajectory planning.
5. **C-AP-005:** Autopilot may intentionally use gravity assists where they improve the selected profile objective.
6. **C-AP-006:** Autopilot never intentionally exceeds current safe structural limits.
7. **C-AP-007:** Any direct manual flight input immediately cancels Autopilot.
8. **C-AP-008:** Cancelling Autopilot does not automatically brake; current physical motion is handed to Flight Assist.
9. **C-AP-009:** Active trajectories are replanned when material conditions change.
10. **C-AP-010:** Material replans occur automatically, with significant changes communicated to the player.
11. **C-AP-011:** If no valid safe route exists, Autopilot refuses to start or terminates the active route with a clear reason.
12. **C-AP-012:** Sudden navigation collision risks may trigger immediate safe avoidance followed by replanning.
13. **C-AP-013:** Navigation collision avoidance includes collidable dynamic hazards but not weapon-projectile dodging.
14. **C-AP-014:** Celestial bodies are not treated as collision obstacles merely because of their projected visual footprint.
15. **C-AP-015:** Autopilot does not fire weapons or activate defensive modules.
16. **C-AP-016:** Hostile attack alone does not automatically cancel Autopilot.
17. **C-AP-017:** Damage-reduced thrust/torque capability is incorporated through replanning; Autopilot aborts only if the route becomes invalid/unsafe.
18. **C-AP-018:** Loss or invalidation of the destination causes controlled termination rather than blind continuation toward stale target data.
19. **C-AP-019:** Ship/station rendezvous ends with matched relative velocity and Relative Position Hold.
20. **C-AP-020:** Free-coordinate arrival ends at the coordinate with global inertial velocity reduced to zero.
21. **C-AP-021:** Generic celestial-body arrival always targets the body's predefined standard orbit.
22. **C-AP-022:** Standard celestial arrival uses the body's defined standard orbit height/radius and fixed prograde direction.
23. **C-AP-023:** After successful orbit insertion, Autopilot ends and the orbit continues under normal Flight Physics without artificial orbit hold.
24. **C-AP-024:** Direct station rendezvous in a planetary orbit does not require an intermediate generic planet orbit.
25. **C-AP-025:** Fast is the default travel profile and primarily minimizes travel time while remaining structurally safe.
26. **C-AP-026:** Efficient primarily minimizes required propulsion effort / delta-v and favors coasting/gravity transfers.
27. **C-AP-027:** Safe uses larger hazard, maneuver and structural margins than Fast.
28. **C-AP-028:** Stealth primarily minimizes duration/intensity of propulsion-generated detectable signatures, accepting longer travel when useful.
29. **C-AP-029:** Stealth may choose completely thrust-free travel when the required destination state is reachable passively.
30. **C-AP-030:** Stealth may incorporate known detector coverage and take detours to reduce expected propulsion exposure.
31. **C-AP-031:** Stealth does not delay departure to wait for a better future launch window; activation plans from the current time/state.
32. **C-AP-032:** If no low-exposure Stealth route exists, the lowest-exposure feasible route is used and remaining risk is communicated.
33. **C-AP-033:** The player may change profile during flight; doing so triggers immediate replanning.
34. **C-AP-034:** Before activation, the player receives route information including expected travel time, profile, major thrust/coasting phases and known risks.

## Parameters and Initial Values

This concept defines parameter ownership and semantics but not final balance values.

| Parameter | Initial value/range | Unit | Tunable | Design purpose / notes |
| --- | ---: | --- | --- | --- |
| Rendezvous distance | Destination/type specific | m | Yes | Distance at which velocity matching/Relative Position Hold becomes the arrival condition. |
| Standard orbit height/radius | Celestial-body specific | m | Yes | Supplied by future World/Orbit content. |
| Fast structural safety margin | To be defined | derived load margin | Yes | Allows maximum safe performance without overload. |
| Safe structural margin | Greater than Fast | derived load margin | Yes | Preserves additional maneuver reserve. |
| Dynamic-hazard clearance | Profile/object dependent | m | Yes | Navigation collision margin. |
| Replan materiality threshold | To be defined | system dependent | Yes | Determines when route/time/risk change must be surfaced to the player. |
| Stealth exposure metric | Supplied by Sensor/Detection | architecture/concept defined | Yes | Quantifies propulsion-detection risk for route comparison. |

## States and Transitions

| From | Trigger / Condition | To | Player-visible result |
| --- | --- | --- | --- |
| Inactive | Destination/profile selected and valid route activated | Active | Ship begins executing planned physical trajectory. |
| Active | Material route condition changes | Replanning | Updated route is calculated automatically. |
| Replanning | Valid route found | Active | New route continues; material changes are reported. |
| Replanning | No valid safe route exists | Terminating | Autopilot stops autonomous travel and explains reason. |
| Active | Player changes profile | Replanning | Route recalculated from current state under new objective. |
| Active | Direct manual flight input | Cancelled/Handoff | Autopilot ends immediately; current motion handed to Flight Assist. |
| Active | Target invalid/lost | Terminating | Controlled handoff to Flight Assist; no stale-target pursuit. |
| Active | Ship/station rendezvous completed | Complete | Relative Position Hold becomes active. |
| Active | Free-coordinate destination completed | Complete | Ship is at target coordinate with global zero velocity. |
| Active | Standard orbit insertion completed | Complete | Autopilot ends; ship continues on physical prograde orbit. |

## Interactions With Other Systems

- [Flight Physics](flight-physics.md) — owns the authoritative physical simulation, gravity, thrust, inertia, collisions and structural loading used by all routes.
- [Flight Assist](flight-assist.md) — owns local stabilization, braking and Position Hold; receives control after cancellation/termination and owns Relative Position Hold after rendezvous.
- World/Orbit concept (future) — supplies prescribed celestial/station motion and body-specific standard-orbit data.
- Ships/Modules concept (future) — supplies current mass, thrust, torque and damage-reduced capability.
- Damage/Structure concept (future) — supplies current safe structural limits.
- Sensor/Detection concept (future) — owns propulsion signature generation, detector coverage and the risk/exposure information consumed by Stealth.
- HUD/Navigation concept (future) — owns route-preview presentation, warnings and detailed map interaction.
- Combat automation concepts (future) — own weapon/defense automation and projectile-evasion behavior; Autopilot deliberately does not own them.

## Player Feedback and Information

Before activation, the player must be able to see at least the selected profile, estimated travel time, major powered/coasting phases and known route risks.

During travel, the player must be informed of at least:

- active destination and profile;
- current phase of the route;
- meaningful route replans;
- materially changed arrival time or risk;
- collision-avoidance deviations;
- ship damage/capability changes that alter the route;
- remaining Stealth detection risk when relevant;
- inability to continue safely and the reason for termination;
- successful transition to rendezvous hold, free-coordinate stop or physical standard orbit.

## Edge Cases

### Moving target accelerates sharply

Autopilot recomputes the future intercept and continues if a safe route remains available. If it no longer does, Autopilot terminates and hands control to Flight Assist.

### Navigation hazard appears during a burn

Autopilot may interrupt the nominal trajectory with an immediate safe navigation-avoidance maneuver and then replan. The selected destination remains unchanged unless the route becomes impossible.

### Incoming hostile fire

Autopilot continues unless navigation becomes unsafe or the player takes manual control. It does not dodge individual weapon projectiles or operate weapons/defenses.

### Engine damage during travel

The active plan is recalculated using the reduced physical capability. Travel may become slower or less direct. Autopilot terminates only if the destination state cannot be reached safely.

### Planet approach through projected body image

The route may cross the visible footprint of a celestial body because that footprint is not collision geometry under Flight Physics. Gravity remains active and is included in the trajectory.

### Orbit perturbed after arrival

After standard orbit insertion, Autopilot is no longer active. Third-body gravity may alter the orbit later; the player may request a new Autopilot approach if they want the standard orbit restored.

### Stealth cannot avoid known sensor exposure

Autopilot selects the lowest-exposure feasible immediate-departure route and warns the player. It does not wait for a later launch window.

## Examples

### Fast transfer

A distant stationary destination can produce a trajectory with heavy acceleration early and heavy braking later. The exact split need not be 50/50 because gravity, asymmetric thrust and destination motion can change the time-optimal solution. The important property is that Fast is willing to use prolonged powered flight if that minimizes arrival time.

### Efficient transfer

Instead of maximizing thrust, the route preserves existing velocity, coasts for a long interval and uses a favorable gravity assist before a smaller arrival burn. The trip is slower but requires less total propulsion effort/delta-v.

### Stealth transfer

A ship chooses Stealth while known detectors cover the direct path. Autopilot selects a longer path with an early correction burn, a long passive coast outside the highest-risk coverage and a low-exposure braking plan. If current momentum permits a fully passive solution, no further propulsion is required.

### Planet destination

The player selects a planet. Autopilot predicts the body's future position, flies a gravity-aware transfer and inserts the ship into the planet's predefined prograde standard orbit. Once insertion is complete, Autopilot disengages and the ship remains in orbit only because of its physical state and gravity.

### Station destination around a planet

The player selects the station rather than the planet. Autopilot predicts the station's future orbital position and performs a direct rendezvous, matching relative velocity and ending in Relative Position Hold without first entering the generic standard planetary orbit.

## Design Decisions and Rationale

| ID | Decision | Rationale | Consequences |
| --- | --- | --- | --- |
| D-AP-001 | Use the same physical simulation for autonomous and manual travel. | Preserves simulation coherence and prevents hidden travel physics. | Route planning must account for real thrust, gravity and current motion. |
| D-AP-002 | Plan to predicted future states for moving targets. | Current-position pursuit is inadequate for orbital/moving destinations. | Target prediction is fundamental to rendezvous. |
| D-AP-003 | Include gravity directly in route planning and allow gravity assists. | Gravity is part of the authoritative simulation and should create useful travel opportunities. | Different profiles may exploit gravity differently. |
| D-AP-004 | Make Fast the default profile. | The normal expectation when selecting Autopilot is prompt arrival unless the player chooses another strategic priority. | Other profiles become deliberate alternatives. |
| D-AP-005 | Separate four travel objectives: Fast, Efficient, Safe and Stealth. | Travel can create meaningful choices beyond a single optimal route. | Route previews must explain profile consequences. |
| D-AP-006 | Make planet arrival mean real standard-orbit insertion. | Hides orbital-mechanics burden without faking the resulting orbit. | Planet destinations have a clear physically meaningful end state. |
| D-AP-007 | End standard-orbit Autopilot after insertion. | Ensures the orbit remains an emergent physical state rather than perpetual hidden assistance. | Later perturbations are allowed. |
| D-AP-008 | End ship/station rendezvous with Relative Position Hold. | Provides a stable usable arrival state for moving local targets. | Flight Assist owns post-arrival station keeping. |
| D-AP-009 | Let manual input cancel immediately without automatic braking. | Preserves direct control and physical continuity. | The player inherits the exact current motion state. |
| D-AP-010 | Treat collision avoidance as navigation, not combat evasion. | Prevents Autopilot from becoming an autonomous combat pilot. | Weapon-projectile dodging remains separate. |
| D-AP-011 | Let Stealth optimize propulsion exposure using sensor information supplied by another system. | Creates a time-versus-detectability travel axis without duplicating sensor rules. | Full Stealth implementation depends on a Sensor/Detection contract. |
| D-AP-012 | Stealth departs immediately rather than waiting for a better launch window. | Keeps Autopilot activation responsive and predictable. | The lowest-exposure route is optimized from the current state/time only. |

## Rejected or Deferred Alternatives

| Alternative | Status | Reason |
| --- | --- | --- |
| Separate simplified cruise/travel physics | Rejected | Conflicts with the approved physically grounded movement model. |
| Fly toward a moving target's current position | Rejected | Does not produce reliable rendezvous for moving/orbital targets. |
| Require planet standard orbit before every station rendezvous | Rejected | Creates unnecessary detours when the station can be intercepted directly. |
| Keep an artificial orbit-hold active after planet arrival | Rejected | The intended result is a real physical orbit. |
| Free-coordinate fly-through as the default | Rejected | The selected behavior is arrival with global zero velocity. |
| Autopilot waits for a future low-signature launch window in Stealth | Rejected | Stealth plans for immediate departure once activated. |
| Automatic weapon/projectile evasion | Rejected for Autopilot scope | This is combat automation rather than navigation. |
| Automatic weapon or defensive-module use | Rejected for Autopilot scope | Owned by future combat/automation systems. |
| Automatically cancel Autopilot merely because hostile fire is detected | Rejected | Player retains the decision to take manual control. |
| Mandatory confirmation for every material route replan | Rejected | Would make continuous autonomous navigation cumbersome; significant changes are communicated instead. |

## Open Questions

No implementation-blocking gameplay questions remain for the core Fast/Safe/Efficient navigation rules defined here.

Two external contracts remain intentionally owned by future concepts:

- the World/Orbit concept must provide each celestial body's standard-orbit parameters;
- the Sensor/Detection concept must define propulsion signatures and the detection/exposure information needed to evaluate Stealth routes.

Until those concepts exist, their dependent Autopilot behavior is conceptually specified but cannot be fully parameterized.

## Acceptance Criteria

- [ ] Autopilot reaches destinations using only forces and capabilities permitted by Flight Physics.
- [ ] Moving stations/ships are intercepted based on predicted future states rather than current position alone.
- [ ] Gravity affects route planning and may be deliberately exploited by suitable profiles.
- [ ] Fast is the default profile and seeks the shortest safe travel time.
- [ ] Efficient favors lower total propulsion effort/delta-v and longer coasting/gravity transfers when appropriate.
- [ ] Safe uses larger structural/hazard margins and avoids unnecessarily aggressive close approaches.
- [ ] Stealth can prefer long coasting phases, detector-aware detours and fully passive trajectories to reduce propulsion exposure.
- [ ] Stealth begins from the current time/state and does not wait for a later departure window.
- [ ] Route preview communicates expected time, profile, major thrust/coasting phases and known risks before activation.
- [ ] Material route changes trigger automatic replanning and meaningful changes are communicated.
- [ ] Manual flight input cancels Autopilot immediately without automatic braking.
- [ ] Sudden dynamic collision hazards can trigger safe avoidance followed by replanning.
- [ ] Autopilot does not automatically dodge weapon projectiles or operate weapons/defensive modules.
- [ ] Hostile attack alone does not cancel Autopilot.
- [ ] Damage-reduced control authority is incorporated into replanning.
- [ ] Invalid/lost destinations cause controlled termination rather than pursuit of stale coordinates.
- [ ] Ship/station arrival matches relative velocity and transitions to Relative Position Hold.
- [ ] Free-coordinate arrival ends at the selected coordinate with global zero velocity.
- [ ] Generic celestial-body arrival inserts the ship into the body's predefined fixed-prograde standard orbit.
- [ ] After orbit insertion, Autopilot disengages and no artificial orbit hold maintains the orbit.
- [ ] Direct station rendezvous in a planetary orbit does not require prior insertion into the planet's standard orbit.
- [ ] If no valid safe route remains, Autopilot terminates and hands the current physical state to Flight Assist with a clear reason.

## Change Log

| Version | Date | Change |
| --- | --- | --- |
| 0.1 | 2026-09-14 | Initial Autopilot concept produced from structured design session and consistency review. |
