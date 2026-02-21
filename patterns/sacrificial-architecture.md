# Sacrificial Architecture

## Problem

Catastrophic events destroy entire systems if all components fail together. Without intentional isolation, a surge affects sensors, processing, storage, and actuation equally. The system collapses completely, leaving no core to recover from.

## Core Rule

Partition the system into a sacrificial layer and a protected core. The sacrificial layer is engineered to fail first under extreme stress, physically or logically disconnecting from the core to prevent cascade.

## Structural Mechanism

Sacrificial architecture separates system into concentric zones:

- **Outer layer (sacrificial):** Antenna, buffers, sensors, temporary memory. Designed to fail fast under extreme stress.
- **Inner layer (protected core):** Essential processing, permanent data storage, irreplaceable logic. Protected from surge currents and failure propagation.
- **Trigger mechanism:** When stress exceeds threshold, the sacrificial layer fails deliberately, physically disconnecting from the core via fuse, circuit breaker, or similar.

Once sacrificial layer fails, the core survives in degraded but functional state. Recovery involves replacing the sacrificial component only, not rebuilding the entire system. Failure is intentional and bounded. Cascade is prevented by design.

![Sacrificial Architecture Diagram](../diagrams/sacrificial-architecture.png)

## Example Instantiation

Communication device under geomagnetic surge:
- Sacrificial: Antenna conducts surge current. Fuse-antenna component melts at threshold, electrically disconnecting from core.
- Protected core: CPU, storage, processing logic isolated by inductor/capacitor. Survives intact.
- Recovery: Replace antenna. Restart device. Core data and logic preserved.

Alternative: Liquidity buffer in financial system. Sacrificial component (10% of reserves) is burned to halt a bank run. Protected core (90% of reserves and essential operations) survives. Recovery involves rebuilding reserves over time.

## Pseudocode

```python
class SafeguardedSystem:
    def __init__(self):
        self.sacrificial = SacrificialComponent()
        self.core = ProtectedCore()
        self.fuse = Fuse(threshold=100_amperes)
    
    def on_surge_detected(self, current):
        if current > self.fuse.threshold:
            self.fuse.blow()  # Sacrificial fails deliberately
            self.core.enter_safe_state()
            return CORE_PROTECTED
        return NOMINAL

def recover():
    if core.is_intact():
        replace_sacrificial_component()
        return SYSTEM_RECOVERED
```

## Domain Adaptation Notes

**Infrastructure:** Load shedding in power grids. Sacrificial: non-critical zones. Protected core: essential infrastructure. Trigger: frequency deviation beyond threshold.

**Finance:** Liquidity buffer drawdown. Sacrificial: reserve funds (10%). Protected core: essential operations. Trigger: deposit withdrawal rate exceeds threshold.

**Autonomous Systems:** Context memory purge. Sacrificial: recent reasoning trace. Protected core: core objectives and state. Trigger: recursion depth exceeds limit.

**Distributed Networks:** Shedding non-critical peers. Sacrificial: non-consensus peers. Protected core: quorum. Trigger: network partition detected.

---

