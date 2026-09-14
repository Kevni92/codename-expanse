# Celestial Bodies & Orbits

**Status:** Draft  
**Version:** 0.1  
**Owner:** Concept / Game Design  
**Last Updated:** 2026-09-14

**Related Documents:**
- [Flight Physics](flight-physics.md)
- [Autopilot](autopilot.md)
- [Playable Star System](../features/playable-star-system.md)
- [Autopilot Travel](../features/autopilot-travel.md)
- [M01 – Flight Sandbox](../milestones/m01-flight-sandbox.md)

> **Concept ownership rule:** This document defines the intended final-game behaviour of celestial bodies and their prescribed orbital relationships. Milestones may deliver only a subset of body types or authored content, but must not redefine this model.

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

Celestial Bodies & Orbits defines the authoritative gameplay model for stars, planets and moons inside a star system. It defines how bodies are classified, what stable physical/environmental attributes they expose, how prescribed hierarchical orbits are represented, how a body's deterministic position changes with simulation time, and what orbital destination context navigation and Autopilot can consume.

The system is designed so authored star systems and future procedurally generated star systems use the same body model. A future generator will decide which valid bodies are created from a system seed; this Concept defines what a valid generated body must ultimately describe.

Celestial bodies are world-scale prescribed objects. They are not dynamically accelerated by gravity. Dynamic objects such as ships and interactive asteroids may nevertheless react to their current gravitational fields according to [Flight Physics](flight-physics.md).

## Design Goals

- **G-CBO-001:** Provide one coherent data model for authored and procedurally generated celestial bodies.
- **G-CBO-002:** Keep celestial motion deterministic and stable without N-body simulation.
- **G-CBO-003:** Support nested orbital hierarchies including moons and multi-star systems.
- **G-CBO-004:** Expose enough physical and environmental identity for later navigation, station, economy, population and rendering systems without prematurely defining those systems.
- **G-CBO-005:** Keep astronomical modelling simplified where additional realism does not create meaningful gameplay value.
- **G-CBO-006:** Allow planets and moons to differ substantially in size, composition, atmosphere and habitability without requiring separate simulation models.
- **G-CBO-007:** Support readable large-scale 2D presentation while preserving the body's authoritative simulated position.
- **G-CBO-008:** Give every navigable celestial body a well-defined orbital arrival context compatible with [Autopilot](autopilot.md).

## Scope

This Concept owns:

- celestial-body terminology and classification;
- the distinction between orbital role, size class and composition class;
- star identity relevant to star-system simulation;
- physical attributes required by gameplay such as mass and radius;
- prescribed hierarchical orbital relationships;
- elliptic/circular, prograde/retrograde celestial orbits;
- deterministic celestial position/state as a function of system time;
- non-physical barycenters used as orbit anchors in multi-star systems;
- simplified planetary/moon environmental attributes including atmospheric pressure, atmosphere compatibility, mean/reference surface temperature, surface class and human habitability;
- star luminosity/radiative contribution as environmental world data;
- body-specific standard-orbit definitions consumed by navigation and Autopilot;
- design requirements for the visual representation of celestial bodies as large deep-layer objects tied to their real relative direction and distance.

## Out of Scope

This Concept does not define:

- procedural star-system generation probabilities, seed algorithms or content-distribution rules;
- the galaxy map or travel/jump rules between star systems;
- exact atmospheric gas composition;
- detailed mineral/resource inventories;
- economic production, consumption, markets or planetary industry;
- population growth, migration or colony simulation;
- station construction rules beyond exposing bodies/orbits as possible anchors;
- ship thermal capacity, cooling, heat ejectors or heat damage;
- sensor equations, thermal signature detection or stealth scoring;
- ship motion, gravity equations or dynamic asteroid motion, which are owned by [Flight Physics](flight-physics.md);
- Autopilot planning or insertion control, which is owned by [Autopilot](autopilot.md);
- technical rendering algorithms, camera implementation or parallax mathematics;
- technical data schemas or generation algorithms.

## Terminology

