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
