# Operations and Safety

## 1. Operational lifecycle (reference)

| Step | Action |
|------|--------|
| Configure | Copy `.env.example` → `.env`; edit `vali.yaml` |
| Start | `./scripts/start.sh` or `docker compose up --build -d` |
| Demo | `./scripts/demo.sh` (V10) |
| Observe | Dashboard + logger API |
| Rotate | `./scripts/rotate.sh` purge/recreate |
| Stop | `docker compose down` |

---

## 2. Isolation requirements

Minimum bar:

- Decoy hosts/containers separate from production data planes  
- No production credentials in decoy content  
- Egress from decoys tightly controlled in real deployments  
- Administrative access to logger/dashboard protected  

---

## 3. Safety and ethics

### Allowed

- Deception on systems you own or are authorized to protect  
- Logging unauthorized interaction  
- Feeding internal blocklists / SOC workflows  

### Disallowed (as product principles)

- Presenting decoys as real services to harm uninvolved third parties  
- Using VALI as cover for illegal access  
- Building retaliatory intrusion features as “default success”  

---

## 4. Data sensitivity

Session exports can reveal:

- Attacker tooling  
- Your decoy topology and naming  
- Internal narrative choices  

Handle exports under existing security-operations data policies.

---

## 5. Failure modes

| Failure | Mitigation |
|---------|------------|
| Decoy fingerprinting | Improve realism carefully; accept residual risk |
| Alert fatigue | Rely on canaries + high-risk thresholds |
| LLM data leakage | Keep LLM off by default; no production secrets in prompts |
| Operator confusion | Strong docs, demo script, clear dashboards |

---

## 6. Compliance note

This documentation is not legal advice. Organizations must validate deception deployments against local law, regulation, and policy.