| Term | Definition |
| --- | --- |
| **Celestial body** | A world-scale star, planet or moon represented as a prescribed object. |
| **Orbital role** | The body's role in the orbital hierarchy: Star, Planet or Moon. This is separate from physical size/composition. |
| **Planet** | A non-stellar celestial body orbiting a star or stellar-system barycenter. |
| **Moon** | A non-stellar celestial body orbiting a planet. |
| **Size class** | A simplified physical scale category such as Dwarf, Earth-scale, Super-Earth, Neptunian or Giant. |
| **Composition class** | A simplified bulk-material category such as Rocky, Icy, Mixed, Volatile-rich or Gas-dominated. |
| **Surface class** | The dominant player-relevant surface character, separate from bulk composition; candidate values include Rocky, Icy, Oceanic, Mixed, Molten and None. |
| **Prescribed orbit** | A deterministic authored/generated orbit that is not altered by gravitational forces during simulation. |
| **Orbit parent** | The body or barycenter relative to which a prescribed orbit is defined. |
| **Barycenter** | A non-physical orbital reference point used to anchor hierarchical multi-star motion. It is not a celestial body, does not generate gravity and is not a normal navigation destination. |
| **Prograde orbit** | Orbit whose direction follows the system/body's defined positive orbital direction. |
| **Retrograde orbit** | Orbit whose direction runs opposite the defined positive orbital direction. |
| **Reference surface temperature** | Stable mean/representative thermal classification value for a body rather than a continuously simulated climate temperature. |
| **Surface pressure** | Numeric atmospheric pressure at the body's reference surface, used to derive an atmosphere-density class where a meaningful surface exists. |
| **Atmosphere compatibility** | Simplified classification of whether the atmosphere is directly compatible with unprotected humans. Exact chemistry is defined elsewhere/later. |
| **Human habitability** | Derived world-environment classification describing whether humans can broadly inhabit the environment without fully closed artificial habitats. |
| **Standard orbit** | Body-specific predefined orbital destination used for generic celestial-body Autopilot arrival. |
| **Orbital anchor** | A celestial body whose orbital environment can be referenced by other gameplay systems such as stations. |

## Player Experience

Star systems should feel like moving astronomical environments rather than static maps. Planets and moons continuously change position along stable, predictable orbits. The player can therefore watch, navigate toward and physically orbit destinations that are themselves moving through the star system.

Celestial bodies should communicate enormous scale without requiring literal astronomical visual scale. From far away a body appears small and enters the screen from the correct relative direction. As the player's ship approaches, the body's rendered representation grows continuously. This visual size is intentionally stylized for readability while remaining monotonic with distance: approaching a body never makes it appear smaller solely because of the distance representation.

Non-luminous bodies are visually lit from their stellar environment. A simple light/dark division should communicate a star-facing and star-opposed side. In systems with multiple stars, combined stellar radiation affects environment calculations while the strongest current lighting contribution is the primary visual light direction unless a later presentation concept specifies a richer multi-light treatment.

When the player's ship physically enters and maintains an orbit, the body's relative position changes around the followed ship/camera. The presentation should therefore create the visual impression that the body moves around the camera as the ship travels around it, without replacing the authoritative physical/orbital state with a camera-only illusion.

## Functional Design

### Celestial-body identity

Every celestial body has an orbital role, a size class and a composition class. These axes are independent.

Orbital role describes hierarchy rather than material nature. A Moon may therefore be rocky, icy or mixed and may possess no atmosphere, a thin atmosphere or a dense atmosphere. A Planet may likewise occupy different physical classes.

The `Dwarf` classification is a size/physical-scale category rather than a separate simulation model. A small body orbiting a star can therefore be represented as a Planet with Dwarf size class, while a similarly sized body orbiting a planet is a Moon with Dwarf size class.

### Size classes

The intended size taxonomy is:

- Dwarf;
- Earth-scale;
- Super-Earth;
- Neptunian;
- Giant.

Exact radius/mass ranges remain open and will be defined as generator/content ranges later in this Concept.

### Composition classes

The intended simplified bulk-composition taxonomy is:

- Rocky;
- Icy;
- Mixed;
- Volatile-rich;
- Gas-dominated.

Composition describes broad physical identity and constrains plausible generated properties, but does not itself encode detailed resource inventories.

### Surface classes

