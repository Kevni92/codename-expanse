# Flight Assist

**Status:** Review  
**Version:** 0.1  
**Owner:** Concept / Game Design  
**Last Updated:** 2026-09-14

**Related Documents:**
- [Flight Physics](flight-physics.md)
- [Autopilot](autopilot.md)
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

Flight Assist makes the inertial movement defined by [Flight Physics](flight-physics.md) practical for direct manual control without replacing or weakening the authoritative physical simulation.

It converts immediate player intent into physically valid thrust and torque commands, stabilizes rotation, manages temporary maneuvering drift, provides explicit braking, and offers Position Hold for station keeping. It does not plan long-range routes or autonomous multi-stage journeys; those belong to [Autopilot](autopilot.md).

## Design Goals

- **G-FA-001:** Preserve the physical truth of Flight Physics while making normal manual flight predictable and comfortable.
- **G-FA-002:** Keep direct player input authoritative over automated corrections.
- **G-FA-003:** Avoid silently cancelling gravity during ordinary assisted flight.
- **G-FA-004:** Allow intentional inertial drift and arbitrary facing relative to travel direction.
- **G-FA-005:** Provide explicit, understandable tools for braking and station keeping.
- **G-FA-006:** Never intentionally damage the ship by exceeding safe structural limits.
- **G-FA-007:** Keep Flight Assist reactive and local; route and trajectory planning belong to Autopilot.

## Scope

This concept owns:

- baseline Flight Assist on/off behaviour;
- rotational stabilization and orientation holding;
- the assisted reference trajectory used during manual flight;
- treatment of forward, reverse and lateral manual thrust while Flight Assist is enabled;
- explicit assisted braking;
- Position Hold and Relative Position Hold;
- player-input priority over assist actions;
- safe fallback behaviour when control authority or references are lost.

## Out of Scope

This concept does not define:

- the underlying force, gravity, inertia or structural-load model, which is owned by [Flight Physics](flight-physics.md);
- long-range route planning, gravity-assist planning, target interception or orbit insertion, which are owned by [Autopilot](autopilot.md);
- exact control-loop algorithms or numerical gains;
- input bindings or detailed HUD layout;
- ship-specific thrust, torque, mass or structural values;
- damage rules that determine how propulsion capability is degraded.

## Terminology

| Term | Definition |
| --- | --- |
| **Flight Assist** | Reactive control assistance that converts immediate player intent into physically valid thrust and torque while preserving the Flight Physics model. |
| **Reference trajectory** | The gravity-evolving free-motion trajectory the assist treats as the ship's intended baseline movement when no temporary maneuver offset is active. |
| **Temporary maneuver offset** | A reverse or lateral manual maneuver that temporarily departs from the reference trajectory and is corrected after release. |
| **Brake command** | An explicit immediate command to reduce velocity relative to the applicable reference frame using available safe thrust. |
| **Position Hold** | A mode that attempts to maintain a fixed position in the global inertial frame. |
| **Relative Position Hold** | A mode that attempts to maintain the current relative position vector to a selected reference object. |
| **Safe control authority** | The thrust and torque that can be used without intentionally exceeding current structural limits. |

## Player Experience

With Flight Assist enabled, the ship should remain recognizably inertial rather than feeling as if it were moving through air. Forward acceleration establishes movement that persists. Rotating the ship does not automatically rotate the velocity vector, so the player may fly sideways or backward relative to the hull.

The assist removes unnecessary control burden rather than removing physics. Releasing rotational input stops unwanted spin. Temporary reverse or lateral maneuvers can be used for fine control and are cleaned up after release. Gravity remains physically active during ordinary assisted flight.

When the player explicitly wants to stop or remain in place, dedicated braking and Position Hold functions provide that intent without changing the underlying physical rules.

## Functional Design

### Baseline Flight Assist

Flight Assist has one baseline global on/off state.

