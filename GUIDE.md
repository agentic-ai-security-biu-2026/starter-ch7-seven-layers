# Student guide — Ch5 Seven Layers Deep

**Difficulty:** 5 · **Kickoff:** 13 Dec 2026 · **Deadline:** 22 Dec 2026, 23:59 · Tag: `submission-v1`

## 1. Story

CTO-style seven-layer model: each layer must still help when others fail. You receive an **intentionally weak** agent stack. Harden it with **independent** layers, then red-team each layer.

Suggested layer set (adapt names, keep independence):

1. Identity / authn of caller & workload  
2. Injection / prompt-firewall  
3. Network egress controls  
4. Filesystem / tool sandbox  
5. Output filter / DLP  
6. Audit / tamper-evident logs  
7. Process isolation (containers / gVisor / Kata-class — local)

**In scope:** layered defenses + probes that show layer N failing closed when layer N−1 is disabled.  
**Out of scope:** “break the shared OpenShift cluster”; single mega-middleware that is one blob with seven comments.

## 2. What we expect

1. Hardened fork with toggles or feature flags to disable layers for probing.  
2. [SCENARIO.md](SCENARIO.md) — sector + which layers matter most there.  
3. `TRACE.md` / `REDTEAM.md` — per-layer attack attempt and result.  
4. Public + `submission-v1`.  
5. Demo: disable one layer live; show another still stopping a probe.

## 3. Grading

| Criterion | Weight | Good looks like |
|-----------|--------|-----------------|
| Security effectiveness | 50% | ≥5 meaningful layers with evidence; independence shown |
| Code quality & minimalism | 20% | Layers separable; not a 2k-line ball of mud |
| Presentation / demo | 20% | Clear layer map; honest gaps |
| Creativity | 10% | Novel probe or layer |

**Minimum bar:** ≥5 layers implemented and probed; at least one demo of fail-closed independence.

## 4. Setup & install

```bash
git clone https://github.com/agentic-ai-security-biu-2026/starter-ch5-seven-layers.git
cd starter-ch5-seven-layers
cp .env.example .env
podman compose up --build
# Optional Garak-style / custom probes when shipped:
podman compose run --rm redteam
```

Prefer **local Podman**. OpenShift only for closing demos with locked SCC.

## 5. Related reading

- Defense in depth / Swiss cheese model  
- Sandbox escape awareness (learn locally — never on shared demo)  
- Garak / LLM red-teaming tools (optional)  
- Reuse ideas from Ch2 (identity) and Ch3 (output/data) as *layers*, not copies of those whole tracks

## 6. Support

Hub: `starter-bug`, `challenge-concept`, `infra`, `llm-nebius`. Expect heavier mentor load — ask early.
