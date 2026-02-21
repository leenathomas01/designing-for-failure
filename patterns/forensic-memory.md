# Forensic Memory

## Problem

Systems that survive catastrophic events learn nothing. Next event uses same thresholds, same logic, same assumptions. The system repeats the same failure mode because it has no record of what failed or why.

## Core Rule

After catastrophic events, maintain an immutable record of: what signals failed, when they failed, how the system responded, and what thresholds proved inadequate. Use structured analysis of these records to adjust thresholds, quorum requirements, and recovery durations.

## Structural Mechanism

Forensic memory is a bounded, append-only log that records each catastrophic event as a discrete entry. Records are immutable once written, preserving integrity for analysis. Retention scope and access controls are defined at system design time:

1. **Event entry:** Timestamp, trigger condition, system state at entry
2. **Detection phase:** What signal detected the crisis, when, confidence level
3. **Response phase:** What actions the system took, duration, outcome
4. **Recovery phase:** Time to exit crisis state, signals that confirmed recovery
5. **Analysis:** Comparison of predicted vs. actual behavior. Threshold adequacy assessment.

After analysis, the system updates operating parameters for next event (e.g., lower entry threshold, longer recovery duration, additional signal source). Forensic memory must not alter live system behavior during crisis. Analysis occurs post-recovery to avoid feedback amplification during instability.

Closed loop: Event → Detection → Containment → Recovery → Analysis → Parameter Adjustment → Updated Operating Baseline.

![Sacrificial Architecture Diagram](../diagrams/forensic-memory.png)

## Example Instantiation

Communication system experiencing geomagnetic disruptions:

**Event 1:**
- Entry trigger: HF noise floor collapses
- Recovery time: 8 hours
- Lesson: 35% stress threshold was adequate but late
- Adjustment: Lower threshold to 25%, increase recovery confirmation to 6 hours

**Event 2 (improved):**
- Entry trigger: Stress at 25% (earlier detection)
- Recovery time: 6 hours (faster due to learned thresholds)
- Lesson: Lower threshold improved performance; 25% is effective

**Event 3 (further improved):**
- New lesson: Two signals are insufficient; add third signal source
- Adjustment: Quorum increases to 3 sources

Each event iteratively improves system response.

## Pseudocode

```python
class ForensicLog:
    def __init__(self):
        self.immutable_log = []
    
    def record_event(self, event_record):
        # Immutable append
        self.immutable_log.append({
            "timestamp": now(),
            "entry_trigger": event_record.trigger,
            "detection_confidence": event_record.confidence,
            "recovery_duration": event_record.recovery_time,
            "signals_used": event_record.signals,
            "threshold_assessment": event_record.threshold_eval
        })
    
    def analyze_trends(self):
        # Compare predicted vs. actual
        recovery_times = [e["recovery_duration"] for e in self.immutable_log]
        threshold_failures = [e for e in self.immutable_log 
                            if e["threshold_assessment"] == "INADEQUATE"]
        return {
            "recommended_threshold_adjustment": compute_adjustment(threshold_failures),
            "recommended_recovery_duration": compute_duration(recovery_times)
        }
    
    def update_parameters(self):
        adjustments = self.analyze_trends()
        return adjustments  # Feed to system configuration
```

## Domain Adaptation Notes

**Infrastructure:** Blackout recovery log. Record: cascade patterns, recovery times, which load-shedding algorithms worked. Adjust: load-shedding parameters based on repeated failures.

**Finance:** Bank-run event log. Record: liquidity drain rate, circuit-breaker effectiveness, recovery timeline. Adjust: trigger thresholds, buffer sizes, reset protocols.

**Autonomous Systems:** Containment event log. Record: what anomaly triggered shutdown, how long autonomous recovery took, which validators were most predictive. Adjust: anomaly detection sensitivity, validation quorum.

**Distributed Networks:** Network partition log. Record: partition duration, divergence in state, reconciliation time. Adjust: consensus timeouts, quorum sizes, partition detection sensitivity.

---

