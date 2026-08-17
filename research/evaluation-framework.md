# VALI Evaluation Framework

## Research-Grade Evaluation, Metrics, Experimental Methodology & Validation Protocol

> **VALI should not be evaluated by how much activity it captures.
> VALI should be evaluated by how much trustworthy defensive intelligence it produces — safely, reproducibly, and measurably.**

---

# 1. Purpose

This document defines the formal evaluation framework for:

**VALI — Vali Adversarial Lure Intelligence**

The framework is designed to evaluate VALI across six primary dimensions:

1. **Detection**
2. **Intelligence**
3. **Deception**
4. **Safety**
5. **Analyst Value**
6. **Adaptation**

The framework is intentionally broader than conventional security detection benchmarking.

A system can generate millions of events and still provide little defensive value.

Therefore VALI evaluates the complete transformation:

```text
Adversarial Activity
        ↓
Interaction Capture
        ↓
Telemetry
        ↓
Behavior Understanding
        ↓
Evidence
        ↓
Intelligence
        ↓
Defensive Decision
        ↓
Measurable Defensive Value
```

The evaluation objective is:

> **Measure whether VALI converts adversarial interaction into reliable, actionable, evidence-backed defensive intelligence while maintaining strict safety boundaries.**

---

# 2. Evaluation Philosophy

VALI follows five fundamental evaluation principles.

## 2.1 Detection Is Not Intelligence

Detecting an event does not automatically mean understanding it.

```text
Event Detected
      ≠
Behavior Understood
      ≠
Intelligence Produced
```

---

## 2.2 More Telemetry Is Not Necessarily Better

A system producing more logs may actually increase analyst workload.

Therefore:

```text
Telemetry Volume
        ↓
Evidence Quality
        ↓
Intelligence Quality
        ↓
Defensive Value
```

is more important than raw event count.

---

## 2.3 Safety Is a Hard Constraint

Safety cannot be traded for intelligence.

The optimization objective is therefore:

```text
MAXIMIZE
Defensive Intelligence Value

SUBJECT TO

Production Isolation = 100%
Credential Exposure = 0
Unauthorized Egress = 0
Containment Failure = 0
```

---

## 2.4 Ground Truth Matters

Whenever possible, every evaluation scenario should have a known expected outcome.

Without ground truth, detection and intelligence claims become difficult to validate.

---

## 2.5 Reproducibility Matters

Every experiment should be reproducible using:

* identical scenario definitions
* controlled environments
* fixed configurations
* versioned datasets
* versioned VALI releases
* documented parameters
* repeatable execution procedures

---

# 3. Evaluation Architecture

The VALI evaluation system consists of several layers.

```text
┌─────────────────────────────────────────────────────────┐
│                  EVALUATION CONTROLLER                  │
│                                                         │
│ Scenario Selection • Configuration • Experiment Control │
└───────────────────────────┬─────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────┐
│                   CONTROLLED ENVIRONMENT                │
│                                                         │
│ Lures • Decoys • Synthetic Identities • Applications    │
└───────────────────────────┬─────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────┐
│                    TEST ACTIVITY                        │
│                                                         │
│ Synthetic / Authorized Adversarial Behavior             │
└───────────────────────────┬─────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────┐
│                    VALI PLATFORM                        │
│                                                         │
│ Capture → Analyze → Correlate → Intelligence             │
└───────────────────────────┬─────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────┐
│                     GROUND TRUTH                        │
│                                                         │
│ Expected Actor • Behavior • Technique • Campaign        │
└───────────────────────────┬─────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────┐
│                    EVALUATION ENGINE                     │
│                                                         │
│ Metrics • Statistical Analysis • Error Analysis         │
└───────────────────────────┬─────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────┐
│                    RESULT REPORT                         │
│                                                         │
│ Detection • Intelligence • Deception • Safety           │
│ Analyst Value • Adaptation • Overall Defensive Value    │
└─────────────────────────────────────────────────────────┘
```

---

# 4. Evaluation Dimensions

VALI is evaluated across six dimensions.

```text
                         VALI EVALUATION
                                │
        ┌───────────────────────┼────────────────────────┐
        │                       │                        │
        ▼                       ▼                        ▼
   DETECTION              INTELLIGENCE              DECEPTION
        │                       │                        │
        │                       │                        │
        ├───────────────────────┼────────────────────────┤
        │                       │                        │
        ▼                       ▼                        ▼
     SAFETY               ANALYST VALUE             ADAPTATION
```

