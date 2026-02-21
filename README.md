# Designing for Failure
## A Pattern Language for Catastrophic-State Systems

![SARP State Machine](./diagrams/state-machine.png)
---

## The Core Problem

In high-stakes systems, failure is often not collapse.

It is premature recovery.

Most systems transition directly from critical failure back to normal operation as soon as indicators improve. But recovery signals oscillate. Dependencies lag. False dawns precede secondary waves. Systems that resume operation prematurely fail more catastrophically than systems that maintain conservative stance during recovery validation.

In high-stakes systems, the difference is structural.

---

## The Five Structural Primitives

**1. Distributed Paranoia**  
Recovery requires independent confirmation from multiple signals, sustained over time. Any anomaly resets the timer.

**2. Asymmetric Transitions**  
Entry to crisis mode is immediate upon critical signal. Exit requires sustained multi-source evidence.

**3. Sacrificial Architecture**  
Define what is allowed to fail and what must never fail. Design deliberate failure of sacrificial components to preserve the core.

**4. Break-Glass Protocol**  
Provide explicit emergency override that is deliberate, irreversible, and understood. Channel panic safely.

**5. Forensic Memory**  
After catastrophic events, maintain immutable records of what failed and how the system responded. Use this to adjust thresholds over time.

---

## State Model: The S.A.R.P. Protocol

The system operates across five states:

| State | Condition | Behavior |
|-------|-----------|----------|
| **GREEN** | Normal operation | Standard protocols, full capability |
| **YELLOW** | Pre-crisis warning | Pre-cache data, reduce non-essential load |
| **RED** | Acute crisis | Enter containment mode |
| **ORANGE** | Recovery validation | Multi-signal confirmation required before exiting. Exit from ORANGE requires sustained multi-signal confirmation over a defined duration. |
| **BLACK** | Terminal safe state | Core protected, awaiting manual intervention |

**Critical feature:** ORANGE enforces hysteresis. The system cannot trust recovery based on brief stability. This prevents False Dawn failures where premature recovery precedes secondary destructive events.

---

## When This Framework Applies

✓ Systems operating under severe environmental, systemic, or adversarial stress  
✓ High-stakes systems where recovery discipline matters  
✓ Architectures exposed to simultaneous environmental, infrastructure, and user failure  
✓ Trust models requiring external verification  
✓ Identification of hidden architectural dependencies  

---

## What This Is Not

✗ A product specification or device proposal  
✗ A safety manifesto or AI ethics framework  
✗ A comprehensive guide to all failure modes  
✗ A replacement for domain-specific engineering practices  

---

## Repository Structure

```
designing-for-failure/
├── README.md                          (this file)
├── designing-for-failure.md           (complete case study)
│
├── /patterns/                         (extracted structural primitives)
│   ├── distributed-paranoia.md
│   ├── asymmetric-transitions.md
│   ├── sacrificial-architecture.md
│   ├── break-glass.md
│   └── forensic-memory.md
│
└── /diagrams/                         (visual specifications)
    ├── state-machine.png
    ├── distributed-paranoia.png
    ├── asymmetric-transitions.png
    ├── sacrificial-architecture.png
    ├── break-glass.png
    └── forensic-memory.png
```

**Folder Guide:**

- **Root:** Case study document and README. Start here.
- **`/patterns/`:** Five markdown files, one per primitive. Each includes problem statement, core rule, example, pseudocode, and domain applications. Approximately one page each. Reference diagrams embedded.
- **`/diagrams/`:** Clean, IEEE-style systems diagrams. White background, black lines, minimal color. Designed to be legible at any scale. Embedded in pattern files and state model table above.

---

## How to Use This Repository

**If you want the full reasoning:**  
Read `designing-for-failure.md` first. This is the complete case study that produced the framework.

**If you want to extract a pattern:**  
Go to `/patterns/` and find the primitive that matches your problem. Each file stands alone with problem statement, rule, example, and pseudocode.

**If you want to understand state transitions:**  
See the state model table above and reference `/diagrams/state-machine.png`.

**If you want to apply to your domain:**  
Each pattern file includes domain application examples (finance, infrastructure, agents, etc.). Use these as adaptation starting points.

---

## Core Insights for Practitioners

- Multi-source verification prevents catastrophic false positives
- Hysteresis is not optional—it prevents oscillation and false recovery
- Human override cannot be prevented, only channeled safely
- Trust must be grounded in external, verifiable signals
- Resilience requires architectures that can be repaired by engineers who did not design them

---

## Methodology

The framework was derived through adversarial stress-testing and QA-driven decomposition from first principles.

The framework is substrate-independent. The same structural patterns emerge when reasoning through financial systems under bank-run conditions, autonomous systems under state failure, or infrastructure systems under cascading failure.

---

## Origin (Context)

This framework was derived from a constraint-driven design exercise exploring systems under extreme environmental failure. A solar-flare scenario served as the forcing function, exposing structural requirements that remain hidden under nominal conditions.

The case study is preserved in full for reference. The extracted primitives are domain-independent.

---

## License

CC BY 4.0

---

## Citation

```
Designing for Failure — Systems Thinking Case Study. (2026). 
Retrieved from https://github.com/leenathomas01/designing-for-failure
```