A body's visible/gameplay surface identity is separate from bulk composition. The current intended surface taxonomy is:

- Rocky;
- Icy;
- Oceanic;
- Mixed;
- Molten;
- None.

`None` is appropriate for bodies such as gas giants that do not expose a conventional solid reference surface for ordinary world interaction.

### Physical properties

Celestial bodies expose at least:

- mass;
- radius;
- physical classification data;
- current deterministic global position derived from the prescribed orbital hierarchy;
- current deterministic global motion state needed by navigation/Autopilot;
- body-specific gravitational parameters consumed by [Flight Physics](flight-physics.md);
- environmental properties defined below.

Mass and radius are authoritative physical attributes. Derived quantities such as surface gravity may be computed from them rather than independently randomized where doing so preserves consistency.

### Stars

Stars use a simplified stellar identity sufficient for world generation, lighting, environmental radiation and later presentation.

The baseline spectral taxonomy is:

- O;
- B;
- A;
- F;
- G;
- K;
- M.

Spectral class is distinct from evolutionary state. The model should support at least a Main Sequence state and remain extensible to later states such as giant stars or stellar remnants without requiring a different celestial-body model.

A star exposes at least:

- mass;
- radius;
- luminosity;
- effective temperature;
- spectral class;
- evolutionary state.

Stars radiate. Their luminosity contributes to stellar radiation/intensity at other positions in the system. This Concept owns the stellar environmental input; later Thermal/Ship systems own how ships accumulate, dissipate or suffer damage from heat.

### Atmosphere

A non-stellar body's atmosphere is represented at a simplified level.

Where a meaningful reference surface exists, the body has a numeric surface pressure. From that value and later supporting rules, the game can expose a qualitative atmosphere-density class such as:

- None;
- Trace;
- Thin;
- Standard;
- Dense;
- Extreme.

The exact pressure boundaries for these labels remain open.

Atmosphere density/pressure is separate from Atmosphere Compatibility. Compatibility answers whether the atmosphere is directly compatible with unprotected humans. Exact gas composition is intentionally deferred until economy/resource/life-support concepts define what chemical detail the game actually needs.

### Reference temperature and stellar radiation

Each non-stellar body has a stable Reference Surface Temperature representing its broad mean environmental state.

This value is not continuously changed as an instantaneous climate simulation while the body moves along an eccentric orbit. It may be generated or derived from stellar luminosity, average orbital conditions and simplified atmospheric effects.

Separately, stellar radiation at a position is current and distance-dependent. Contributions from all stars in a multi-star system are combined.

This separation allows world classification to remain stable while future ship-thermal systems can still react to current proximity to one or more stars.

### Human habitability

Human Habitability is a derived environmental classification distinct from Atmosphere Compatibility.

The intended qualitative states are:

- Uninhabitable;
- Marginal;
- Habitable;
- Highly Habitable.

Habitability may later consume factors such as reference temperature, surface pressure, atmosphere compatibility and surface conditions. This Concept owns the environmental classification, while later population/economy systems own population capacity, growth and economic consequences.

### Prescribed orbital hierarchy

Celestial bodies do not use dynamic mutual gravitational simulation.

Each orbiting celestial body has an Orbit Parent and a prescribed deterministic orbit. A body's global position is resolved through the hierarchy from its local orbital state relative to its parent.

A simple hierarchy may therefore be:

```text
Star
├── Planet
│   └── Moon
└── Planet
```

The model also supports multi-star hierarchies through Barycenters:

```text
System Barycenter
├── Star A
├── Star B
└── Circumbinary Planet
```

A Barycenter may itself participate in a larger prescribed hierarchy when needed for future multi-star system layouts, but it remains non-physical.

### Orbit shape and direction

Prescribed celestial orbits support circular and elliptic motion.

A circular orbit is represented as the zero-eccentricity case of the same orbital model rather than as a separate system.

Orbits may be prograde or retrograde. Generator rules may later make retrograde motion uncommon for ordinary planets and more common for irregular/captured moons, but generation probability is outside this Concept's current scope.

The gameplay world remains fundamentally 2D/coplanar. The future 3D Galaxy Map may place star systems in three-dimensional galactic space without requiring local star-system flight or celestial orbits to become a full 3D orbital simulation.