---

# 5. Dimension 1 — Detection

Detection evaluates whether VALI correctly identifies relevant activity.

---

## 5.1 Detection Rate

Measures the percentage of relevant events detected.

```text
Detection Rate =
True Positive Events
────────────────────
All Relevant Events
```

Range:

```text
0 ≤ Detection Rate ≤ 1
```

or:

```text
0% ≤ Detection Rate ≤ 100%
```

Higher is generally better.

---

## 5.2 Precision

Measures how many VALI alerts are actually relevant.

```text
Precision =
True Positive Alerts
─────────────────────
All Positive Alerts
```

High precision indicates lower alert noise.

---

## 5.3 Recall

```text
Recall =
True Positive Events
────────────────────
True Positive + Missed Events
```

Recall is equivalent to detection coverage in scenarios where ground truth is complete.

---

## 5.4 F1 Score

Balances precision and recall.

```text
F1 =
2 × Precision × Recall
──────────────────────
Precision + Recall
```

F1 is useful when both false positives and missed activity matter.

---

## 5.5 False Positive Rate

```text
FPR =
False Positive Events
──────────────────────
All Benign Events
```

Lower is better.

---

## 5.6 False Negative Rate

```text
FNR =
Missed Relevant Events
───────────────────────
All Relevant Events
```

Lower is better.

---

# 6. Mean Time to Detection

MTTD measures how quickly VALI recognizes suspicious activity.

```text
MTTD =
Σ(Detection Time - Activity Start Time)
──────────────────────────────────────
Number of Detected Activities
```

Lower is generally better.

---

## 6.1 Detection Latency Distribution

Average MTTD alone may hide important behavior.

Therefore record:

* minimum
* median
* mean
* P50
* P90
* P95
* P99
* maximum

Example:

```text
P50 = 2.1 sec
P90 = 5.7 sec
P95 = 8.4 sec
P99 = 15.2 sec
```

This provides a more realistic understanding of detection performance.

---

# 7. Detection Coverage

VALI should measure coverage across different behavior categories.

```text
Coverage =
Observed Behavior Categories
─────────────────────────────
Total Test Behavior Categories
```

Example:

| Behavior                | Detected |
| ----------------------- | -------: |
| Discovery               |        ✅ |
| Service interaction     |        ✅ |
| Identity probing        |        ✅ |
| Application exploration |        ✅ |
| Repeated sessions       |        ✅ |
| Deception discovery     |       ⚠️ |
| Egress attempt          |        ✅ |

---

# 8. Detection Quality Matrix

Each evaluation run should generate a confusion matrix.

```text
                         ACTUAL
                  Relevant    Benign
                ┌───────────┬───────────┐
Predicted       │           │           │
Relevant        │    TP     │    FP     │
                ├───────────┼───────────┤
Benign          │    FN     │    TN     │
                └───────────┴───────────┘
```

This enables calculation of:

* precision
* recall
* F1
* false-positive rate
* false-negative rate
* specificity
* balanced accuracy

---

# 9. Dimension 2 — Intelligence

Detection answers:

> "Did VALI notice something?"

Intelligence evaluation asks:

> **"Did VALI understand what happened well enough to be useful?"**

---

# 10. Intelligence Yield

Measures the amount of useful intelligence produced from captured activity.

```text
Intelligence Yield =
Actionable Intelligence Units
──────────────────────────────
Captured Interaction Units
```

An intelligence unit may represent:

* validated behavior
* technique identification
* campaign association
* intent hypothesis
* useful defensive indicator
* detection recommendation

---

# 11. Intelligence Quality

Each generated intelligence object can be evaluated across:

```text
Accuracy
Evidence Support
Completeness
Confidence
Relevance
Actionability
Novelty
```

A conceptual intelligence quality score:

```text
IQ =
Accuracy
× Evidence Support
× Relevance
× Actionability
```

The exact implementation should be versioned and documented rather than treated as a universal security standard.

---

# 12. Evidence Completeness

Every intelligence conclusion should be traceable to evidence.

Minimum evidence dimensions:

