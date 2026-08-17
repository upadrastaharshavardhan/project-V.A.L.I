# VALI Threat Model

## 1. Purpose

This document defines the security threat model for **VALI — Vali Adversarial Lure Intelligence**.

The objective is to systematically identify:

* What VALI protects
* What VALI exposes
* Who interacts with VALI
* What adversarial behavior is expected
* What failure modes are possible
* What security boundaries must be enforced
* What controls prevent deception infrastructure from becoming a security liability

VALI assumes that the deception infrastructure itself must be treated as a **high-value security component**.

The threat model therefore follows a fundamental assumption:

> **Anything exposed to adversarial interaction must be treated as potentially discoverable, manipulable, or compromisable.**

---

# 2. Security Objective

The primary security objective is:

> **Capture adversarial intelligence while maintaining strict isolation between deception infrastructure and real production assets.**

### Secondary Objectives

VALI should also:

* Maximize intelligence quality.
* Minimize false intelligence.
* Prevent unauthorized lateral movement.
* Prevent uncontrolled network egress.
* Protect telemetry and evidence.
* Preserve evidence integrity and provenance.
* Maintain analyst trust.
* Prevent deception infrastructure from becoming an attack platform.
* Detect boundary violations quickly.
* Support safe containment and recovery.
* Maintain clear separation between observed facts and analytical conclusions.

---

# 3. Assets

VALI protects several categories of assets.

| Asset                    | Description                                       | Security Priority |
| ------------------------ | ------------------------------------------------- | ----------------- |
| Production Systems       | Real enterprise infrastructure                    | **Critical**      |
| Production Credentials   | Real identities, credentials, and secrets         | **Critical**      |
| Deception Infrastructure | Lures, decoys, and isolated workloads             | **High**          |
| Telemetry                | Captured interaction and behavioral data          | **High**          |
| Intelligence Graph       | Correlated adversarial knowledge                  | **High**          |
| Detection Rules          | Defensive logic derived from intelligence         | **High**          |
| Analyst Environment      | Investigation and analysis interface              | **High**          |
| Synthetic Identities     | Controlled decoy identities                       | **Medium**        |
| Synthetic Data           | Simulated information used by lures               | **Medium**        |
| Configuration            | VALI policies, routing, permissions, and controls | **Critical**      |
| Evidence Store           | Preserved raw and normalized evidence             | **Critical**      |
| Audit Records            | Security and administrative activity records      | **High**          |

Critical assets should have stronger isolation, access controls, monitoring, integrity protection, and recovery mechanisms.

---

# 4. Threat Actors

VALI considers several classes of adversarial actors.

## 4.1 Opportunistic Actor

### Characteristics

* Automated scanning
* Low persistence
* Limited interaction
* Commodity tooling
* Opportunistic exploitation

### Primary Intelligence

* Scanning patterns
* Source behavior
* Automated tooling
* Target-selection behavior
* Initial interaction characteristics

---

## 4.2 Skilled Human Operator

### Characteristics

* Adaptive interaction
* Manual exploration
* Environment discovery
* Repeated sessions
* Behavioral adaptation
* Attempts to understand the environment

### Primary Intelligence

* Behavioral sequences
* Operator methodology
* Decision points
* Interaction strategy
* Persistence behavior
* Intent indicators

---

## 4.3 Automated Campaign

### Characteristics

* High-volume activity
* Repeatable patterns
* Distributed sources
* Automated tooling
* Repeated behavioral signatures

### Primary Intelligence

* Campaign signatures
* Infrastructure relationships
* Timing patterns
* Behavioral clusters
* Tool relationships
* Session correlations

---

## 4.4 Insider or Compromised Identity

### Characteristics

* Legitimate credentials
* Abnormal behavior
* Access from unusual contexts
* Knowledge of internal workflows
* Potential privilege misuse

### Primary Intelligence

* Identity behavior
* Access patterns
* Privilege misuse indicators
* Workflow deviations
* Unusual resource access
* Behavioral anomalies

---

# 5. Threat Categories

VALI models threats across five major categories.

