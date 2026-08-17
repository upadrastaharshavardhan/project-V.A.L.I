# Evolution: VALI V1 → V10

This section documents the **implemented reference trajectory**. Each version was designed to ship a working loop, then deepen intelligence and operations.

---

## Capability matrix

| Capability | V1 | V2 | V3 | V4 | V5 | V6 | V7 | V8 | V9 | V10 |
|------------|----|----|----|----|----|----|----|----|----|-----|
| Progressive web decoy | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Session telemetry | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Dashboard | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| SSH honeypot | | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Risk scoring | | | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Canaries / vault layer | | | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Profiling + correlation | | | | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Campaigns + metrics | | | | | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Kill-chain + notes + webhooks | | | | | | ✓ | ✓ | ✓ | ✓ | ✓ |
| Playbooks + blocklist | | | | | | | ✓ | ✓ | ✓ | ✓ |
| LLM adaptive + attack paths | | | | | | | | ✓ | ✓ | ✓ |
| STIX-lite + narratives | | | | | | | | | ✓ | ✓ |
| Release packaging + demo | | | | | | | | | | ✓ |

---

## V1 — MVP

**Intent:** Prove progressive engagement and the observe loop.

- Web decoy portal  
- Session tracking  
- Central logger  
- Basic dashboard  

**Outcome:** The Vali mechanic is demable: more interaction → more structure.

---

## V2 — Multi-protocol

**Intent:** Attackers do not only use HTTP.

- SSH honeypot  
- Shared telemetry concepts  
- Stronger operational scripts  

---

## V3 — Precision and priority

**Intent:** Not all events are equal.

- Risk scores  
- Canary tokens  
- Secrets vault progressive layer  
- Export beginnings  

---

## V4 — Understanding the actor

**Intent:** Label behavior, not only count events.

- Profiles (scanner/automated/interactive/targeted)  
- Cross-service correlation by IP  
- Timelines  

---

## V5 — Campaigns

**Intent:** Analysts think in campaigns.

- Aggregate by source IP  
- Metrics endpoint  
- Campaign-oriented dashboard views  

---

## V6 — Adversary semantics

**Intent:** Map activity to attack stages.

- Kill-chain style tags  
- Campaign risk  
- Analyst notes API  
- Canary webhooks  

---

## V7 — Closed loop (defensive)

**Intent:** Intelligence should drive action hooks.

- Auto-playbooks on high risk / canary  
- Local high-risk IP blocklist  
- Blocklist API + UI  

---

## V8 — Adaptive realism

**Intent:** Reduce obvious honeypot stiffness carefully.

- Shared optional LLM client  
- Adaptive SSH responses for unknowns  
- Attack path summaries per session  

---

## V9 — Shareable intelligence

**Intent:** Meet the organization where intel lives.

- STIX-lite export  
- Campaign narratives  
- High-risk webhooks  

---

## V10 — Release posture

**Intent:** Make the system operable for demos and handoff.

- Polished README, CHANGELOG, LICENSE  
- `demo.sh` path  
- Consistent version branding  
- Recommended entry point for users  

---

## Design lesson across versions

Ship **working value** early (V1), then add **semantic depth** (risk → profile → campaign → kill-chain → narrative), then **operational closure** (playbooks, exports, packaging)—without abandoning isolation or non-retaliation.