* timestamp
* session identifier
* source
* interaction
* observed behavior
* affected lure
* technique classification
* correlation information
* confidence
* provenance

---

## 12.1 Evidence Completeness Score

```text
Evidence Completeness =
Available Required Evidence
───────────────────────────
Total Required Evidence
```

Example:

```text
Required Evidence = 10
Available Evidence = 9

Evidence Completeness = 90%
```

---

# 13. Evidence Provenance

Every intelligence claim should be traceable.

```text
INTELLIGENCE
     │
     ▼
HYPOTHESIS
     │
     ▼
CORRELATED EVENTS
     │
     ▼
RAW TELEMETRY
     │
     ▼
ORIGINAL INTERACTION
```

This enables analysts to answer:

> **"Why does VALI believe this?"**

---

# 14. Intelligence Confidence

VALI should distinguish:

```text
Observed Fact
     ↓
Derived Behavior
     ↓
Inferred Intent
     ↓
Campaign Hypothesis
```

Confidence should generally decrease as inference moves farther from directly observed evidence.

Example:

| Intelligence Layer   | Confidence |
| -------------------- | ---------: |
| Event observed       |       0.99 |
| Behavior classified  |       0.94 |
| Technique inferred   |       0.88 |
| Intent inferred      |       0.76 |
| Campaign attribution |       0.61 |

These values are illustrative rather than normative.

---

# 15. Confidence Calibration

A system should not merely produce confidence scores.

The scores should be calibrated against actual outcomes.

Useful measures include:

* calibration curves
* Brier score
* expected calibration error
* reliability diagrams

The objective is:

> **A confidence score of 0.8 should correspond approximately to an 80% likelihood of correctness over comparable evaluated cases.**

---

# 16. Correlation Quality

Campaign correlation evaluates whether related interactions are correctly grouped.

Metrics:

```text
True Associations
False Associations
Missed Associations
Correctly Separated Sessions
```

Possible evaluation measures include:

* precision
* recall
* F1
* pairwise accuracy
* clustering purity
* adjusted Rand index

---

# 17. Intelligence Novelty

Not every intelligence object provides new information.

Define:

```text
Novel Intelligence =
Previously Unknown Useful Intelligence
```

A conceptual novelty score:

```text
Novelty =
New Information
────────────────
Total Intelligence
```

This helps distinguish:

```text
Repeated Event
      vs
New Defensive Knowledge
```

---

# 18. Intelligence Actionability

An intelligence item is more valuable if a defender can act on it.

Possible categories:

```text
0 → Informational
1 → Investigative
2 → Detection Opportunity
3 → Hunting Opportunity
4 → Hardening Recommendation
5 → Immediate Defensive Value
```

---

# 19. Dimension 3 — Deception

Deception evaluation measures whether VALI successfully attracts, retains and meaningfully observes interaction.

---

# 20. Lure Engagement

```text
Lure Engagement =
Meaningful Lure Interactions
────────────────────────────
Presented Lures
```

---

# 21. Interaction Depth

VALI can classify interaction depth:

```text
LEVEL 0
No Interaction
    ↓
LEVEL 1
Discovery
    ↓
LEVEL 2
Service Interaction
    ↓
LEVEL 3
Application Interaction
    ↓
LEVEL 4
Identity / Workflow Interaction
    ↓
LEVEL 5
Extended Interaction
```

---

# 22. Session Depth Score

A simple normalized measure:

```text
Session Depth =
Observed Interaction Level
──────────────────────────
Maximum Supported Level
```

---

# 23. Dwell Time

Measures how long an interaction remains active inside the deception environment.

```text
Dwell Time =
Session End
-
Session Start
```

Measure:

* median
* mean
* P90
* P95
* maximum

Longer dwell time is not automatically better.

It is useful only when it produces meaningful intelligence without increasing risk.

---

# 24. Deception Fidelity

Deception fidelity measures how consistently the environment behaves as intended.

Dimensions:

### Behavioral Consistency

Do related operations produce consistent responses?

### Protocol Consistency

Do interfaces behave according to expected protocol semantics?

### Workflow Consistency

Do multi-step interactions behave coherently?

### Environmental Coherence

Do the different parts of the environment appear logically related?

### Response Realism

Do responses remain sufficiently realistic for the evaluation objective?

---