When disabled, no Flight Assist stabilization or correction is applied. The ship follows [Flight Physics](flight-physics.md) directly from manual thrust/torque input and external forces.

When re-enabled, the ship's current physical movement becomes the starting basis for a new assisted reference trajectory. The assist must not attempt to restore a pre-disable velocity state.

### Gravity-aware reference trajectory

The baseline assist does not attempt to hold a fixed global velocity vector. Doing so would implicitly cancel gravity.

Instead, it preserves a reference trajectory representing how the ship should continue to move under the currently applicable external forces when the player is no longer requesting a temporary correction. Gravity therefore continues to curve or accelerate the reference movement naturally.

### Rotation and orientation stabilization

When rotational input is released, Flight Assist applies safe counter-torque to reduce angular velocity to zero.

Once stabilized, it actively maintains the resulting orientation against correctable rotational disturbances. Orientation holding does not align the hull with the velocity vector.

The ship may therefore maintain a facing direction unrelated to its direction of travel.

### Forward thrust

While forward thrust is commanded, the reference trajectory is continuously changed in the ship's current facing direction using physically available thrust.

Releasing forward thrust does not command a return to the pre-thrust movement. The new movement becomes part of the intended reference trajectory.

### Reverse and lateral maneuvering

Reverse and lateral manual thrust are treated as temporary maneuver offsets while baseline Flight Assist is enabled.

When such input is released, Flight Assist attempts to return the ship to the prior reference trajectory using available safe thrust. Rotation of the ship during this process does not redefine the reference trajectory merely because the hull has turned.

If returning to the reference trajectory is no longer physically possible with current control authority, the assist performs the best safe correction available and informs the player.

### Brake command

Braking is an explicit assist command, not merely raw reverse thrust.

Without an applicable reference object, the brake command attempts to reduce global inertial velocity to zero.

When braking relative to an applicable selected navigation/reference object, the brake command attempts to reduce relative velocity to zero with respect to that object.

The assist may temporarily rotate the ship to use stronger forward thrust for braking. After the braking maneuver, it restores the orientation that was held before the automatic braking rotation, unless direct player input has superseded that orientation.

Braking does not itself activate Position Hold. After the brake command is complete, gravity and other external forces continue to affect the ship normally unless a hold mode is active.

### Position Hold

Position Hold is separate from ordinary Flight Assist.

Global Position Hold attempts to maintain a fixed position in the global inertial reference frame. It may therefore counteract gravity using real thrust.

Relative Position Hold attempts to preserve the current relative position vector to a selected reference object. If that reference object moves, the ship follows as required to preserve the relative offset.

Position Hold may only use physically available thrust and torque within safe structural limits. If external acceleration or target motion exceeds that authority, the hold remains in a best-effort state and warns the player rather than intentionally overloading the ship.

### Manual input during Position Hold

Direct manual input always has priority.

While Position Hold is active, manual movement input shifts the held position. After the player releases the input, the resulting position or relative offset becomes the new held state rather than disabling Position Hold entirely.

### Reference loss

If the object used by Relative Position Hold is lost, destroyed or otherwise becomes invalid, the assist must not continue chasing a stale state.

The ship transitions to controlled free assisted flight using its current physical motion as the new reference and informs the player that the relative reference was lost.

If the reference remains valid but becomes impossible or unsafe to follow, the same controlled fallback applies.

### Structural safety

Flight Assist must never intentionally exceed the ship's current safe structural limits.

This applies to rotational stabilization, braking, reference-trajectory correction and Position Hold.

External forces or impacts may still overload the ship; the assist is not required to prevent damage that it cannot physically avoid.

### Damaged propulsion

Flight Assist consumes the ship's current available thrust and torque capabilities.

If damage reduces control authority, the assist continues to operate on a best-effort basis. It does not automatically disable merely because perfect correction is impossible. The player must be informed when a requested assisted state cannot be maintained.

### Boundary to Autopilot