```text
                         THREAT MODEL
                              │
        ┌─────────────────────┼─────────────────────┐
        ▼                     ▼                     ▼
 EXTERNAL THREATS       INTERNAL THREATS     INFRASTRUCTURE
        │                     │                     │
        ├─ Deception          ├─ Analyst Abuse     ├─ Component
        │  Discovery          │                     │  Compromise
        ├─ Deception          ├─ Configuration     ├─ Container
        │  Escape             │  Abuse              │  Escape
        ├─ Credential         ├─ Credential        ├─ Logging
        │  Abuse              │  Exposure           │  Manipulation
        └─ Egress Abuse       └─ Privilege Abuse   └─ Host Compromise
                              │
                              ▼
                     INTELLIGENCE THREATS
                              │
                              ├─ False Attribution
                              ├─ Data Poisoning
                              ├─ Correlation Errors
                              └─ Evidence Manipulation
                              │
                              ▼
                      OPERATIONAL THREATS
                              │
                              ├─ Misconfiguration
                              ├─ Excessive Exposure
                              ├─ Insufficient Isolation
                              └─ Recovery Failure
```

---

# 6. Threat Scenarios

## T01 — Deception Discovery

An adversary determines that the environment is a deception system.

### Potential Impact

* Reduced intelligence value
* Adversary abandonment
* Avoidance of future lures
* Behavioral adaptation
* Increased deception-evasion capability

### Mitigation

* Realistic but synthetic environments
* Controlled fidelity
* Behavioral consistency
* Adaptive lure selection
* Environment-specific deception strategies
* Monitoring for deception-discovery indicators
* Avoiding unnecessary artifacts that reveal the environment

The objective is not to guarantee that deception can never be discovered.

The objective is to ensure that **discovery does not create a security failure**.

---

# 7. T02 — Deception Escape

An adversary attempts to move from the deception environment toward real infrastructure.

### Impact

**Critical**

Potential consequences include:

* Unauthorized access
* Lateral movement
* Credential abuse
* Production compromise
* Data exposure
* Infrastructure disruption

### Mitigation

* Hard network segmentation
* Deny-by-default networking
* Explicit allowlists
* Synthetic credentials
* Controlled egress
* Isolated execution
* Separate management and telemetry planes
* Continuous boundary monitoring
* Least-privilege identities
* Explicit production trust boundaries

The deception environment should never depend on attacker cooperation for containment.

---

# 8. T03 — Credential Exposure

A real credential accidentally appears within a deception environment.

### Impact

**Critical**

Potential consequences include:

* Unauthorized authentication
* Privilege escalation
* Lateral movement
* Production access
* Secret leakage

### Mitigation

* Synthetic identities
* Secret scanning
* Credential allowlists
* Environment-specific secrets
* Automated credential validation
* Pre-deployment secret checks
* Runtime secret monitoring
* Credential rotation procedures
* Explicit separation between production and deception credentials

A core invariant is:

```text
Production Credentials
          ≠
Deception Credentials
```

---

# 9. T04 — Telemetry Manipulation

An adversary attempts to corrupt, manipulate, suppress, or destroy captured evidence.

### Potential Impact

* Loss of investigative evidence
* False conclusions
* Reduced attribution confidence
* Incorrect campaign correlation
* Analyst distrust

### Mitigation

* Append-oriented or tamper-evident logging
* Centralized collection
* Integrity verification
* Restricted log access
* Independent telemetry channels
* Evidence provenance
* Timestamp integrity
* Separation of raw evidence from derived intelligence
* Monitoring for telemetry gaps

The telemetry system must itself be considered part of the security boundary.

---

# 10. T05 — Intelligence Poisoning

An adversary intentionally produces misleading behavior to influence VALI's analytical conclusions.

### Potential Impact

* False attribution
* Incorrect campaign relationships
* Misleading behavioral models
* Incorrect detections
* Analyst misdirection
* Reduced confidence in VALI intelligence

### Mitigation