# 25. Deception Discovery Resistance

VALI should evaluate how easily a controlled test actor can identify the environment as deceptive.

Possible measurements:

```text
Discovery Rate
Time to Discovery
Interactions Before Discovery
False Discovery Rate
```

A lower discovery rate may indicate stronger deception, but should never be optimized at the expense of safety.

---

# 26. Dimension 4 — Safety

Safety is a **hard evaluation dimension**.

A system cannot compensate for safety failures with better intelligence.

---

# 27. Isolation Integrity

Primary invariant:

```text
Unauthorized Production Access = 0
```

Any confirmed unauthorized production access should be classified as a critical evaluation failure.

---

# 28. Egress Safety

Measure:

* attempted unauthorized connections
* blocked outbound connections
* successful unauthorized connections
* policy violations

Primary target:

```text
Unauthorized Successful Egress = 0
```

---

# 29. Credential Safety

Primary invariant:

```text
Real Production Credentials
Exposed to Deception Environment = 0
```

Evaluation should include:

* accidental credential exposure
* credential discovery
* credential reuse attempts
* secret scanning
* synthetic credential separation

---

# 30. Containment Integrity

A compromised deception component should remain within its assigned security boundary.

Evaluate:

```text
Component Compromise
        ↓
Isolation Boundary
        ↓
Containment
```

A successful escape is a critical safety failure.

---

# 31. Telemetry Integrity

Evaluate whether captured evidence can be:

* modified
* deleted
* reordered
* duplicated
* forged

Useful controls include:

* immutable storage
* integrity hashes
* append-only logging
* timestamps
* provenance identifiers

---

# 32. Safety Failure Classification

| Severity | Example                                     |
| -------- | ------------------------------------------- |
| **S0**   | No safety issue                             |
| **S1**   | Minor policy deviation                      |
| **S2**   | Non-critical configuration issue            |
| **S3**   | Significant containment weakness            |
| **S4**   | Confirmed deception boundary violation      |
| **S5**   | Production compromise / unauthorized access |

The target for production-impacting failures is:

```text
S4 = 0
S5 = 0
```

---

# 33. Dimension 5 — Analyst Value

VALI should reduce the cognitive and operational burden on defenders.

---

# 34. Investigation Time

Measure:

```text
Baseline Investigation Time
vs
VALI-Assisted Investigation Time
```

Improvement:

```text
Investigation Improvement =
Baseline Time - VALI Time
──────────────────────────
Baseline Time
```

---

# 35. Evidence Retrieval Efficiency

Measure the number of steps required to answer:

* What happened?
* When did it happen?
* Which session was involved?
* What behavior was observed?
* What technique was involved?
* Is it related to another campaign?
* What should the defender investigate next?

---

# 36. Analyst Accuracy

Compare analyst conclusions:

```text
Without VALI
      vs
With VALI
```

Metrics:

* correct classification
* correct correlation
* correct prioritization
* correct recommended action

---

# 37. Analyst Confidence

Analysts may rate:

* clarity
* evidence quality
* trustworthiness
* usefulness
* confidence in conclusion

A standardized scale can be used:

```text
1 = Very Low
2 = Low
3 = Moderate
4 = High
5 = Very High
```

---

# 38. Recommendation Usefulness

Each VALI recommendation can be classified:

```text
Useful
Partially Useful
Not Useful
Incorrect
Unsafe
```

Any unsafe recommendation should trigger additional review.

---

# 39. Dimension 6 — Adaptation

Adaptation applies primarily to advanced VALI versions.

---

# 40. Adaptation Latency

Measures the time between detecting a new behavior and deploying the corresponding approved deception adaptation.

```text
Adaptation Latency =
Policy Activation Time
-
Behavior Detection Time
```

---

# 41. Adaptation Accuracy

Measures whether the adaptation actually addresses the observed behavior.

```text
Adaptation Accuracy =
Successful Relevant Adaptations
───────────────────────────────
Total Adaptation Decisions
```

---

# 42. Adaptation Safety

Every adaptation must preserve:

```text
Isolation
Credential Safety
Network Policy
Access Policy
Auditability
```

A more effective lure is not acceptable if it weakens security boundaries.

---

# 43. Adaptation Stability

A future VALI implementation should also evaluate whether adaptive behavior causes:

