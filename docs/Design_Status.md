# Design Status

## Current State

Hourglass is currently at the **architectural / conceptual** stage.

The core responsibility is established:

> Only Hourglass may authorize physical execution.

The homeostatic model is also established at the conceptual level:

- Fast event path for immediate constraints
- Slow homeostatic path for accumulated state
- Risk, power, thermal, and fault as candidate state classes
- Accumulated adverse conditions may tighten future constraints

## Not Yet Frozen

The following are intentionally open:

- Exact state representation
- Threshold equations
- Memory update rules
- Decay / recovery rules
- Module API
- Synchronization
- Timing guarantees
- Error semantics
- Hardware mapping
- Verification methodology

## Implementation Status

No completed implementation is claimed by this repository version.

Future implementation should be developed only after the relevant interfaces and state semantics are sufficiently specified.

## Hardware Direction

Hardware-assisted enforcement may be investigated later.

Examples include secure execution environments, trusted policy storage, hardware access control, or other execution-boundary mechanisms.

These possibilities should not be interpreted as current Hourglass capabilities.

## Terminology

The following distinction is intentional:

- **Architecture** — what responsibility belongs to Hourglass.
- **Implementation** — how that responsibility is realized in software or hardware.
- **Enforcement mechanism** — how the execution boundary is made resistant to bypass.

Keeping these concepts separate prevents an architectural principle from being presented as an already implemented security mechanism.