### Deterministic celestial state

For a fixed star-system definition, epoch/initial orbital state and simulation time, every prescribed celestial body must have a deterministic position and motion state.

Authored systems and generated systems must use the same rule: a seed or authored definition provides stable content parameters; current celestial state follows deterministically from those parameters and time.

This allows Autopilot, navigation and automated tests to predict future target positions without relying on rendering.

### Dynamic asteroids boundary

Interactive asteroids are not prescribed celestial bodies under this Concept.

They are dynamic objects governed by [Flight Physics](flight-physics.md), react to celestial gravity and may have their trajectories altered by forces/collisions. Asteroid fields or later generator rules may define how such objects are created, but their trajectories are not immutable celestial orbits.

### Standard orbit

Every celestial body that may be selected as a generic Autopilot celestial destination provides a body-specific Standard Orbit definition.

The Standard Orbit includes the orbital radius/altitude required by [Autopilot](autopilot.md). Generic celestial arrival is prograde according to the already-approved Autopilot rules.

The Standard Orbit is navigation content, not an artificial holding mode. After Autopilot insertion, the ship follows normal [Flight Physics](flight-physics.md).

### Orbital anchors for stations

Celestial bodies provide persistent orbital anchors that later station systems may use.

The intended wider-game premise is that stations are built/placed in orbits associated with celestial bodies. Exact station-placement restrictions, allowable orbit bands, construction rules and economic consequences belong to a future Station concept rather than this Concept.

### Visual representation and parallax

Celestial bodies are represented as large deep-layer visual objects tied to their authoritative simulated positions.

Their rendered direction on screen follows their actual relative direction from the camera/ship. Their apparent size increases continuously as distance decreases, but is intentionally stylized rather than constrained to literal astronomical angular size.

The mapping from physical distance to rendered size must remain monotonic and coherent enough that the player can visually understand approach and recession.

Planets/moons may be rendered as simple circles where appropriate. Non-luminous bodies should show a star-facing illuminated side and star-opposed shadowed side. In multi-star systems, all stellar radiation contributes environmentally, while the strongest current stellar lighting contribution defines the default principal light/shadow direction.

The detailed scale function, camera mathematics, render layers and shaders belong to technical architecture/presentation implementation.

### Future procedural generation boundary

A future procedural Star System Generator consumes this Concept's valid body model.

Each star system has a stable seed. Given the same generator version/configuration and seed, the generator is expected to produce the same star-system content definition.

This Concept defines the attribute categories and valid semantic relationships that generated bodies must satisfy. It does not define the random distributions, generation sequence, rejection sampling, stability heuristics or balancing probabilities used by the generator.

### Future economy/population boundary

Celestial bodies will later participate in economic simulation.

Broad world properties such as composition, surface class, atmosphere and habitability may later influence available resources, production options, population support and demand. Concrete resources, atmospheric chemistry, industries, population growth rates and market demand are intentionally deferred until the relevant economy/population concepts exist.

## Rules and Invariants