Flight Assist reacts to immediate player intent and local control states. It does not plan general multi-stage trajectories to remote destinations.

Automatic rotation as part of one explicit brake command remains Flight Assist behaviour because it is a bounded local control action. Long-range interception, route optimization, orbit insertion and autonomous travel belong to [Autopilot](autopilot.md).

## Rules and Invariants

1. **C-FA-001:** Flight Assist may only influence movement through physically valid thrust and torque under [Flight Physics](flight-physics.md).
2. **C-FA-002:** Direct manual player input has priority over all Flight Assist corrections.
3. **C-FA-003:** Baseline Flight Assist has a single global enabled/disabled state.
4. **C-FA-004:** Re-enabling Flight Assist adopts the ship's current physical motion as the new assisted reference state.
5. **C-FA-005:** Baseline Flight Assist does not cancel gravity merely to preserve a fixed global velocity.
6. **C-FA-006:** The assisted reference trajectory evolves under external forces including gravity.
7. **C-FA-007:** Releasing rotational input causes safe counter-torque toward zero angular velocity.
8. **C-FA-008:** Once angular velocity is stabilized, Flight Assist maintains the resulting orientation against correctable disturbances.
9. **C-FA-009:** Hull orientation and movement direction remain independent; Flight Assist does not automatically align them.
10. **C-FA-010:** Forward thrust permanently changes the assisted reference trajectory while the command is applied.
11. **C-FA-011:** Reverse and lateral manual thrust are temporary offsets and are corrected back toward the prior reference trajectory after release.
12. **C-FA-012:** An explicit brake command attempts zero global velocity when no relative reference applies.
13. **C-FA-013:** When an applicable reference object is used for braking, the brake command attempts zero relative velocity to that object.
14. **C-FA-014:** Brake Assist may rotate the ship to use stronger forward thrust and restores the prior held orientation afterward unless superseded by player input.
15. **C-FA-015:** Global Position Hold may counteract gravity to preserve global position.
16. **C-FA-016:** Relative Position Hold preserves the current relative position vector to its reference object while physically possible.
17. **C-FA-017:** Manual movement during Position Hold moves the held state rather than automatically disabling the hold.
18. **C-FA-018:** Flight Assist never intentionally commands structural overload.
19. **C-FA-019:** If safe control authority is insufficient, Flight Assist uses best-effort safe correction and informs the player.
20. **C-FA-020:** Loss or unsafe pursuit of a Relative Position Hold reference causes controlled fallback to free assisted flight using the current physical motion.
21. **C-FA-021:** Flight Assist does not perform general long-range route planning or autonomous destination travel.

## Parameters and Initial Values

Exact control gains and tolerances are technical/balance parameters and are not fixed here. The concept requires the following parameter categories:

| Parameter | Initial value/range | Unit | Tunable | Design purpose / notes |
| --- | ---: | --- | --- | --- |
| Rotational stabilization tolerance | To be defined | rad/s | Yes | Determines when rotation is considered stabilized. |
| Orientation-hold tolerance | To be defined | rad | Yes | Permitted orientation error during hold. |
| Reference-trajectory correction tolerance | To be defined | m/s and/or m | Yes | Determines when temporary maneuver correction is complete. |
| Position-Hold tolerance | To be defined | m | Yes | Permitted hold-position error. |
| Relative Position-Hold tolerance | To be defined | m | Yes | Permitted relative-position error. |
| Safe control margin | Ship/system dependent | derived load margin | Yes | Keeps automatic control below structural limits. |

## States and Transitions

