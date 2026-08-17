# System Architecture

## 1. Architectural statement

VALI is a **modular, container-friendly deception fabric** with a central intelligence service. Interactive decoys are disposable; intelligence is durable.

---

## 2. Logical components

```text
+------------------+       +------------------+
|   Web Decoy      |       |  SSH Honeypot    |
|  (FastAPI/UI)    |       |  (asyncssh)      |
+--------+---------+       +--------+---------+
         |                          |
         +------------+-------------+
                      |
                      v
              +---------------+
              | Logger/Intel  |
              |  (FastAPI)    |
              +-------+-------+
                      |
          +-----------+-----------+
          |                       |
          v                       v
   +-------------+         +--------------+
   | Dashboard   |         | Exports/Hooks|
   | (Streamlit) |         | STIX/CSV/WH  |
   +-------------+         +--------------+
```

---

## 3. Component responsibilities

### 3.1 Web decoy

- Presents an enterprise control-plane illusion  
- Maintains session state (actions, unlocks)  
- Emits request/login/unlock/canary events  
- Gates modules by progressive rules  

### 3.2 SSH honeypot

- Accepts connections on a non-production port  
- Provides medium-interaction command surface  
- Logs commands and authentication attempts  
- Optionally uses LLM for unknown command text (V8+)  

### 3.3 Logger / intelligence engine

- Authenticates ingest with API key  
- Appends JSONL events  
- Maintains per-session JSON intelligence documents  
- Computes risk, profile, kill-chain tags, campaigns  
- Executes playbooks (notes, blocklist, webhooks)  
- Serves exports and metrics  

### 3.4 Dashboard

- Reads session/canary/blocklist artifacts  
- Presents ranked sessions, campaigns, timelines  

### 3.5 Configuration

`config/vali.yaml` controls:

- Unlock thresholds and dependencies  
- Scoring weights  
- Profiling thresholds  
- Canary IDs/paths  
- Playbook flags  

---

## 4. Data architecture

```text
data/
  logs/          # events-YYYY-MM-DD.jsonl
  sessions/      # {session_id}.json
  canaries/      # canary hit records
  blocklist/     # high_risk_ips.txt (V7+)
  ssh/           # optional SSH runtime
```

### Session document (conceptual fields)

- identity: session_id, source_ip, service  
- time: first_seen, last_seen  
- behavior: paths, commands, unlocks, depth  
- detection: tools, login_attempts, canary_hits  
- intelligence: risk_score, profile, kill_chain_tags, attack_path  
- collaboration: notes, related_sessions  

---

## 5. Network isolation model

Reference deployment uses Docker Compose on a private bridge network:

- Decoys publish only intended ports  
- Logger is internal-facing except API/metrics as configured  
- No requirement for decoys to reach production databases  

Production hardening (beyond reference) may add:

- Separate VLANs  
- Kubernetes NetworkPolicies  
- Brokered egress deny-by-default  

---

## 6. Control vs data plane

| Plane | Contents |
|-------|----------|
| Control | config, playbooks, API keys, unlock rules |
| Data | events, sessions, canaries, exports |
| Presentation | decoy UI, dashboard UI |

---

## 7. Extension points

- New decoy protocols (RDP, SMB, cloud control APIs)  
- New scorers / ML models  
- SIEM connectors beyond STIX-lite  
- Multi-tenant campaign correlation  

See also: [diagrams/architecture.md](../diagrams/architecture.md)