1. **C-CBO-001:** Celestial bodies are prescribed world objects; their trajectories are not altered by simulated gravitational forces.
2. **C-CBO-002:** Dynamic objects may respond to celestial gravity according to [Flight Physics](flight-physics.md), but celestial bodies do not dynamically respond to one another.
3. **C-CBO-003:** Every celestial body has an orbital role independent from its size and composition classifications.
4. **C-CBO-004:** The normative orbital roles are Star, Planet and Moon.
5. **C-CBO-005:** A Planet orbits a star or stellar-system barycenter; a Moon orbits a planet.
6. **C-CBO-006:** Dwarf is a physical size class rather than a separate movement/simulation model.
7. **C-CBO-007:** Size class and composition class are independent axes.
8. **C-CBO-008:** A body's surface class is distinct from its bulk composition.
9. **C-CBO-009:** Prescribed celestial orbits use one model supporting both circular and elliptic cases.
10. **C-CBO-010:** Prescribed celestial orbits may be prograde or retrograde.
11. **C-CBO-011:** Local star-system celestial motion is modeled in the game's 2D plane; a future 3D galaxy layout does not imply 3D local orbital mechanics.
12. **C-CBO-012:** A Barycenter is a non-physical orbit anchor, does not generate gravity and is not a normal celestial navigation destination.
13. **C-CBO-013:** Multi-star systems may contain planets orbiting an individual star or a shared stellar barycenter.
14. **C-CBO-014:** For fixed star-system content and simulation time, prescribed celestial position and motion state are deterministic.
15. **C-CBO-015:** Authored and procedurally generated systems use the same celestial-body semantic model.
16. **C-CBO-016:** Interactive asteroids are dynamic objects rather than prescribed celestial bodies.
17. **C-CBO-017:** Every generic celestial Autopilot destination exposes a body-specific Standard Orbit.
18. **C-CBO-018:** A Standard Orbit definition supplies navigation context but does not artificially hold an inserted ship in orbit.
19. **C-CBO-019:** Atmosphere surface pressure and Atmosphere Compatibility are distinct properties.
20. **C-CBO-020:** Exact atmospheric gas chemistry is not required by this Concept until another gameplay system establishes a need for it.
21. **C-CBO-021:** Reference Surface Temperature is a stable environmental body property rather than a continuously simulated instantaneous climate value.
22. **C-CBO-022:** Current stellar radiation/intensity is distance-dependent and combines contributions from all stars in the system.
23. **C-CBO-023:** Human Habitability is distinct from Atmosphere Compatibility and is derived from multiple environmental conditions.
24. **C-CBO-024:** Non-luminous celestial bodies visually communicate a lit star-facing side and darker star-opposed side.
25. **C-CBO-025:** In a multi-star system, the strongest current stellar lighting contribution defines the default principal visual light direction while all stars may contribute environmentally.
26. **C-CBO-026:** Apparent celestial-body size is stylized for readability but must change monotonically with physical distance.
27. **C-CBO-027:** Celestial-body visual position remains tied to authoritative relative spatial direction; presentation must not create a contradictory gameplay position.
28. **C-CBO-028:** Celestial bodies provide persistent orbital-anchor identity that later station systems may consume.
29. **C-CBO-029:** Resource inventories, atmospheric chemistry, population behaviour and economic production are not inferred as normative rules from broad body classifications in this Concept.
30. **C-CBO-030:** Future procedural generation must populate the attribute model defined by this Concept rather than inventing a competing celestial-body representation.

## Parameters and Initial Values

Values below identify required semantic parameters. Numerical ranges remain Draft/open until the next design rounds.

| Parameter | Initial value/range | Unit | Tunable | Design purpose / notes |
| --- | ---: | --- | --- | --- |
| Body mass | Body-specific | kg | Yes | Physical identity; consumed by gravity/world systems. |
| Body radius | Body-specific | m | Yes | Physical/world scale identity. |
| Size class | Dwarf / Earth-scale / Super-Earth / Neptunian / Giant | category | Yes | Simplified physical scale taxonomy. |
| Composition class | Rocky / Icy / Mixed / Volatile-rich / Gas-dominated | category | Yes | Simplified bulk composition. |
| Surface class | Rocky / Icy / Oceanic / Mixed / Molten / None | category | Yes | Player-relevant surface character. |
| Surface pressure | Body-specific | Pa or bar | Yes | Numeric atmospheric-pressure basis; qualitative labels derived from it. |
| Atmosphere class | None / Trace / Thin / Standard / Dense / Extreme | category | Derived | Player-facing atmospheric-density category; exact thresholds open. |
| Atmosphere compatibility | Compatible / Incompatible / None | category | Yes | Human breathing/environment compatibility abstraction; exact chemistry deferred. |
| Reference surface temperature | Body-specific | K | Yes | Stable representative environment temperature. |
| Human habitability | Uninhabitable / Marginal / Habitable / Highly Habitable | category | Derived | Broad environmental suitability for humans. |
| Orbit semi-major axis | Body-specific | m | Yes | Primary prescribed orbital size parameter. |
| Orbit eccentricity | 0 ≤ e < 1 for bound elliptic celestial orbit | dimensionless | Yes | 0 represents a circular orbit. |
| Orbit phase/epoch parameter | Body-specific | architecture-defined canonical orbital angle/time value | Yes | Establishes deterministic position at a reference epoch. |
| Orbit direction | Prograde / Retrograde | category | Yes | Direction of prescribed motion. |
| Standard-orbit radius/altitude | Body-specific | m | Yes | Generic celestial Autopilot arrival destination. |
| Stellar luminosity | Star-specific | W or solar-luminosity equivalent | Yes | Environmental radiation source. |
| Stellar effective temperature | Star-specific | K | Yes | Stellar classification/presentation input. |
| Stellar spectral class | O / B / A / F / G / K / M | category | Yes | Simplified stellar spectral identity. |
| Stellar evolutionary state | At least Main Sequence; extensible | category | Yes | Separates spectrum from life-cycle state. |

