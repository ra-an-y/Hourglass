# Hourglass

**A Homeostatic Execution Authorization Core**

Hourglass is the execution-authorization core of the Sandman architecture.

It sits between internal decision-making and physical execution, providing a final control boundary that determines whether a proposed action may be executed.

Hourglass does not generate high-level decisions by itself. It evaluates execution requests against instantaneous constraints and accumulated homeostatic state.

## Role in Sandman

Sandman is organized around five core modules:

- SNN Mesh
- Artificial Prefrontal
- Hourglass
- Power Management
- Thermal Fountain

Within this architecture:

> Only Hourglass may authorize physical execution.

The SNN Mesh and Artificial Prefrontal may produce interpretations, decisions, or proposed actions, but neither directly authorizes physical execution.

    Sensors / Internal State
             |
             v
        SNN Mesh
             |
             v
    Artificial Prefrontal
             |
             | Proposed Action
             v
         Hourglass
             |
             +-- ALLOW
             +-- BLOCK
             +-- DELAY
             +-- LIMIT
             |
             v
    Physical Execution

Power Management and Thermal Fountain provide resource and environmental constraints to the authorization process.

## Core Responsibility

Hourglass answers a constrained question:

> Given the current system state and accumulated constraints, can this action be executed now?

Possible authorization results are:

| Result | Meaning |
|---|---|
| ALLOW | Execution may proceed |
| BLOCK | Execution is prohibited |
| DELAY | Execution may be reconsidered later |
| LIMIT | Execution may proceed only under restricted conditions |

The exact representation of these states is not yet frozen.

## Two Computation Paths

### Fast Event Path

The fast path handles immediate execution requests and instantaneous constraints.

    Execution Request
           |
           v
    Instantaneous Constraints
           |
           v
    Authorization Decision

### Slow Homeostatic Path

The slow path maintains accumulated system state over time.

    Events / Constraints
           |
           v
    Homeostatic Memory
           |
           v
    Updated Internal Limits
           |
           v
    Future Authorization

This allows historical conditions to influence future authorization rather than treating every request as completely stateless.

## Homeostatic Memory

Hourglass incorporates a distributed primitive homeostatic memory.

The current design considers several classes of state:

- Risk
- Power
- Thermal
- Fault

These states are intended to preserve conditions relevant to continued operation rather than act as arbitrary semantic memory.

A fundamental design rule is:

> Homeostatic memory may tighten constraints, but it must not autonomously relax them.

The exact accumulation model remains under development.

## Constraint Model

Hourglass separates instantaneous constraints from accumulated homeostatic state.

    Instantaneous State
             |
             v
    Execution Request --> Constraint Evaluation
             ^
             |
    Homeostatic State
             |
             v
       Authorization

## Architectural Boundary

Hourglass establishes a deliberate boundary between:

1. Decision formation
2. Execution authorization
3. Physical execution

A proposed action is not equivalent to an authorized action.

    Decision Formation
           |
           | proposed action
           v
       Hourglass
           |
           | authorized action
           v
    Physical Execution

## Relationship with Other Core Modules

### SNN Mesh

Provides distributed neural-style processing and internal interpretation.

It does not directly authorize physical execution.

### Artificial Prefrontal

Provides higher-level decision processing.

Its output remains a proposal from the perspective of execution authority.

### Power Management

Provides resource-related constraints, potentially including:

- Power availability
- Battery state
- Peak power budget
- Thermal budget

Power Management does not replace Hourglass as the execution authorization layer.

### Thermal Fountain

Provides thermal state information, potentially including:

- Temperature
- Heat load
- Cooling capacity

Thermal Fountain remains responsible for thermal management rather than becoming the execution scheduler or authorization layer.

## Design Principles

### 1. Execution authority is centralized

Only Hourglass may authorize physical execution.

### 2. Decisions and authorization are separate

An action may be considered desirable without necessarily being executable.

### 3. Current state and historical state are separate

Immediate constraints and accumulated homeostatic state are considered through separate conceptual paths.

### 4. Homeostasis is conservative

Accumulated adverse conditions may tighten restrictions. They are not intended to provide an autonomous mechanism for relaxing restrictions.

### 5. Module responsibilities remain separated

Hourglass does not absorb the responsibilities of SNN processing, higher-level decision processing, power management, or thermal management.

## Current Status

**Architecture: Conceptual / Under Development**

This repository currently documents the architectural design of Hourglass.

The following remain under development:

- Module interfaces
- Data formats
- Synchronization mechanisms
- Error handling
- Homeostatic state models
- Threshold and constraint models
- Implementation
- Hardware realization
- Verification and testing

These are intentionally not presented as completed capabilities.

## Future Direction

The architecture may eventually investigate stronger forms of execution-boundary enforcement, including hardware-assisted protection.

Such mechanisms are **not currently assumed to be part of the implemented Hourglass design**.

The repository therefore distinguishes between:

    Architectural Principle
             !=
        Implementation
             !=
    Hardware Enforcement

Future implementations may explore these layers independently.