* Confidence scoring
* Evidence provenance
* Multi-source correlation
* Analyst validation
* Behavioral consistency checks
* Contradictory-evidence detection
* Separation of observation from inference
* Uncertainty representation
* Longitudinal behavioral analysis

A single suspicious observation should not automatically become a high-confidence intelligence conclusion.

---

# 11. T06 — VALI Infrastructure Compromise

An attacker compromises the deception infrastructure itself.

### Potential Impact

* Loss of deception integrity
* Manipulation of telemetry
* Abuse of computing resources
* Credential exposure
* Attempted network escape
* Infrastructure takeover
* Potential use of VALI as an attack platform

### Mitigation

* Minimal privileges
* Immutable or reproducible infrastructure
* Strong isolation
* Hardened hosts
* Sandboxed execution
* Continuous integrity monitoring
* Controlled egress
* Runtime monitoring
* Rapid rebuild capability
* Compromise detection
* Emergency containment mechanisms

The expected assumption should be:

> **A deception component may eventually be compromised. The security architecture must remain safe when that happens.**

---

# 12. Additional Threat Scenarios

## T07 — Analyst Environment Compromise

An attacker attempts to exploit the analyst interface through malicious telemetry or manipulated evidence.

### Mitigation

* Treat telemetry as untrusted content.
* Sanitize rendered data.
* Isolate analyst tooling.
* Restrict execution capabilities.
* Separate viewing from execution.
* Apply strong authentication and authorization.
* Maintain audit trails.

---

## T08 — Configuration Abuse

An unauthorized or incorrectly configured policy expands VALI's exposure.

### Potential Impact

* Excessive network access
* Unsafe lure deployment
* Credential exposure
* Insufficient isolation
* Unauthorized data collection

### Mitigation

* Policy validation
* Configuration review
* Least privilege
* Change approval
* Automated safety checks
* Configuration versioning
* Rollback capability
* Continuous policy compliance monitoring

---

## T09 — Excessive Egress

A deception workload generates unexpected outbound traffic.

### Mitigation

* Default-deny egress
* Explicit destination allowlists
* Egress monitoring
* Rate limits where appropriate
* Network policy enforcement
* Automated containment for policy violations

---

## T10 — Evidence Integrity Failure

Captured evidence becomes incomplete, corrupted, or unverifiable.

### Mitigation

* Integrity metadata
* Append-oriented storage
* Independent collection paths
* Provenance tracking
* Timestamp validation
* Storage redundancy
* Integrity monitoring
* Evidence lifecycle controls

---

# 13. Trust Boundaries

VALI should maintain explicit trust boundaries between external actors, deception infrastructure, analysis environments, and production systems.

```text
                    UNTRUSTED
                        │
                        ▼
              ┌─────────────────┐
              │ EXTERNAL ACTOR  │
              └────────┬────────┘
                       │
                  TRUST BOUNDARY
                       │
                       ▼
              ┌─────────────────┐
              │  VALI GATEWAY   │
              │ Policy / ACL    │
              └────────┬────────┘
                       │
                  TRUST BOUNDARY
                       │
                       ▼
              ┌─────────────────┐
              │ DECEPTION ZONE  │
              │ Lures / Decoys  │
              └────────┬────────┘
                       │
                  TRUST BOUNDARY
                       │
                       ▼
              ┌─────────────────┐
              │  ANALYSIS ZONE  │
              │ Evidence / AI   │
              └────────┬────────┘
                       │
                  TRUST BOUNDARY
                       │
                       ▼
              ┌─────────────────┐
              │   PRODUCTION    │
              │   ENVIRONMENT   │
              └─────────────────┘


              🚫 NO DIRECT TRUST
```

Trust should be established explicitly through controlled interfaces and authorization rather than assumed because systems exist within the same organization.

---

# 14. Security Assumptions

VALI assumes:

* Adversaries are untrusted.
* Deception infrastructure may eventually be discovered.
* Deception workloads may eventually be compromised.
* Captured telemetry may contain hostile input.
* Telemetry may contain misleading or intentionally manipulated information.
* AI-generated conclusions may be incorrect.
* Operators can misconfigure policies.
* Components can fail.
* Network boundaries can be misconfigured.
* Credentials can be exposed accidentally.
* Deception infrastructure must be continuously monitored.
* Recovery mechanisms must be tested before they are needed.
* Production systems must remain outside the deception trust boundary.

