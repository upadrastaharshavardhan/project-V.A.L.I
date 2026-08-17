# Intelligence Model

## 1. Purpose

Convert adversarial interaction into **decision-ready structure** for humans and downstream systems.

---

## 2. Event layer

Atomic observations:

- Timestamp  
- Session id  
- Source IP  
- Service (web/ssh)  
- Event type  
- Path / command  
- User-agent  
- Details blob  
- Derived kill-chain tags  

Events are appended to daily JSONL logs and folded into session documents.

---

## 3. Session layer

A session is the primary analytical object.

### Derived behavioral features

- Path sequence  
- Unlock list and depth  
- Login attempt count  
- Tool set  
- Command list (SSH)  
- Canary hit count and IDs  
- Duration and event rate  

### Derived intelligence features

- Risk score  
- Profile label  
- Kill-chain tag set  
- Attack path (ordered)  
- Related sessions (same IP)  
- Analyst notes  

---

## 4. Risk scoring

Risk is a **bounded heuristic**, not a probability of identity.

Typical contributors:

| Signal | Rationale |
|--------|-----------|
| Depth / unlocks | Pursuit of value |
| Login attempts | Credential access interest |
| Tool diversity | Capability / automation |
| Volume (capped) | Activity intensity |
| Canaries | High-precision interest |
| Targeted paths | Intent toward secrets/backups |
| High rate | Automation |

Operators should tune weights to their environment.

---

## 5. Kill-chain tags

Lightweight labels aligned loosely with common adversarial stages:

- `recon`  
- `credential_access`  
- `discovery`  
- `collection`  
- `execution`  
- `high_value`  
- `progress`  

Tags are explanatory aids; they are not a full ATT&CK implementation.

---

## 6. Campaign layer

Campaigns aggregate sessions sharing a source IP (reference design):

- session_count  
- max/avg/campaign risk  
- profiles and services observed  
- canary totals  
- ordered attack path union  
- human-readable **narrative** (later versions)  

---

## 7. Export layer

| Format | Use |
|--------|-----|
| JSON | Full fidelity archive |
| CSV | Spreadsheet / quick triage |
| STIX-lite | Threat intel tooling interop |
| Metrics | Monitoring scrape |

---

## 8. Quality principles

1. Prefer **precision** on canaries over noisy low-level alerts  
2. Keep models **explainable** (weights, tags)  
3. Preserve **raw events** for re-analysis  
4. Treat intelligence as **sensitive operational data**  