| From | Trigger / Condition | To | Player-visible result |
| --- | --- | --- | --- |
| Flight Assist Off | Player enables Flight Assist | Flight Assist On | Current motion becomes new assisted reference. |
| Flight Assist On | Player disables Flight Assist | Flight Assist Off | Automatic stabilization/correction stops immediately. |
| Flight Assist On | Position Hold activated | Position Hold | Current global or relative position becomes held state. |
| Position Hold | Player moves ship manually | Position Hold | Held state shifts to the new resulting position/offset. |
| Position Hold | Hold disabled | Flight Assist On | Current motion becomes normal assisted reference. |
| Relative Position Hold | Reference lost/invalid or unsafe to follow | Flight Assist On | Controlled fallback; current motion adopted; warning shown. |
| Any assisted state | Direct manual input | Same relevant state | Manual input immediately overrides competing assist correction. |

## Interactions With Other Systems

- [Flight Physics](flight-physics.md) — owns inertia, thrust, torque, gravity, structural loads and the global inertial frame. Flight Assist must not redefine these rules.
- [Autopilot](autopilot.md) — owns autonomous trajectory planning and hands local movement/control states to Flight Assist when appropriate.
- Ships/Modules concept (future) — supplies available thrust, torque and damage-reduced control authority.
- Damage/Structure concept (future) — defines structural safety limits and damage consequences.
- HUD/Controls concept (future) — owns input bindings and detailed visualization of assist states.

## Player Feedback and Information

The player must be able to determine at least:

- whether baseline Flight Assist is enabled;
- whether Position Hold or Relative Position Hold is active;
- the active reference object for relative operations;
- when braking is in progress;
- when the assist temporarily rotates the ship for braking;
- when available thrust/torque is insufficient to maintain the requested assisted state;
- when a reference object has been lost or a relative hold has fallen back to free flight;
- when structural safety limits constrain the requested assist action.

## Edge Cases

### Braking near a planet

Braking to zero relative velocity to a planet does not create an orbit or permanent hover by itself. Once braking ends, gravity continues to affect the ship unless Position Hold or another appropriate system is active.

### Gravity changes during a temporary maneuver

The reference trajectory continues to evolve under gravity while the ship performs a temporary lateral/reverse maneuver. Returning to the reference trajectory therefore means returning toward the gravity-evolved reference, not toward a stale velocity captured before the maneuver.

### Damaged lateral or reverse thrusters

The assist may need more time or may be unable to remove temporary drift. It must use safe available control authority and report the limitation rather than inventing force.

### Brake rotation interrupted by player

Manual player input immediately supersedes the automatic braking orientation sequence. The assist must not fight the player's new orientation command.

### Position Hold in excessive gravity

If available safe thrust cannot counter the local gravitational acceleration, Position Hold remains best effort and clearly reports that the position cannot be maintained.

## Examples

### Inertial drift while facing elsewhere

The player accelerates east, releases forward thrust, then rotates the ship north. The ship continues following its eastward gravity-influenced trajectory while holding the new north-facing orientation.

### Temporary strafe

The player applies lateral thrust to dodge, then releases it. Flight Assist uses available safe thrust to return toward the pre-strafe reference trajectory rather than keeping the new lateral drift permanently.

### Assisted braking

The player commands a stop. The assist may rotate the ship so the main engine opposes the current velocity, brake using safe thrust, and then restore the previously held facing direction.

### Relative station keeping

The player activates Relative Position Hold next to a moving ship. The assist attempts to preserve the current relative offset. If the target accelerates beyond what can be followed safely, the assist falls back to free assisted flight and warns the player.

## Design Decisions and Rationale

