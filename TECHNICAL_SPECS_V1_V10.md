# VALI Technical Specifications — V1 to V10

**Product:** VALI — Deception-Driven Security Fabric  
**Concept:** Upadrasta Harsha Vardhan  
**Scope:** Reference implementation trajectory V1 → V10  

---

## 1. Platform baseline (all versions unless noted)

| Item | Specification |
|------|----------------|
| Primary language | Python 3.12 |
| Web framework | FastAPI |
| Dashboard | Streamlit |
| SSH stack | asyncssh (V2+) |
| Config | YAML (`vali.yaml`) |
| Packaging | Docker Compose |
| Default web port | 8080 |
| Default SSH port | 2222 |
| Default logger port | 8001 |
| Default dashboard port | 8501 |
| Isolation model | Docker bridge network `vali-net` |
| Telemetry format | JSON events + per-session JSON |
| Auth (API) | `X-API-Key` header on logger |

---

## 2. Component matrix by version

| Component | V1 | V2 | V3 | V4 | V5 | V6 | V7 | V8 | V9 | V10 |
|-----------|----|----|----|----|----|----|----|----|----|-----|
| Web progressive decoy | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Logger / session store | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Dashboard | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| SSH honeypot | — | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Risk engine | — | — | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Canary system | — | — | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Secrets vault layer | — | — | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Attacker profiling | — | — | — | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| IP correlation | — | — | — | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Campaign aggregation | — | — | — | — | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Metrics endpoint | — | — | — | — | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Kill-chain tags | — | — | — | — | — | ✓ | ✓ | ✓ | ✓ | ✓ |
| Analyst notes API | — | — | — | — | — | ✓ | ✓ | ✓ | ✓ | ✓ |
| Canary webhooks | — | — | — | — | — | ✓ | ✓ | ✓ | ✓ | ✓ |
| Auto-playbooks | — | — | — | — | — | — | ✓ | ✓ | ✓ | ✓ |
| Local blocklist | — | — | — | — | — | — | ✓ | ✓ | ✓ | ✓ |
| LLM adaptive client | — | — | — | — | — | — | — | ✓ | ✓ | ✓ |
| Attack path summary | — | — | — | — | — | — | — | ✓ | ✓ | ✓ |
| STIX-lite export | — | — | — | — | — | — | — | — | ✓ | ✓ |
| Campaign narratives | — | — | — | — | — | — | — | — | ✓ | ✓ |
| High-risk webhooks | — | — | — | — | — | — | — | — | ✓ | ✓ |
| Demo + release pack | — | — | — | — | — | — | — | — | — | ✓ |

---

## 3. Version-by-version technical specification

### V1 — MVP
| Spec | Detail |
|------|--------|
| Goal | Prove progressive engagement + observe loop |
| Surfaces | Web decoy only |
| Session model | Cookie/session actions + unlock list |
| Storage | JSONL events, session JSON |
| UI | Basic dashboard |
| Deliverable | Runnable Compose stack |

### V2 — SSH
| Spec | Detail |
|------|--------|
| Goal | Multi-protocol deception |
| New | Medium-interaction SSH honeypot |
| Logging | Web + SSH into shared logger model |
| Fingerprinting | User-agent / tool regex foundations |

### V3 — Risk & Canaries
| Spec | Detail |
|------|--------|
| Goal | Prioritize high-value interactions |
| Risk | Weighted 0–100 score |
| Canaries | Path-based high-priority alerts |
| Vault | Progressive secrets vault module |
| Export | JSON / CSV beginnings |

### V4 — Profiling
| Spec | Detail |
|------|--------|
| Goal | Label attacker behavior classes |
| Profiles | scanner, automated, interactive, targeted, unknown |
| Correlation | Same-IP related sessions |
| UI | Timelines |

### V5 — Campaigns
| Spec | Detail |
|------|--------|
| Goal | Campaign-level analysis |
| Aggregation | By source IP |
| Metrics | Prometheus-style text metrics |
| Dashboard | Campaigns view |

