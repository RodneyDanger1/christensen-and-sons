# Christensen & Sons

> **5 agents, 297 skills, 1 GPU** — A self-hosted multi-agent enterprise running on a TensorDock A100 80GB. From Roblox game engineering to SEC filings to viral marketing campaigns. Import and go.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Paperclip](https://img.shields.io/badge/Powered_by-Paperclip-blue)](https://github.com/paperclipai/paperclip)

---

## Quick Start

```bash
npx paperclipai company import --from ./christensen-and-sons
```

## Org Chart

```
Clara Muse (CEO) — Nemotron 30B — Enterprise, Finance, Ops
├── Elias Redstone (CLO) — Nemotron 30B (shared) — Legal, Compliance, Risk
├── Marcus Christensen (CDS) — Qwen3 8B — Quant, Genomics, Data Science
├── Niko Relay (CD) — Gemma 4 E2B — Creative, Video, Social, Ad-Tech
└── Viktor Forge (CTO) — Qwen3.6-35B — GameDev, Roblox, Backend, Netcode
```

## Agents

| Agent | Title | True Model | Context | Skills |
|---|---|---|---|---|
| **Clara Muse** | CEO & Enterprise Leader | Nemotron 30B | 128K | 59 |
| **Elias Redstone** | Chief Legal & Risk Officer | Nemotron 30B (shared) | 128K | 60 |
| **Marcus Christensen** | Chief Data Scientist | Qwen3 8B | 16K | 60 |
| **Niko Relay** | Creative Director | Gemma 4 E2B | 4K | 59 |
| **Viktor Forge** | CTO | Qwen3.6-35B | 64K | 59 |

## Infrastructure

- **GPU:** NVIDIA A100 80GB (TensorDock)
- **Models:** 5 chat models + nomic-embed-text embeddings
- **VRAM:** ~69GB / 80GB resident
- **API:** OpenAI-compatible via Ollama (`OPENAI_BASE_URL`)

## How Nemotron Sharing Works

Clara (CEO) and Elias (CLO) both use `openai/gpt-4o` which routes to the **same** Nemotron 30B Ollama endpoint. The model is loaded **once** in VRAM (~30GB). Both agents send requests to the same URL but with completely different system prompts. Zero additional VRAM cost.

## Directory Structure

```
christensen-and-sons/
├── COMPANY.md              # Company metadata (agentcompanies/v1)
├── .paperclip.yaml         # Paperclip configuration (paperclip/v1)
├── README.md               # This file
├── LICENSE                  # MIT
├── agents/
│   ├── clara-muse/AGENTS.md
│   ├── elias-redstone/AGENTS.md
│   ├── marcus-christensen/AGENTS.md
│   ├── niko-relay/AGENTS.md
│   └── viktor-forge/AGENTS.md
└── skills/
    ├── m-a-target-triage/SKILL.md
    ├── gacha-pull-simulator/SKILL.md
    ├── ... (297 total skill directories)
    └── oauth2-flow-implementer/SKILL.md
```

## Skill Domains

### Clara Muse — Enterprise (59 skills)
M&A target triage, supply chain recovery, quarterly fiscal close, shift optimization, executive briefing generation, vendor contract renewal, incident command response, agile sprint planning, IoT fleet maintenance, strategic pivot evaluation, corporate reorganization, meeting deflation, SaaS spend audit, logistics load balancing, macro risk adjustment, OKR cascade validation, manufacturing yield loop, pricing elasticity sweep, multi-agent load balancing.

### Elias Redstone — Legal & Risk (60 skills)
Pre-publish content gate, vendor onboarding audit, SOC2 compliance, data subject access requests, algorithmic deployment check, KYC pipeline, internal fraud detection, cyber incident reporting, source code sanitization, shadow IT sweep, clinical trial data compliance, statutory data purge, SEC filing, real estate acquisition check, whistleblower escalation, NDA enforcement, zero-trust validation, policy drift alignment, insider threat analysis, AI feature impact assessment.

### Marcus Christensen — Quant & Data (60 skills)
Algorithmic strategy validation, compound screening, competitor analysis, genomic data pipeline, real-time fraud detection, data warehouse build, clinical trial efficacy, options Greeks recalculation, material science simulation, ad hoc SQL queries, macro economic response, instrument data ingestion, corporate liquidity forecast, bond market recalibration, HFT pattern sweep, sensor telemetry aggregation, biomarker validation, graph relationship discovery, model drift correction, credit risk assessment.

### Niko Relay — Creative & Marketing (59 skills)
Cross-platform video launch, A/B testing, podcast post-production, trend hijacking, global product rollout, influencer campaign audit, web accessibility sweep, crisis communications, storyboard generation, immersive audio design, SEO content optimization, UI prototype generation, event B-roll curation, predictive creative scoring, social media autopilot, AR filter deployment, dynamic pricing banners, voiceover sync, audience segmentation, viral loop optimization.

### Viktor Forge — Engineering (59 skills)
Roblox auto-playtest, virtual inflation correction, multiplayer netcode sync, microservice outage recovery, gacha system verification, dynamic server scaling, physics engine optimization, procedural world generation, zero-downtime migration, competitive matchmaking, NPC behavior refinement, tech debt refactoring, LiveOps event balancing, exploit duplication prevention, automated QA test suite, real-time leaderboard update, crafting economy tuning, async thread optimization, WebSocket stream recovery, dynamic player retention loop.

---

Built for [Paperclip](https://github.com/paperclipai/paperclip) | Self-hosted on TensorDock
