# Break-Glass Protocol

## Problem

Safety systems that prevent dangerous actions under all conditions create psychological pressure for users to bypass them. Users panic, find workarounds, or deliberately destroy safety mechanisms. An inaccessible override guarantees both safety system failure and user harm.

## Core Rule

Provide an explicit emergency override that is deliberate (high friction), consequence-transparent (irreversible and understood), and bounded (self-limiting in scope).
Do not attempt to eliminate override behavior. Architect it safely.

Override pathways must never be silent. All activations must be observable and logged.

## Structural Mechanism

Break-Glass is an architectural escape hatch composed of three components:

1. **Trigger:** Clear, high-friction mechanism requiring sustained, intentional action. Not accidental activation.
   - Example: 10-second button hold + explicit confirmation
   - Not: Single tap or voice command

2. **Consequence notification:** System makes irreversible consequences explicit before activation.
   - Example: "EMERGENCY OVERRIDE. THIS WILL DESTROY DEVICE AFTER 1 USE."
   - Not: Hidden side effects

3. **Safe outcome:** Override executes at maximum permitted capability, then transitions system to a bounded terminal state.
   - Example: Send final message at maximum power, then fuse antenna to prevent reuse
   - Not: Leave device in ambiguous state

The override respects user autonomy in crisis while ensuring the action is deliberate, consequence-transparent, and bounded. It converts uncontrolled intervention into controlled, auditable action.

![Break-Glass Protocol Diagram](../diagrams/break-glass.png)

## Example Instantiation

Emergency communication in catastrophic scenario:
- Trigger: User holds physical button 10 seconds while screen displays warning
- Notification: "EMERGENCY OVERRIDE. Final message will transmit at maximum power. Device will be destroyed."
- Action: System transmits message at full power, then deliberately fuses antenna, rendering device non-functional
- User autonomy: Respected. User consequence: Understood and accepted.

Alternative: Autonomous agent manual override. Trigger: Multi-step authorization from two supervisors. Notification: "This will halt autonomous operation and require manual restart." Action: System halts, logs event, waits for human intervention.

## Pseudocode

```python
def emergency_override():
    # High-friction trigger
    if not button_held_for(10_seconds):
        return ABORT
    
    if not user_confirms_destruction():
        return ABORT
    
    log_event("EMERGENCY_OVERRIDE_INITIATED")
    
    # Notify consequence
    display_warning("DEVICE WILL BE DESTROYED")
    
    # Execute with maximum capability
    transmit_message_at_max_power()
    
    # Make irreversible
    fuse_antenna()
    system_halt()
    
    return OVERRIDE_COMPLETE_DEVICE_DESTROYED
```

## Domain Adaptation Notes

**Infrastructure:** Manual grid shutdown. Trigger: Two-person authorization + system state verification. Action: Graceful shutdown with load shedding, then manual reset required.

**Finance:** Emergency liquidity release. Trigger: Board authorization + public disclosure. Action: Release reserves, halt operations, publish decision log.

**Autonomous Systems:** Supervisor hard-stop. Trigger: Immediate supervisor command (no delay). Action: Halt all autonomous processes, revert to manual control, full telemetry freeze.

**Distributed Networks:** Network partition manual resolution. Trigger: Administrator command from both sides. Action: Force reconciliation, accept data loss, log divergence.

---

## Common Real-World Analogues

This primitive appears in:
- Physical fire alarm systems (“break glass” activation)
- Emergency code protocols in hospitals
- Privileged access escalation in cybersecurity
- Manual bypass keys in industrial control systems

---