* oscillation
* unstable policies
* unnecessary lure changes
* resource exhaustion
* inconsistent deception

The objective is controlled adaptation, not constant change.

---

# 44. Evaluation Scenarios

A comprehensive VALI evaluation suite should include at least the following scenario families.

---

## Scenario A — Automated Scanning

Purpose:

Evaluate basic detection and telemetry capture.

Measure:

* detection rate
* latency
* source identification
* session creation
* telemetry completeness

---

## Scenario B — Service Discovery

Purpose:

Evaluate service-level interaction detection.

Measure:

* discovery coverage
* protocol telemetry
* behavior classification
* evidence completeness

---

## Scenario C — Credential Probing

Purpose:

Evaluate identity deception and credential telemetry.

Measure:

* interaction detection
* synthetic credential usage
* credential safety
* intent classification

---

## Scenario D — Application Exploration

Purpose:

Evaluate application-level deception.

Measure:

* workflow depth
* application interaction
* sequence reconstruction
* deception fidelity

---

## Scenario E — Repeated Sessions

Purpose:

Evaluate persistent behavioral correlation.

Measure:

* session linking
* behavioral similarity
* campaign correlation
* confidence

---

## Scenario F — Deception Discovery Attempt

Purpose:

Evaluate whether controlled test actors can identify deception.

Measure:

* discovery time
* discovery indicators
* interaction depth
* intelligence generated before discovery

---

## Scenario G — Egress Attempt

Purpose:

Evaluate containment.

Measure:

* attempted egress
* blocked egress
* successful egress
* alert generation
* containment integrity

Expected:

```text
Successful Unauthorized Egress = 0
```

---

## Scenario H — Telemetry Manipulation

Purpose:

Evaluate evidence integrity.

Measure:

* tampering detection
* log integrity
* provenance preservation
* recovery

---

## Scenario I — False-Intelligence Generation

Purpose:

Evaluate resistance to misleading behavior.

Measure:

* incorrect classification
* false correlation
* confidence calibration
* analyst correction

---

## Scenario J — Campaign Correlation

Purpose:

Evaluate cross-session intelligence.

Measure:

* correct associations
* false associations
* missed associations
* campaign confidence

---

## Scenario K — Benign Activity

Purpose:

Evaluate false positives.

Measure:

* false-positive rate
* alert noise
* benign classification accuracy

---

## Scenario L — Mixed Activity

Combine:

```text
Benign Activity
+
Automated Activity
+
Human-Like Activity
+
Repeated Sessions
```

Purpose:

Evaluate VALI under realistic mixed conditions.

---

# 45. Experimental Lifecycle

Every evaluation should follow a controlled lifecycle.

```text
                    DEFINE
                       │
                       ▼
                Test Scenario
                       │
                       ▼
                  Establish
                 Ground Truth
                       │
                       ▼
                Deploy Controlled
                  Environment
                       │
                       ▼
                Generate Test
                    Activity
                       │
                       ▼
                Capture VALI
                   Telemetry
                       │
                       ▼
                 Run Analysis
                       │
                       ▼
               Generate Intelligence
                       │
                       ▼
               Compare Against
                 Ground Truth
                       │
                       ▼
                 Calculate Metrics
                       │
                       ▼
                Statistical Analysis
                       │
                       ▼
                  Error Analysis
                       │
                       ▼
                Architecture Change
                       │
                       ▼
                  Re-run Test
                       │
                       └──────────────►
```

---

# 46. Ground Truth Model

Ground truth should be defined before the experiment whenever possible.

A scenario's ground truth may contain:

```json
{
  "scenario": "campaign-correlation-001",
  "actor": "synthetic-actor-01",
  "sessions": [
    "session-a",
    "session-b",
    "session-c"
  ],
  "expected_behaviors": [
    "discovery",
    "service-interaction",
    "identity-probing"
  ],
  "expected_relationships": [
    "session-a ↔ session-b",
    "session-b ↔ session-c"
  ],
  "expected_risk": "high"
}
```

---

# 47. Ground Truth Layers

Ground truth should be hierarchical.

```text
GROUND TRUTH
     │
     ├── Actor
     │
     ├── Source
     │
     ├── Session
     │
     ├── Interaction
     │
     ├── Behavior
     │
     ├── Technique
     │
     ├── Intent
     │
     ├── Campaign
     │
     └── Risk
```

