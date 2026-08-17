# VALI — Architecture & Technical Specifications (Confluence)

> **Status:** Reference architecture  
> **Versions:** V1 → V10  
> **Concept:** Upadrasta Harsha Vardhan  
> **Inspiration:** Vāli (Ramayana) — engagement strengthens the defender  

---

## 1. Executive summary

**VALI** is a deception-driven security fabric. Attackers who engage isolated decoy surfaces generate structured intelligence (sessions, risk, tools, kill-chain, campaigns) while production stays out of the fight.

| Goal | Mechanism |
|------|-----------|
| Raise attacker cost | Progressive unlocks + friction |
| Gain visibility | Full telemetry + scoring |
| Stay safe | Strict isolation, no retaliation |
| Act | Canaries, webhooks, blocklist, exports |

---

## 2. System architecture

**Insert image:** `01-system-architecture.png`

| Layer | Components |
|-------|------------|
| Engagement | Web decoy, SSH honeypot |
| Intelligence | Logger (score, profile, tag, campaign) |
| Presentation | Streamlit dashboard |
| Output | JSON/CSV/STIX-lite, webhooks, blocklist |

---

## 3. Progressive engagement (Vali mechanic)

**Insert image:** `02-progressive-engagement.png`

```
Home / Login / Ops / Identity
        ↓ spend
   API Gateway unlock
        ↓ spend
   Staging unlock
        ↓ spend
   Config unlock
        ↓ spend
   Backups unlock
        ↓ spend
   Secrets Vault + Canaries
```

---

## 4. Intelligence pipeline

**Insert image:** `03-intelligence-pipeline.png`

| Stage | Output |
|-------|--------|
| Event ingest | JSONL + session update |
| Derivation | tools, depth, rate |
| Scoring | risk 0–100 |
| Semantics | profile + kill-chain + attack path |
| Aggregate | campaigns + narratives |
| Act | notes, blocklist, webhooks |
| Share | exports |

---

## 5. V1–V10 roadmap

**Insert image:** `04-v1-v10-roadmap.png`

| Ver | Theme | Headline capability |
|-----|-------|---------------------|
| V1 | MVP | Progressive web + telemetry |
| V2 | Protocol | SSH honeypot |
| V3 | Priority | Risk + canaries + vault |
| V4 | Actor | Profiling + correlation |
| V5 | Campaign | IP campaigns + metrics |
| V6 | Semantics | Kill-chain + notes + webhooks |
| V7 | Response | Playbooks + blocklist |
| V8 | Adaptive | LLM SSH + attack paths |
| V9 | Share | STIX-lite + narratives |
| V10 | Release | Demo + packaging |

Full tables: see `TECHNICAL_SPECS_V1_V10.md`.

---

## 6. Deployment topology

**Insert image:** `05-deployment-topology.png`

| Service | Port | Role |
|---------|------|------|
| web-decoy | 8080 | Progressive portal |
| ssh-honeypot | 2222 | Medium-interaction SSH |
| logger | 8001 | Intel API + exports |
| dashboard | 8501 | Analyst UI |

Network: isolated Docker bridge `vali-net`.

---

## 7. Safety panel

| Rule | Requirement |
|------|-------------|
| Isolation | No production secrets in decoys |
| Authorization | Deploy only on owned/authorized systems |
| Retaliation | Not part of core design |
| Data handling | Treat exports as sensitive SOC data |

---

## 8. Related pages

- Technical specs (V1–V10 tables)
- Philosophy & origin (Ramayana metaphor boundaries)
- Vision 2030
- Operations runbook

---

*Attackers spend. Defenders learn.*