## States and Transitions

Celestial bodies do not use a gameplay state machine for orbital motion. Their prescribed state evolves continuously and deterministically with simulation time.

A body's classification and authored/generated orbital definition do not normally change during ordinary gameplay under this Concept.

Dynamic transitions such as a body being created/destroyed, stellar evolution occurring during play, planetary terraforming changing atmosphere/habitability, or a world changing economic state are not currently defined and require future owning concepts if introduced.

## Interactions With Other Systems

- [Flight Physics](flight-physics.md) — consumes current celestial positions and gravitational body parameters; owns dynamic motion/gravity response and dynamic asteroids. This Concept owns celestial identity and prescribed motion.
- [Autopilot](autopilot.md) — consumes predicted celestial state and Standard Orbit definitions; owns trajectory planning, transfer execution and physical orbit insertion.
- [Playable Star System](../features/playable-star-system.md) — composes celestial motion with Flight Physics into a traversable moving system.
- [Autopilot Travel](../features/autopilot-travel.md) — uses celestial bodies as moving navigation destinations.
- Future Star System Generation concept — will own seed-driven body creation probabilities/distributions while using this Concept's body model.
- Future Galaxy/Interstellar Travel concept — will own 3D galactic star-system placement and jumps between systems.
- Future Stations concept — will consume celestial bodies as orbital anchors and own valid station-orbit construction/placement rules.
- Future Economy/Population concepts — may consume body composition, atmosphere, surface and habitability; they own concrete resources, production and population effects.
- Future Thermal/Ships concept — may consume current stellar radiation and owns ship heat generation, storage, dissipation, overheat and damage consequences.
- Future Sensors/Detection concept — may consume thermal/signature state and owns detection behaviour.

## Player Feedback and Information

The wider game should be capable of communicating, where relevant:

- body name;
- body orbital role;
- broad physical/world classification;
- current navigation distance;
- current body/environment identity such as atmosphere/habitability when the appropriate UI context exists;
- orbital relationships and parent body in navigation/map views;
- Standard Orbit as the generic celestial arrival destination where relevant;
- visual star-facing illumination direction;
- visually readable approach/recession through changing apparent size.

Exact HUD layout and interaction presentation belong to the relevant UI/navigation concepts.

## Edge Cases

- **Circular orbit:** eccentricity zero uses the same prescribed-orbit model as elliptical motion.
- **Retrograde moon:** valid when its orbit definition specifies retrograde direction; no alternative simulation model is used.
- **Circumbinary planet:** the Planet orbits a stellar Barycenter rather than either star individually.
- **Planet around one star in a multi-star system:** valid when its Orbit Parent is that star; radiation from other stars still contributes at its current position.
- **No atmosphere:** surface pressure is effectively zero and qualitative atmosphere class is None; Atmosphere Compatibility is None rather than Compatible.
- **Gas-dominated giant:** may use Surface Class None; detailed deep-atmosphere modelling is not implied.
- **Strongly eccentric orbit:** Reference Surface Temperature remains a stable world property, while current stellar radiation changes with distance.
- **Dynamic asteroid near a planet:** the asteroid follows Flight Physics and is not converted into a prescribed moon merely because it passes through the planet's vicinity.
- **Barycenter:** cannot be treated as a gravity source, ordinary celestial target or habitable/economic body.
- **Multiple illuminating stars:** environmental radiation is additive; principal visual lighting defaults to the strongest current stellar contribution.

## Examples