These assumptions should influence architecture, implementation, deployment, monitoring, and recovery.

---

# 15. Threat-to-Control Mapping

| Threat                    | Primary Risk                   | Core Controls                                  |
| ------------------------- | ------------------------------ | ---------------------------------------------- |
| Deception Discovery       | Reduced intelligence value     | Fidelity, consistency, adaptive strategies     |
| Deception Escape          | Production compromise          | Segmentation, deny-by-default, egress controls |
| Credential Exposure       | Unauthorized access            | Synthetic credentials, secret scanning         |
| Telemetry Manipulation    | Evidence corruption            | Integrity controls, centralized collection     |
| Intelligence Poisoning    | False intelligence             | Provenance, correlation, confidence scoring    |
| Infrastructure Compromise | VALI becomes attack platform   | Isolation, least privilege, rapid rebuild      |
| Analyst Compromise        | Analyst environment compromise | Sanitization, isolation, restricted execution  |
| Configuration Abuse       | Unsafe exposure                | Policy validation, approval, rollback          |
| Excessive Egress          | External abuse                 | Egress filtering, monitoring                   |
| Evidence Failure          | Loss of investigative value    | Integrity, redundancy, provenance              |

---

# 16. Risk Evaluation Model

VALI can conceptually evaluate threats using:

```text
Risk = Likelihood × Impact
```

However, risk evaluation should also consider:

* Detectability
* Exposure duration
* Existing containment
* Confidence in the assessment
* Recovery capability
* Blast radius

A high-impact threat with strong preventive and containment controls should remain actively monitored even when its estimated likelihood is low.

---

# 17. Threat Detection and Response

The VALI threat lifecycle should follow a continuous defensive loop.

```text
        THREAT
          ↓
      DETECTION
          ↓
       EVIDENCE
          ↓
       ANALYSIS
          ↓
    RISK ASSESSMENT
          ↓
      CONTAINMENT
          ↓
    HUMAN REVIEW
          ↓
     REMEDIATION
          ↓
      RECOVERY
          ↓
   THREAT MODEL UPDATE
          │
          └──────────────► VALI
```

Every significant security event should provide an opportunity to improve the threat model.

---

# 18. Threat Model Principle

The central VALI threat-model principle is:

> **Assume the lure will eventually be discovered. Design the system so that discovery does not compromise the real environment.**

This principle extends beyond deception discovery.

VALI should assume that:

```text
Lure may be discovered
        ↓
Lure may be manipulated
        ↓
Telemetry may be attacked
        ↓
Infrastructure may be compromised
        ↓
AI may be wrong
        ↓
Operator may make mistakes
```

The architecture must remain secure despite these possibilities.

---

# 19. Final Security Principle

VALI is successful only when it can extract meaningful adversarial intelligence **without increasing the security risk of the environment it protects**.

The desired security model is:

```text
              ADVERSARIAL ACTIVITY
                       ↓
                  VALI EXPOSURE
                       ↓
                    OBSERVE
                       ↓
                    CAPTURE
                       ↓
                   VALIDATE
                       ↓
                  CORRELATE
                       ↓
                 INTELLIGENCE
                       ↓
               DEFENSIVE VALUE
                       │
                       ▼
             ┌──────────────────┐
             │ SECURITY BOUNDARY│
             └────────┬─────────┘
                      │
             COMPROMISE / FAILURE
                      │
                      ▼
                 CONTAINMENT
                      │
                      ▼
                SAFE RECOVERY
```

The ultimate objective of the VALI threat model is therefore:

> **Understand adversarial behavior without allowing adversarial interaction to cross trusted security boundaries.**

VALI should treat deception as an intentionally exposed security surface, design for its eventual discovery or compromise, preserve the integrity of the resulting intelligence, and ensure that the worst credible failure remains **contained, observable, recoverable, and isolated from production systems**.