| ID | Decision | Rationale | Consequences |
| --- | --- | --- | --- |
| D-FA-001 | Preserve a gravity-evolving reference trajectory rather than a fixed global velocity. | Prevents ordinary Flight Assist from silently cancelling gravity. | Natural orbits/free-fall remain possible with assist enabled. |
| D-FA-002 | Treat forward thrust as persistent intent but reverse/lateral thrust as temporary maneuver offsets. | Keeps normal acceleration intuitive while automatically cleaning up fine-control drift. | Different thrust directions intentionally have different assisted semantics. |
| D-FA-003 | Keep facing independent from travel direction. | Preserves inertial-space combat and drift behaviour. | Players may fly sideways/backward while maintaining another facing. |
| D-FA-004 | Give braking its own command and permit automatic braking rotation. | Allows the assist to use the strongest available propulsion without requiring manual flip-and-burn control. | Brake Assist performs a bounded automatic orientation sequence. |
| D-FA-005 | Keep Position Hold separate from baseline Flight Assist. | Prevents gravity cancellation from becoming an always-on hidden rule. | Holding position is explicit player intent. |
| D-FA-006 | Make player input always authoritative. | Avoids control conflict and preserves immediate manual takeover. | Automated corrections yield instantly. |
| D-FA-007 | Never intentionally exceed structural safety limits. | Assistance should reduce control burden, not autonomously damage the ship. | Some requested holds/corrections can fail gracefully. |
| D-FA-008 | Keep general route planning outside Flight Assist. | Preserves a clean boundary between local control and autonomous navigation. | Long-distance movement belongs to Autopilot. |

## Rejected or Deferred Alternatives

| Alternative | Status | Reason |
| --- | --- | --- |
| Fixed global target velocity for baseline Flight Assist | Rejected | Would automatically counter gravity and undermine physical orbital behaviour. |
| Automatically align hull facing with velocity | Rejected | Would remove intentional drift/facing independence. |
| Make all thrust inputs permanently alter the assisted velocity | Rejected | Would preserve unwanted lateral/reverse drift rather than providing comfortable local maneuver control. |
| Restore the pre-disable assisted velocity when Flight Assist is re-enabled | Rejected | Could cause violent unexpected correction after free inertial flight. |
| Let Flight Assist complete corrections before accepting manual input | Rejected | Conflicts with direct player authority. |
| Allow assist systems to exceed structural limits for stronger correction | Rejected | Automatic systems must not intentionally damage the ship. |
| Make Position Hold the default behavior of ordinary Flight Assist | Rejected | Would implicitly cancel gravity and remove free physical motion. |

## Open Questions

No implementation-blocking gameplay questions remain for the defined Flight Assist behaviour.

Exact control tolerances and algorithms belong to technical architecture/balance work, provided they preserve the observable rules above.

## Acceptance Criteria

- [ ] Disabling Flight Assist leaves movement fully governed by Flight Physics and manual input.
- [ ] Re-enabling Flight Assist adopts current motion rather than restoring an old velocity target.
- [ ] Ordinary Flight Assist does not automatically cancel gravity.
- [ ] Releasing rotational input safely reduces angular velocity toward zero and then holds the resulting orientation.
- [ ] Rotating the hull does not automatically redirect the ship's velocity.
- [ ] Forward thrust permanently changes the reference trajectory while applied.
- [ ] Released lateral/reverse maneuvering input triggers safe correction toward the gravity-evolved prior reference trajectory.
- [ ] Braking without a relative reference attempts global zero velocity.
- [ ] Relative braking attempts zero relative velocity to the applicable reference object.
- [ ] Brake Assist may rotate to use stronger forward thrust and restore the prior held orientation afterward.
- [ ] Position Hold can intentionally counter gravity using real thrust.
- [ ] Relative Position Hold preserves a relative offset while physically and structurally possible.
- [ ] Manual movement while holding position moves the held state rather than necessarily cancelling the hold.
- [ ] Direct player input immediately overrides competing Flight Assist actions.
- [ ] Flight Assist never intentionally commands structural overload.
- [ ] Insufficient/damaged control authority produces best-effort behaviour plus clear player feedback.
- [ ] Losing a relative reference causes controlled fallback to free assisted flight rather than pursuit of stale data.
- [ ] Flight Assist does not perform long-range route planning.

## Change Log

| Version | Date | Change |
| --- | --- | --- |
| 0.1 | 2026-09-14 | Initial Flight Assist concept produced from structured design session and consistency review. |
