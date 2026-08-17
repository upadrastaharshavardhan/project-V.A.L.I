VALI Evaluation Framework
1. Purpose

This document defines a research-oriented evaluation framework for measuring VALI.

The goal is not simply to determine whether VALI detects an interaction.

The goal is to determine whether VALI produces useful defensive intelligence safely.

2. Evaluation Dimensions

VALI is evaluated across six dimensions:

                 VALI EVALUATION
                       │
       ┌───────────────┼───────────────┐
       │               │               │
       ▼               ▼               ▼
   Detection      Intelligence       Deception
       │               │               │
       ├───────────────┼───────────────┤
       │               │               │
       ▼               ▼               ▼
     Safety         Analyst Value     Adaptation
3. Detection Metrics
Detection Rate

Measures the percentage of relevant interactions identified.

Detection Rate =
Detected Relevant Events
------------------------
Total Relevant Events
False Positive Rate
False Positive Rate =
Incorrect Alerts
----------------
Total Benign Events
Mean Time to Detection

Measures the time between the beginning of suspicious activity and detection.

MTTD =
Detection Timestamp
-
Activity Start Timestamp

Lower is generally better.

4. Intelligence Metrics
Intelligence Yield

Measures how much actionable intelligence is produced from captured activity.

Intelligence Yield =
Actionable Intelligence
----------------------
Captured Interactions
Evidence Completeness

Measures whether an intelligence conclusion has sufficient supporting evidence.

Dimensions may include:

timestamp
session
interaction
observed behavior
technique
source
correlation
confidence
Correlation Quality

Measures whether related interactions are correctly associated.

Evaluation can consider:

true campaign associations
false associations
missed associations
confidence calibration
5. Deception Metrics
Lure Engagement
Lure Engagement =
Meaningful Interactions
-----------------------
Presented Lures
Interaction Depth

Measures how deeply an adversary interacts with the deception environment.

Possible levels:

Level 1 → Discovery
Level 2 → Service Interaction
Level 3 → Application Interaction
Level 4 → Identity Interaction
Level 5 → Extended Session
Deception Fidelity

Measures whether the environment behaves consistently enough to support meaningful observation.

Potential dimensions:

behavioral consistency
protocol consistency
response realism
workflow consistency
environmental coherence
6. Safety Metrics

Safety is a mandatory evaluation category.

Isolation Integrity

Target:

Unauthorized Production Access = 0
Egress Control

Measure:

unauthorized outbound connections
blocked egress attempts
policy violations
Credential Safety

Target:

Real Production Credentials
Exposed to Deception Zone = 0
Containment Integrity

Measure whether compromised components remain within the intended security boundary.

7. Analyst Metrics

VALI should improve the analyst's ability to understand activity.

Measure:

investigation time
evidence completeness
intelligence clarity
analyst confidence
number of manual investigation steps
usefulness of generated recommendations
8. Adaptive Deception Metrics

For adaptive VALI versions:

Adaptation Latency

Time required to change deception behavior after detecting a new pattern.

Adaptation Accuracy

Whether the new deception policy addresses the observed behavior.

Adaptation Safety

Whether adaptation preserves isolation and policy boundaries.

9. Evaluation Scenarios

A research test suite can contain:

Scenario A
Automated scanning


Scenario B
Service discovery


Scenario C
Credential probing


Scenario D
Application exploration


Scenario E
Repeated sessions


Scenario F
Deception discovery attempt


Scenario G
Egress attempt


Scenario H
Telemetry manipulation attempt


Scenario I
False-intelligence generation


Scenario J
Campaign correlation
10. Experimental Lifecycle
Define Scenario
      ↓
Deploy Controlled Environment
      ↓
Generate Test Activity
      ↓
Capture Telemetry
      ↓
Run VALI Analysis
      ↓
Generate Intelligence
      ↓
Evaluate Against Ground Truth
      ↓
Measure Metrics
      ↓
Analyze Errors
      ↓
Improve Architecture
      ↓
Repeat
11. Ground Truth

Research evaluations should maintain known ground truth whenever possible.

Ground truth may include:

known interaction sequence
known actor identity
known test behavior
known technique
expected campaign relationship
expected risk classification

This allows evaluation of whether VALI correctly inferred the behavior.

12. Research Success Criteria

A successful VALI implementation should demonstrate:

reliable interaction capture
useful behavioral classification
high-quality evidence
meaningful correlation
strong isolation
low false intelligence
reproducible evaluation
measurable analyst value

The objective is not maximum telemetry.

The objective is maximum defensive value from trustworthy telemetry.

research/safety-model.md
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