### M01 authored system

The M01 test system may be represented as:

```text
Sun (Star, G-type)
├── Earth (Planet, Earth-scale, Rocky)
│   └── Moon (Moon, Dwarf, Rocky)
└── Mars (Planet, Earth-scale, Rocky)
```

For M01, these bodies are authored content rather than generated. They still use the same attribute model intended for the future generator.

Current agreed environmental identity:

- **Earth:** Earth-scale Rocky Planet; atmosphere present with Standard-class pressure; Atmosphere Compatibility = Compatible; Human Habitability expected to be Habitable/Highly Habitable once thresholds are finalized.
- **Mars:** Earth-scale Rocky Planet; thin atmosphere; Atmosphere Compatibility = Incompatible; Human Habitability expected to be Uninhabitable/Marginal depending on final threshold rules.
- **Moon:** Dwarf Rocky Moon; no atmosphere; Atmosphere Compatibility = None; Human Habitability = Uninhabitable under natural surface conditions.

### Multi-star hierarchy

```text
System Barycenter
├── Star A
├── Star B
└── Planet AB-1
```

Star A and Star B follow prescribed orbits around the Barycenter. Planet AB-1 follows its own prescribed circumbinary orbit. The Barycenter itself produces no gravity.

## Design Decisions and Rationale

| ID | Decision | Rationale | Consequences |
| --- | --- | --- | --- |
| D-CBO-001 | Celestial orbits are prescribed rather than dynamically produced by N-body gravity. | Stable deterministic worlds are more valuable than full stellar mechanics and already align with Flight Physics. | Celestial trajectories never drift due to simulation forces. |
| D-CBO-002 | Orbital role, size class and composition class are separate axes. | Avoids conflating hierarchy with physical nature and supports realistic variety among planets/moons. | Generator/content must populate multiple independent classifications. |
| D-CBO-003 | Dwarf is treated as a physical size category rather than a separate movement model. | Keeps small planets/moons structurally consistent with larger bodies. | Small star-orbiting bodies remain Planet role with Dwarf size class. |
| D-CBO-004 | Elliptic and circular orbits share one model. | Preserves useful astronomical variety without duplicate systems. | Circular orbit is eccentricity 0. |
| D-CBO-005 | Prograde and retrograde prescribed orbits are supported. | Allows irregular/captured-moon style systems without special-case motion. | Generator later determines frequency. |
| D-CBO-006 | Multi-star systems are supported through non-physical Barycenters. | Enables individual-star and circumbinary orbital hierarchies cleanly. | Barycenters require no gravity/physical-body behaviour. |
| D-CBO-007 | Local star-system simulation remains 2D even though the future galaxy map is 3D. | Preserves the core top-down game while allowing spatial galactic navigation. | Local orbital inclination is not a gameplay dimension. |
| D-CBO-008 | Atmosphere uses numeric surface pressure plus derived qualitative class and separate compatibility. | Supports generation/consistency while keeping player-facing meaning simple. | Detailed gas chemistry can remain deferred. |
| D-CBO-009 | Reference Surface Temperature is stable while current stellar radiation is dynamic. | Avoids unnecessary climate simulation but preserves meaningful stellar-proximity effects for later ship thermal systems. | World classification remains stable along eccentric orbits. |
| D-CBO-010 | Human Habitability is derived and distinct from breathable atmosphere. | Temperature/pressure/surface conditions matter independently of breathing compatibility. | Economy/population can consume one environmental suitability signal later. |
| D-CBO-011 | Surface class is separate from bulk composition. | A body's visible/interactive surface may differ from its overall composition. | Supports oceanic/icy/molten worlds without overloading composition. |
| D-CBO-012 | Radiation from all stars combines; strongest stellar contribution drives the default primary visual light direction. | Multi-star systems should remain physically coherent without requiring complex multi-light gameplay presentation. | Environment and visuals use related but not identical simplifications. |
| D-CBO-013 | Apparent body size is stylized but monotonic with distance. | Literal angular scale would make planets unreadably small over most gameplay distances. | Rendering must preserve approach/recession cues rather than real angular size. |
| D-CBO-014 | Authored and generated systems share the same body model. | Prevents M01 content from becoming a throwaway structure incompatible with future generation. | M01 data must already populate the long-term semantic fields needed by this Concept. |