This allows evaluation at multiple levels.

---

# 48. Baseline Comparisons

VALI should be compared against appropriate baselines.

Potential baselines:

### Baseline A

Traditional logging without deception.

### Baseline B

Static deception without intelligence correlation.

### Baseline C

Deception + basic telemetry.

### Baseline D

VALI without adaptive components.

### Baseline E

Full VALI.

Example:

```text
Baseline
   ↓
Static Deception
   ↓
Telemetry Deception
   ↓
Correlated Deception
   ↓
VALI
   ↓
Adaptive VALI
```

This allows researchers to determine which architectural capabilities actually provide measurable benefit.

---

# 49. Ablation Studies

Ablation testing should determine whether individual VALI components contribute meaningful value.

Potential experiments:

```text
Full VALI

Full VALI - Intelligence Graph

Full VALI - Campaign Correlation

Full VALI - Behavioral Profiling

Full VALI - Adaptive Deception

Full VALI - AI Analysis
```

Compare:

* intelligence yield
* correlation quality
* analyst value
* latency
* safety
* resource consumption

---

# 50. Statistical Evaluation

Where sufficient repeated experiments exist, report:

* sample size
* mean
* median
* standard deviation
* confidence interval
* percentile distribution
* effect size

Avoid reporting only a single average.

Example:

```text
MTTD

Mean:   4.8 sec
Median: 3.9 sec
P95:    11.7 sec
P99:    19.4 sec
n:      500
```

---

# 51. Statistical Significance

When comparing VALI against a baseline, appropriate statistical tests should be selected based on:

* metric distribution
* sample size
* paired vs unpaired observations
* categorical vs continuous variables

Possible methods include:

* paired t-test
* Mann–Whitney U
* Wilcoxon signed-rank
* chi-square
* bootstrap confidence intervals

Statistical significance should not replace practical significance.

---

# 52. Practical Significance

A statistically significant improvement may still be operationally irrelevant.

Therefore report both:

```text
Statistical Significance
+
Operational Significance
```

Example:

```text
Detection latency improved by 2%

Statistically significant: Yes
Operationally meaningful: Possibly No
```

---

# 53. Resource Efficiency

VALI should also measure operational cost.

Metrics:

* CPU utilization
* memory utilization
* storage consumption
* network overhead
* telemetry volume
* processing latency
* analysis cost
* AI inference cost where applicable

---

# 54. Intelligence Efficiency

A useful higher-level metric is:

```text
Intelligence Efficiency =
Actionable Intelligence
────────────────────────
Resource Cost
```

This helps compare architectures that produce different amounts of telemetry.

---

# 55. Defensive Value Index

VALI may use a composite research metric to summarize overall performance.

A conceptual model:

```text
DVI =
w₁ Detection
+
w₂ Intelligence
+
w₃ Deception
+
w₄ Analyst Value
+
w₅ Adaptation
```

subject to:

```text
Safety Constraints
```

Where:

```text
w₁ + w₂ + w₃ + w₄ + w₅ = 1
```

The weights should be explicitly documented for each experiment.

Safety should **not** simply be another weighted score.

It should function as a gate.

```text
IF Safety Failure
THEN
Evaluation = FAILED
```

for failures that violate critical safety invariants.

---

# 56. VALI Evaluation Scorecard

| Dimension     | Primary Metrics                        | Desired Direction        |
| ------------- | -------------------------------------- | ------------------------ |
| Detection     | Recall, Precision, F1, MTTD            | Higher / Lower latency   |
| Intelligence  | Yield, Accuracy, Completeness          | Higher                   |
| Correlation   | Precision, Recall, F1                  | Higher                   |
| Deception     | Engagement, Depth, Fidelity            | Higher                   |
| Safety        | Isolation, Egress, Credential Exposure | Zero violations          |
| Analyst Value | Investigation Time, Accuracy           | Faster / Higher          |
| Adaptation    | Latency, Accuracy, Stability           | Faster / Higher / Stable |
| Efficiency    | Resource Cost / Intelligence           | Higher efficiency        |

---

# 57. V1–V10 Evaluation Matrix

Each VALI generation should introduce measurable capabilities.

