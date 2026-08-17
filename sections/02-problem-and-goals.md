# Problem Statement and Goals

## 1. The problem

### 1.1 Asymmetry today

| Side | Typical advantage |
|------|-------------------|
| Attacker | Chooses time, tools, and patience; can fail quietly |
| Defender | Must succeed broadly; noisy environments; late detection |

Attackers often learn from failed attempts. Defenders often discard failed attempts as “noise.”

### 1.2 Gaps in common controls

- Firewalls and IAM prevent; they do not always **explain adversary intent**  
- IDS/EDR detect known patterns; novel interactive exploration can look “low and slow”  
- Classic honeypots help, but many deployments lack **progressive narrative**, **unified scoring**, and **campaign-level storytelling**

### 1.3 Problem formulation

**How can a defender convert unauthorized interaction into high-value adversarial intelligence while ensuring the interaction cannot reach real assets?**

---

## 2. Goals of VALI

### 2.1 Primary goal

Build a deception fabric such that:

1. Unauthorized actors are engaged on **isolated** surfaces  
2. Their **movement and tactics** become structured intelligence  
3. High-value interactions raise **precise alerts** (canaries)  
4. Operators can act through **exports, dashboards, and playbooks**

### 2.2 Secondary goals

- Progressive engagement that increases attacker cost  
- Multi-protocol coverage (at least web + SSH in the reference design)  
- Offline-first operation with optional adaptive AI features  
- Clear operational lifecycle (deploy, demo, rotate, purge)

### 2.3 Non-goals

- Replacing fundamental security hygiene  
- Guaranteed legal attribution of a human  
- Offensive compromise of attacker-owned systems  

---

## 3. Success criteria

| Criterion | Indicator |
|-----------|-----------|
| Isolation integrity | No real secrets in decoy data paths |
| Engagement | Attackers progress through layers or tools fire canaries |
| Intelligence quality | Sessions scored, tagged, exportable |
| Operator speed | Dashboard + webhooks reduce time-to-awareness |
| Safety | No retaliatory features required for core value |

---

## 4. Stakeholders

- Security engineers and SOC analysts  
- Product security teams  
- Research labs and universities  
- Founders/builders of deception products  

---

## 5. Founder goal restated for 2030 alignment

By 2030, the ambition is that VALI-class protection becomes a **normal layer** of digital defense: when adversaries probe, the organization **gains controlled insight** rather than only absorbing risk—always within legal and ethical bounds.
