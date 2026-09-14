# Game Vision

**Status:** Draft  
**Version:** 0.1  

## Table of Contents

1. [Vision](#vision)
2. [Core Experience](#core-experience)
3. [World](#world)
4. [Flight](#flight)
5. [Ships and Combat](#ships-and-combat)
6. [Presentation](#presentation)
7. [Interface](#interface)
8. [Development Direction](#development-direction)

## Vision

Codename Expanse is a modern browser-based 2D top-down space simulation inspired by the readability of games such as Starsector and classic browser space games, while pursuing a deeper physically grounded simulation beneath accessible controls.

## Core Experience

The player directly flies a spacecraft inside a very large star system, travels between meaningful locations, fits ships with visible modules, interacts with stations and NPCs, and fights at both local and potentially very long ranges.

The simulation should remain internally coherent even when assists make local control feel arcade-like.

## World

Star systems are intended to feel enormous rather than compressed into a few screens. They contain stars, procedurally generated planets, asteroid fields, stations, NPCs and other points of interest.

Large-scale travel should require sustained acceleration/coasting/deceleration or an autopilot capable of planning such manoeuvres.

## Flight

Base flight follows inertia: removing thrust does not implicitly remove velocity. Optional flight-assist/autopilot modes may apply counter-thrust to create a more familiar, damped control mode.

The physically simulated state remains authoritative regardless of how assists generate control inputs.

## Ships and Combat

Ships use visible hardpoints. Weapons/modules can be installed through a ship editor and should be represented on the ship where practical.

A target ship can be selected and individual modules/subsystems may later be targetable. The simulation should permit very long-lived projectiles such as a railgun round travelling far beyond the immediate camera view when technically/gameplay appropriate.

## Presentation

The world uses layered rendering, lighting/shadow effects and parallax to communicate depth and scale. Distant stars, dust and environmental layers should react differently to camera/world movement.

Approaching a region such as an asteroid field should progressively reveal denser/more local environmental detail rather than switching abruptly from empty space to a field.

Large planets and possibly stations may use lower/deeper visual layers to communicate scale while remaining tied to their actual simulated location.

## Interface

The HUD should remain compact. Contextual popups show selected-object information. A bottom action area exposes active modules and ship energy/capacitor state. Energy can be distributed between systems such as shields, weapons and propulsion.

Selecting a target may open a secondary target view in the upper-right, effectively rendering another camera/view of the same simulation and enabling subsystem inspection/selection.

## Development Direction

The first milestone is a high-quality browser-only prototype. A server architecture may follow later. Early architecture should therefore avoid unnecessary coupling between rendering/UI and authoritative simulation state.