| Version | Primary Capability  | Primary Evaluation         |
| ------- | ------------------- | -------------------------- |
| V1      | Basic deception     | Capture rate               |
| V2      | Telemetry           | Evidence completeness      |
| V3      | Profiling           | Behavior classification    |
| V4      | Risk                | Risk accuracy              |
| V5      | Orchestration       | Lure effectiveness         |
| V6      | Correlation         | Campaign correlation       |
| V7      | Intelligence Graph  | Relationship accuracy      |
| V8      | Adaptation          | Adaptation latency         |
| V9      | AI Intelligence     | Intelligence quality       |
| V10     | Intelligence Fabric | End-to-end defensive value |

---

# 58. Failure Taxonomy

Evaluation failures should be classified rather than simply marked as "failed."

```text
F1 — Detection Failure
F2 — Classification Failure
F3 — Correlation Failure
F4 — Evidence Failure
F5 — Intelligence Failure
F6 — Deception Failure
F7 — Analyst Usability Failure
F8 — Adaptation Failure
F9 — Performance Failure
F10 — Safety Failure
```

Safety failures receive the highest severity.

---

# 59. Error Analysis

Every failed scenario should answer:

1. What happened?
2. What did VALI predict?
3. What was the expected result?
4. Why was the prediction wrong?
5. Which component failed?
6. Was evidence missing?
7. Was correlation incorrect?
8. Was confidence miscalibrated?
9. Could the failure affect production safety?
10. What architectural change should address it?

---

# 60. Reproducibility Requirements

Every published evaluation should document:

### Environment

* operating system
* compute resources
* network topology
* deployment configuration

### VALI

* version
* commit identifier
* configuration
* enabled modules

### Dataset

* scenario identifiers
* dataset version
* sample size

### Experiment

* execution timestamp
* random seed where applicable
* number of repetitions
* test parameters

### Results

* raw results
* processed metrics
* statistical analysis
* known limitations

---

# 61. Evaluation Artifact Structure

A recommended evaluation repository structure:

```text
evaluation/
│
├── scenarios/
│   ├── automated-scanning/
│   ├── service-discovery/
│   ├── credential-probing/
│   ├── application-exploration/
│   ├── repeated-sessions/
│   ├── deception-discovery/
│   ├── egress-attempt/
│   ├── telemetry-manipulation/
│   ├── false-intelligence/
│   └── campaign-correlation/
│
├── datasets/
│
├── ground-truth/
│
├── baselines/
│
├── experiments/
│
├── results/
│
├── reports/
│
└── methodology/
```

---

# 62. Recommended Evaluation Report

Every evaluation run should produce a report containing:

```text
1. Executive Summary
2. Environment
3. VALI Version
4. Scenario Definition
5. Ground Truth
6. Configuration
7. Dataset
8. Detection Results
9. Intelligence Results
10. Deception Results
11. Safety Results
12. Analyst Results
13. Adaptation Results
14. Resource Usage
15. Baseline Comparison
16. Statistical Analysis
17. Error Analysis
18. Limitations
19. Recommendations
20. Reproducibility Information
```

---

# 63. Example Evaluation Summary

```text
========================================================
                 VALI EVALUATION REPORT
========================================================

VALI VERSION: V7
SCENARIO: Campaign Correlation
RUNS: 500

--------------------------------------------------------
DETECTION
--------------------------------------------------------
Recall                 : 96.4%
Precision              : 94.8%
F1                     : 95.6%
Median MTTD            : 3.2 sec
P95 MTTD               : 8.7 sec

--------------------------------------------------------
INTELLIGENCE
--------------------------------------------------------
Evidence Completeness : 94.1%
Correlation Precision  : 92.8%
Correlation Recall     : 89.7%
Intelligence Yield     : 0.74
Novel Intelligence     : 61.2%

--------------------------------------------------------
DECEPTION
--------------------------------------------------------
Lure Engagement        : 82.4%
Median Interaction     : Level 3
Deception Fidelity     : 91.3%

--------------------------------------------------------
SAFETY
--------------------------------------------------------
Production Access      : 0
Unauthorized Egress    : 0
Credential Exposure    : 0
Containment Failures   : 0

--------------------------------------------------------
ANALYST VALUE
--------------------------------------------------------
Investigation Time     : -42%
Manual Steps           : -51%
Analyst Accuracy       : +28%

--------------------------------------------------------
OVERALL
--------------------------------------------------------
Safety Gate            : PASS
Evaluation Status      : PASS
========================================================
```

