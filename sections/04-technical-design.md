# Technical Design

## 1. Progressive engagement engine

### 1.1 Mechanism

Each meaningful web request increments `session["actions"]`.  
Unlock rules declare `min_actions` and optional `requires` dependencies.

Example (illustrative):

```yaml
progressive:
  unlocks:
    api_docs: { min_actions: 3 }
    staging: { min_actions: 5, requires: api_docs }
    config_panel: { min_actions: 8, requires: staging }
    backup_files: { min_actions: 11, requires: config_panel }
    secrets_vault: { min_actions: 14, requires: backup_files }
```

### 1.2 Design intent

- Early pages look open and legitimate  
- High-value pages appear only after investment  
- Navigation can reveal unlock state (e.g., green indicators)  

This is the engineering form of the Vali mechanic: **engagement depth increases defender signal**.

---

## 2. Web decoy design

### 2.1 Surface style

Later UI iterations use a dense enterprise control-plane layout:

- Sidebar information architecture  
- Top bar status/search  
- Cards, tables, tags, charts  
- Breadcrumbs and module status  

### 2.2 Event emission

Typical event types:

- `request`  
- `login_attempt`  
- `unlock`  
- `canary`  

Payload includes path, method, user-agent, source IP, session id, optional details.

### 2.3 Cost imposition

Optional adaptive delay increases friction under aggressive behavior (config-driven).

---

## 3. SSH honeypot design

### 3.1 Interaction level

Medium interaction:

- Accept auth attempts  
- Provide prompt and common command responses  
- Fake filesystem and files (notes, config snippets, decoy secrets)  

### 3.2 Adaptive layer (optional)

When `ENABLE_LLM=true`, unknown commands may receive generated shell-like output via an OpenAI-compatible client, with offline fallback to `command not found`.

---

## 4. Logger / intelligence engine

### 4.1 Ingest API

- `POST /ingest` — general events  
- `POST /canary` — high-priority canary path  
- `POST /sessions/{id}/notes` — analyst notes  

Authenticated with `X-API-Key`.

### 4.2 Session update pipeline

1. Load or create session document  
2. Append event  
3. Update derived fields (paths, tools, unlocks, commands)  
4. Tag kill-chain labels for the event  
5. Recompute risk and profile  
6. Recompute attack path  
7. Run playbooks if thresholds crossed  
8. Correlate related sessions by IP  
9. Persist JSON  

### 4.3 Tool fingerprinting

User-agent and path regexes map to tool labels (sqlmap, nikto, scanners, dirbusters, browsers, etc.).

---

## 5. Risk model (reference)

Weighted contributors (configurable):

- Unlock depth  
- Login attempts  
- Unique tools  
- Event volume (capped)  
- SSH command volume (capped)  
- Canary hits  
- Targeted path interest  
- Fast automation rate  

Output: integer score in `[0, 100]`.

---

## 6. Profiling heuristic

| Profile | Typical signals |
|---------|-----------------|
| scanner | scanner tools, low depth |
| automated | high event rate, non-browser |
| interactive | browser, longer duration |
| targeted | high depth and/or canaries |
| unknown | insufficient signal |

---

## 7. Playbooks and response hooks

| Trigger | Actions (reference) |
|---------|---------------------|
| Risk crosses threshold | auto note, blocklist IP, optional webhook |
| Canary hit | auto note, blocklist IP, webhook, canary file |

Blocklist is local/file-based in the reference design—intended as a feed for downstream controls, not an autonomous internet weapon.

---

## 8. Export interfaces

- JSON sessions  
- CSV summary  
- STIX-lite bundle (indicator + IP objects + VALI extensions)  
- Prometheus-style metrics text  

---

## 9. Technology choices (reference stack)

| Area | Choice |
|------|--------|
| Web decoy | Python, FastAPI, Jinja templates |
| SSH | asyncssh |
| Intel API | FastAPI |
| Dashboard | Streamlit |
| Packaging | Docker Compose |
| Config | YAML |

These choices optimize for inspectability and rapid iteration, not for a single vendor lock-in.