## Rejected or Deferred Alternatives

| Alternative | Status | Reason |
| --- | --- | --- |
| Fully dynamic N-body celestial mechanics | Rejected | Adds instability/complexity without corresponding gameplay value and conflicts with the prescribed-world model already established in Flight Physics. |
| Separate simulation model for moons | Rejected | Moons should use the same body/environment/orbit model as planets; only orbital role/parent differs. |
| Strict real-angular-size rendering | Rejected | Would make celestial bodies visually negligible through much of large-system travel. |
| Single combined physical body class such as `Terrestrial Moon` | Rejected | Conflates orbital hierarchy, size and composition and limits generator flexibility. |
| Atmosphere represented only by qualitative labels | Rejected | Numeric pressure provides a consistent generation/derivation basis while still allowing simplified labels. |
| Only one star influences a planet's environment | Rejected | Fails for circumbinary/multi-star systems. |
| Dynamic instantaneous climate simulation along eccentric orbits | Rejected | Additional complexity is not required for the intended gameplay model. |
| Detailed atmosphere chemistry and explicit resource inventories now | Deferred | These need the economy/resource/life-support design first to avoid modelling unused detail. |
| Procedural generation probability tables | Deferred | Belong to the future Star System Generation concept after the valid body model and ranges are complete. |

## Open Questions

- [ ] Define exact radius/mass ranges and plausibility constraints for Dwarf, Earth-scale, Super-Earth, Neptunian and Giant bodies.
- [ ] Define exact atmosphere surface-pressure thresholds for None, Trace, Thin, Standard, Dense and Extreme.
- [ ] Define reference-temperature categories/ranges and the derivation semantics used for Human Habitability.
- [ ] Define exact Human Habitability thresholds for Uninhabitable, Marginal, Habitable and Highly Habitable.
- [ ] Define the acceptable combinations/constraints between size class, composition class and surface class.
- [ ] Define baseline numeric ranges for O/B/A/F/G/K/M Main Sequence star mass, radius, luminosity and effective temperature suitable for generation.
- [ ] Decide which stellar evolutionary states beyond Main Sequence are required for the final generator's initial scope.
- [ ] Define required prescribed-orbit parameters beyond semi-major axis, eccentricity, phase/epoch and direction for the 2D model.
- [ ] Decide whether moons of moons/submoons are allowed or the hierarchy stops at Planet -> Moon.
- [ ] Define how Standard Orbit radius/altitude is selected for different body sizes/classes.

## Acceptance Criteria

- [ ] Authored and future generated star systems can describe stars, planets and moons through one common semantic model.
- [ ] A body's orbital role does not constrain it to one composition or atmosphere model beyond explicit plausibility rules.
- [ ] Circular, elliptical, prograde and retrograde prescribed orbits can be represented without separate movement systems.
- [ ] Multi-star systems can represent individual-star and circumbinary orbital hierarchies through non-physical Barycenters.
- [ ] For fixed content and simulation time, celestial state is deterministic and usable without rendering.
- [ ] Flight Physics can consume current celestial positions/gravity parameters without requiring celestial bodies to become dynamic objects.
- [ ] Autopilot can obtain a future celestial destination state and a body-specific Standard Orbit.
- [ ] Atmosphere, reference temperature and human habitability are represented at the agreed simplified level without requiring detailed chemistry.
- [ ] Current radiation from multiple stars can be combined independently from stable body climate classification.
- [ ] Celestial presentation communicates relative direction, approach/recession and illuminated/dark sides without redefining physical position.
- [ ] M01's Sun, Earth, Moon and Mars can be authored with this model without introducing milestone-only body semantics.
- [ ] Future station/economy/population/thermal/sensor systems can consume celestial properties through clear ownership boundaries rather than requiring this Concept to define their gameplay.

## Change Log

| Version | Date | Change |
| --- | --- | --- |
| 0.1 | 2026-09-14 | Expanded Planned stub into active Draft; captured agreed classification, orbital hierarchy, multi-star, atmosphere, habitability, stellar-radiation and presentation model. |
