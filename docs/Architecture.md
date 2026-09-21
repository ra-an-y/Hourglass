# Hourglass Architecture

## 1. Purpose

Hourglass is the execution-authorization core of the Sandman architecture.

Its responsibility is to evaluate proposed actions against current constraints and accumulated homeostatic state before physical execution.

It is not the component responsible for generating high-level decisions.

## 2. Authority Boundary

The proposed architecture separates decision formation from execution authorization.

    SNN Mesh
        |
        v
    Artificial Prefrontal
        |
        | Proposed Action
        v
    Hourglass
        |
        | Authorization Result
        v
    Physical Execution

Only Hourglass owns the authorization step within this architecture.

An authorization result may be ALLOW, BLOCK, DELAY, or LIMIT. Physical execution therefore occurs only when the resulting policy permits execution.

## 3. Computation Paths

Hourglass contains two conceptual paths.

### Fast Event Path

Processes an immediate request against instantaneous constraints.

    Request -> Current State -> Authorization

### Slow Homeostatic Path

Maintains accumulated state that can affect later authorization.

    Events -> Homeostatic Memory -> Constraint State -> Future Authorization

These paths are complementary rather than mutually exclusive.

## 4. Homeostatic State

The current design considers:

- Risk
- Power
- Thermal
- Fault

The purpose of these states is to preserve operational conditions relevant to future authorization.

Homeostatic state is intended to be conservative:

> Accumulated adverse conditions may tighten restrictions, but accumulated state does not autonomously relax restrictions.

The concrete mathematical and implementation model remains open.

## 5. External Constraints

Hourglass receives relevant constraints from other Sandman modules.

### Power Management

Potential inputs:

- Available power
- Battery state
- Peak power budget

### Thermal Fountain

Potential inputs:

- Temperature
- Heat load
- Cooling capacity

These modules retain their own responsibilities. Hourglass consumes their relevant state for authorization rather than replacing them.

## 6. Authorization Results

The current conceptual result set is:

- ALLOW
- BLOCK
- DELAY
- LIMIT

The exact API and data representation are not yet frozen.

## 7. Non-Claims

The current architecture does not claim:

- Hardware-enforced immutability
- A hardware root of trust
- TEE enforcement
- NPU/neuromorphic fail-safe enforcement
- A completed implementation
- Formal safety certification

Those are possible future implementation or research directions, not current capabilities.

## 8. Design Boundary

Hourglass should remain a distinct execution-authorization layer.

Its architecture should not be expanded merely by absorbing functionality that belongs to:

- SNN Mesh
- Artificial Prefrontal
- Power Management
- Thermal Fountain

The purpose of the module boundary is to keep decision formation, resource management, thermal management, and execution authorization distinguishable.