### V6 — Kill-chain
| Spec | Detail |
|------|--------|
| Goal | Semantic attack-stage labeling |
| Tags | recon, credential_access, discovery, collection, execution, high_value, progress |
| Notes | Analyst notes API |
| Alerts | Optional canary webhooks |
| Campaign risk | Aggregate score |

### V7 — Playbooks
| Spec | Detail |
|------|--------|
| Goal | Closed-loop defensive hooks |
| Auto-notes | On high-risk threshold and canary |
| Blocklist | `high_risk_ips.txt` + API + dashboard tab |
| Threshold | Configurable (default 60) |

### V8 — LLM + Paths
| Spec | Detail |
|------|--------|
| Goal | Adaptive realism + clearer story |
| LLM | Optional OpenAI-compatible client |
| SSH | Dynamic replies for unknown commands |
| Attack path | Ordered unique kill-chain progression |
| Fallback | Fully offline when LLM disabled |

### V9 — STIX + Narratives
| Spec | Detail |
|------|--------|
| Goal | Shareable threat intelligence |
| Export | STIX-lite bundle (`indicator`, `ipv4-addr`, `x_vali`) |
| Narrative | Human-readable per-IP campaign summary |
| Webhooks | High-risk + canary |

### V10 — Release
| Spec | Detail |
|------|--------|
| Goal | Operable product posture |
| Packaging | README, CHANGELOG, LICENSE |
| Scripts | start, demo, status, rotate |
| Entry point | Recommended production of the series |

---

## 4. Progressive unlock specification (reference)

| Unlock module | Typical min_actions | Requires | Decoy value signal |
|---------------|---------------------|----------|---------------------|
| api_docs | 3 | — | Internal API map |
| staging | 5–6 | api_docs | Non-prod control panel |
| config_panel | 8–10 | staging | Config + danger zone |
| backup_files | 11–14 | config_panel | Backup index |
| secrets_vault | 14–17 | backup_files | Masked secrets store |

---

## 5. Risk model specification (reference weights)

| Feature | Example weight role |
|---------|---------------------|
| depth (unlocks) | Strong intent signal |
| login_attempts | Credential access |
| unique_tools | Capability / automation |
| event_count | Volume (capped) |
| ssh_commands | Interactive depth (capped) |
| canary_hit | Highest precision boost |
| fast_automation | Rate-based automation |
| targeted_paths | Secrets/backup/config interest |

Score clamped to **0–100**.

---

## 6. API surface (logger, mature versions)

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/health` | GET | Liveness |
| `/ingest` | POST | Event ingest |
| `/canary` | POST | Canary alert |
| `/sessions` | GET | List sessions |
| `/sessions/{id}` | GET | Session detail |
| `/sessions/{id}/notes` | POST | Add note |
| `/campaigns` | GET | Campaign aggregate |
| `/stats` | GET | Global stats |
| `/metrics` | GET | Prometheus text |
| `/blocklist` | GET | High-risk IPs (V7+) |
| `/export/sessions.json` | GET | Full export |
| `/export/sessions.csv` | GET | CSV export |
| `/export/stix-lite` | GET | STIX-lite (V9+) |

---

## 7. Data products

| Artifact | Path (reference) | Description |
|----------|------------------|-------------|
| Event log | `data/logs/events-*.jsonl` | Append-only events |
| Session intel | `data/sessions/*.json` | Derived intelligence |
| Canary records | `data/canaries/*.json` | High-priority hits |
| Blocklist | `data/blocklist/high_risk_ips.txt` | Downstream feed |

---

## 8. Non-functional requirements

| NFR | Target (reference) |
|-----|---------------------|
| Isolation | Decoys never require production DB/credentials |
| Offline mode | Full function with LLM disabled |
| Operability | One-command start; rotate/purge scripts |
| Safety | No retaliation features in core design |
| Explainability | Weighted scores + tags over opaque-only ML |

---

*End of technical specifications.*