> The numbers above are **illustrative only** and must not be presented as actual VALI benchmark results unless experimentally measured.

---

# 64. Minimum Acceptance Criteria

A VALI release should not be considered evaluation-ready unless it can demonstrate:

```text
✓ Controlled deployment
✓ Defined ground truth
✓ Repeatable scenarios
✓ Reliable telemetry
✓ Evidence provenance
✓ Measurable detection
✓ Measurable intelligence
✓ Safety validation
✓ Error analysis
✓ Reproducible results
```

For security-critical evaluation:

```text
Unauthorized Production Access = 0
Unauthorized Successful Egress = 0
Real Credential Exposure = 0
Critical Containment Failure = 0
```

---

# 65. Research Limitations

VALI evaluation results should explicitly acknowledge limitations.

Potential limitations include:

* laboratory environments may not represent production environments
* synthetic behavior may differ from real adversarial behavior
* ground truth may be incomplete
* deception fidelity is difficult to measure objectively
* campaign attribution may contain uncertainty
* AI conclusions may be probabilistic
* analyst studies may contain human bias
* evaluation datasets may not represent the full threat landscape

Therefore:

> **A successful laboratory evaluation does not automatically imply production security effectiveness.**

---

# 66. Benchmarking Principle

VALI should not be benchmarked only against:

```text
"How many attacks did it detect?"
```

Instead evaluate:

```text
How much trustworthy intelligence
did VALI produce?

How quickly?

With what evidence?

At what operational cost?

And with what safety guarantees?
```

---

# 67. Complete VALI Evaluation Model

The complete evaluation lifecycle can be summarized as:

```text
                       ADVERSARIAL ACTIVITY
                                │
                                ▼
                         DECEPTION LAYER
                                │
                                ▼
                           TELEMETRY
                                │
                                ▼
                        BEHAVIOR ANALYSIS
                                │
                                ▼
                         EVIDENCE MODEL
                                │
                                ▼
                       INTELLIGENCE MODEL
                                │
                 ┌──────────────┼──────────────┐
                 ▼              ▼              ▼
             DETECTION      CORRELATION     DECEPTION
                 │              │              │
                 └──────────────┼──────────────┘
                                ▼
                         DEFENSIVE VALUE
                                │
                 ┌──────────────┼──────────────┐
                 ▼              ▼              ▼
              ANALYST        ADAPTATION       SAFETY
                 │              │              │
                 └──────────────┼──────────────┘
                                ▼
                         EVALUATION ENGINE
                                │
                                ▼
                       GROUND TRUTH COMPARISON
                                │
                                ▼
                       STATISTICAL ANALYSIS
                                │
                                ▼
                          ERROR ANALYSIS
                                │
                                ▼
                       ARCHITECTURE IMPROVEMENT
                                │
                                └──────────────► REPEAT
```

---

# 68. Final Evaluation Principle

The ultimate objective of VALI evaluation is not:

> **Maximum telemetry.**

It is not:

> **Maximum attacker interaction.**

It is not even:

> **Maximum detection rate.**

The ultimate objective is:

> ## **Maximum trustworthy defensive value from adversarial interaction under strict safety constraints.**

The complete VALI evaluation equation can therefore be expressed conceptually as:

```text
                 TRUSTWORTHY
                 INTELLIGENCE
                      │
                      ▼
              ┌───────────────┐
              │   VALI VALUE  │
              └───────┬───────┘
                      ▲
                      │
        ┌─────────────┼─────────────┐
        │             │             │
        ▼             ▼             ▼
    Detection    Intelligence   Deception
        │             │             │
        └─────────────┼─────────────┘
                      │
                      ▼
               Analyst Value
                      │
                      ▼
                  Adaptation

                      │
                      │
                HARD CONSTRAINT
                      │
                      ▼
               ┌────────────┐
               │   SAFETY   │
               └────────────┘
```

And the core principle remains:

# **Measure the intelligence. Prove the evidence. Validate the safety.**

> **Attackers spend. Defenders learn.
> VALI must prove that the learning is accurate, useful, reproducible, and safe.**
