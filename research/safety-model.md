VALI Safety Model
1. Safety Philosophy

Safety is not an operational add-on to VALI.

It is a core architectural constraint.

VALI must remain useful even when:

a lure is compromised
an attacker discovers the deception
telemetry is malicious
an operator makes a mistake
an AI component produces an incorrect conclusion

The central safety principle is:

A compromised deception environment must not become a compromised real environment.

2. Safety Layers
┌────────────────────────────────────┐
│          GOVERNANCE LAYER          │
│ Authorization • Audit • Policy     │
└──────────────────┬─────────────────┘
                   ↓
┌────────────────────────────────────┐
│          IDENTITY LAYER            │
│ Least Privilege • Synthetic IDs    │
└──────────────────┬─────────────────┘
                   ↓
┌────────────────────────────────────┐
│          NETWORK LAYER             │
│ Segmentation • Egress Controls     │
└──────────────────┬─────────────────┘
                   ↓
┌────────────────────────────────────┐
│          EXECUTION LAYER           │
│ Isolation • Sandboxing              │
└──────────────────┬─────────────────┘
                   ↓
┌────────────────────────────────────┐
│          DATA LAYER                │
│ Synthetic Data • Secret Controls   │
└──────────────────┬─────────────────┘
                   ↓
┌────────────────────────────────────┐
│          OBSERVABILITY             │
│ Audit • Integrity • Monitoring     │
└────────────────────────────────────┘
3. Network Isolation

The deception environment should operate inside an explicitly controlled network boundary.

Recommended principles:

deny-by-default
explicit allowlists
controlled outbound traffic
separate management plane
separate telemetry plane
no unrestricted production connectivity

Conceptual model:

Internet
   │
   ▼
VALI Gateway
   │
   ▼
Deception Network
   │
   ├── Lures
   ├── Decoys
   └── Isolated Workloads
   │
   ▼
Telemetry Collector
   │
   ▼
Analysis Environment


Production Network
       ✕
       │
       └── No direct trust
4. Identity Safety

VALI should prefer:

synthetic users
synthetic credentials
synthetic API tokens
fake organizational identities
non-production certificates

Real production credentials should not be intentionally exposed inside deception environments.

5. Data Safety

Deception data should be synthetic whenever possible.

Examples:

Synthetic Customer
Synthetic Account
Synthetic Order
Synthetic API
Synthetic Database
Synthetic Documents
Synthetic Credentials

The objective is to provide realistic interaction without exposing actual sensitive information.

6. Telemetry Safety

Telemetry itself may contain hostile content.

Therefore:

treat logs as untrusted input
sanitize visualization
prevent command interpretation
restrict analyst execution paths
protect log integrity
separate raw evidence from interpreted intelligence
7. AI Safety

AI components should operate under explicit boundaries.

Evidence
   ↓
AI Analysis
   ↓
Hypothesis
   ↓
Confidence
   ↓
Evidence Validation
   ↓
Human Review
   ↓
Defensive Decision

AI should not independently:

retaliate
attack external systems
modify production security controls without authorization
access unrelated sensitive systems
expand its own privileges
8. Kill-Switch

VALI should support an emergency shutdown mechanism.

Potential triggers:

isolation failure
unexpected egress
credential exposure
abnormal resource consumption
policy violation
infrastructure compromise

Conceptual response:

ANOMALY
   ↓
SAFETY POLICY
   ↓
KILL SWITCH
   ↓
ISOLATE
   ↓
PRESERVE EVIDENCE
   ↓
ALERT OPERATOR
   ↓
REBUILD / RECOVER
9. Safety Invariants

The following invariants should remain true:

S1
Production credentials ≠ Deception credentials
S2
Production network ≠ Deception network
S3
Adversarial input ≠ Trusted input
S4
AI conclusion ≠ Ground truth
S5
Detection ≠ Retaliation
S6
Deception compromise ≠ Production compromise
10. Human Oversight

Human operators remain responsible for:

deployment authorization
policy configuration
environment scope
intelligence validation
high-impact defensive actions
incident escalation

VALI should assist defenders rather than remove accountability.

11. Safety Principle

VALI must be designed so that the safest failure mode is containment.
