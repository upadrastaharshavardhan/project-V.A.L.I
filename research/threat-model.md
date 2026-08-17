VALI Threat Model
1. Purpose

This document defines the security threat model for VALI — Vali Adversarial Lure Intelligence.

The objective is to identify:

what VALI protects
what VALI exposes
who interacts with VALI
what adversarial behavior is expected
what failure modes are possible
what controls prevent deception infrastructure from becoming a security liability

VALI assumes that deception infrastructure itself must be treated as a high-value security component.

2. Security Objective

The primary objective is:

Capture adversarial intelligence while maintaining strict isolation between deception infrastructure and real production assets.

Secondary objectives include:

maximize intelligence quality
minimize false intelligence
prevent unauthorized lateral movement
prevent uncontrolled egress
protect telemetry
preserve evidence integrity
maintain analyst trust
prevent deception infrastructure from becoming an attack platform
3. Assets

VALI protects several categories of assets.

Asset	Description	Security Priority
Production systems	Real enterprise infrastructure	Critical
Production credentials	Real identities and secrets	Critical
Deception infrastructure	Lures and decoys	High
Telemetry	Captured interaction data	High
Intelligence graph	Correlated adversarial knowledge	High
Detection rules	Defensive logic generated from intelligence	High
Analyst environment	Investigation interface	High
Synthetic identities	Controlled decoy identities	Medium
Synthetic data	Fake information used by lures	Medium
Configuration	VALI policy and routing	Critical
4. Threat Actors

VALI considers several classes of adversarial actors.

4.1 Opportunistic Actor

Characteristics:

automated scanning
low persistence
limited interaction
commodity tooling

Primary intelligence:

scanning patterns
source behavior
automated tooling
4.2 Skilled Human Operator

Characteristics:

adaptive interaction
manual exploration
environment discovery
repeated sessions

Primary intelligence:

behavioral sequence
operator methodology
decision points
intent
4.3 Automated Campaign

Characteristics:

high-volume activity
repeatable patterns
distributed sources
automated tooling

Primary intelligence:

campaign signatures
infrastructure relationships
timing patterns
behavioral clusters
4.4 Insider or Compromised Identity

Characteristics:

legitimate credentials
abnormal behavior
access from unusual contexts
knowledge of internal workflows

Primary intelligence:

identity behavior
access patterns
privilege misuse indicators
5. Threat Categories

VALI models threats across five major categories.

External Threat
      │
      ├── Deception Discovery
      ├── Deception Escape
      ├── Credential Abuse
      ├── Egress Abuse
      │
      ▼
Internal Threat
      │
      ├── Analyst Abuse
      ├── Configuration Abuse
      ├── Credential Exposure
      │
      ▼
Infrastructure Threat
      │
      ├── Component Compromise
      ├── Container Escape
      ├── Logging Manipulation
      │
      ▼
Intelligence Threat
      │
      ├── False Attribution
      ├── Data Poisoning
      ├── Correlation Errors
      │
      ▼
Operational Threat
      │
      ├── Misconfiguration
      ├── Excessive Exposure
      └── Insufficient Isolation
6. Threat Scenarios
T01 — Deception Discovery

An adversary determines that the environment is a deception system.

Impact
reduced intelligence value
adversary abandonment
possible evasion of future lures
Mitigation
realistic but synthetic environments
controlled fidelity
behavioral consistency
adaptive lure selection
T02 — Deception Escape

An adversary attempts to move from the deception environment into real infrastructure.

Impact

Critical

Mitigation
hard segmentation
deny-by-default networking
synthetic credentials
controlled egress
isolated execution
continuous boundary monitoring
T03 — Credential Exposure

A real credential accidentally appears within a deception environment.

Impact

Critical

Mitigation
synthetic identities
secret scanning
credential allowlists
environment-specific secrets
automated credential validation
T04 — Telemetry Manipulation

An adversary attempts to corrupt or destroy captured evidence.

Mitigation
append-only logging
centralized collection
integrity verification
restricted log access
independent telemetry channels
T05 — Intelligence Poisoning

An adversary intentionally produces misleading behavior.

Mitigation
confidence scoring
evidence provenance
multi-source correlation
analyst validation
behavioral consistency checks
T06 — VALI Infrastructure Compromise

An attacker compromises the deception infrastructure itself.

Mitigation
minimal privileges
immutable infrastructure
isolation
hardened hosts
continuous integrity monitoring
rapid rebuild capability
7. Trust Boundaries
                    UNTRUSTED
                        │
                        ▼
              ┌─────────────────┐
              │ External Actor  │
              └────────┬────────┘
                       │
                  TRUST BOUNDARY
                       │
                       ▼
              ┌─────────────────┐
              │ VALI Gateway    │
              └────────┬────────┘
                       │
                  TRUST BOUNDARY
                       │
                       ▼
              ┌─────────────────┐
              │ Deception Zone  │
              └────────┬────────┘
                       │
                  TRUST BOUNDARY
                       │
                       ▼
              ┌─────────────────┐
              │ Analysis Zone   │
              └────────┬────────┘
                       │
                  TRUST BOUNDARY
                       │
                       ▼
              ┌─────────────────┐
              │ Production      │
              │ Environment     │
              └─────────────────┘


              🚫 NO DIRECT TRUST
8. Security Assumptions

VALI assumes:

adversaries are untrusted
deception infrastructure may eventually be discovered
captured telemetry may contain hostile input
AI-generated conclusions may be incorrect
operators can misconfigure policies
components can fail
deception infrastructure must be continuously monitored
9. Threat Model Principle

Assume the lure will eventually be discovered. Design the system so that discovery does not compromise the real environment.
