# Christensen & Sons

> **5 agents · 297 skills · 1 GPU** — A fully autonomous, self-hosted multi-agent enterprise running on a TensorDock A100 80GB. From Roblox game studios to Facebook community empires to SEC filings. Import and go.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Paperclip](https://img.shields.io/badge/Powered_by-Paperclip-blue)](https://github.com/paperclipai/paperclip)

---

## Quick Start

```bash
npx paperclipai company import --from ./christensen-and-sons
```

---

## The Company

Christensen & Sons is not a single-product shop. It's a **holding company** — a portfolio of autonomous business verticals that share infrastructure, talent, and intelligence. Every vertical below is run by the same 5-agent team, each contributing their domain expertise.

## Business Verticals

### 🎮 Roblox Game Studio
Build, ship, and monetize Roblox experiences end-to-end. Viktor writes Luau with `--!strict`, Clara designs the economy math, Elias audits for COPPA/ToS compliance, Niko creates the marketing assets, and Marcus models the retention curves.

- Gacha/loot box verification (10M simulated pulls)
- Dynamic difficulty adjustment & player retention loops
- LiveOps event balancing (battle passes, daily rewards)
- Crafting economy tuning & virtual inflation correction
- Multiplayer netcode sync, matchmaking, leaderboards

### 📱 Social Media & Content Agency
Full-service content creation, scheduling, and campaign management across every platform. Niko runs the creative pipeline while Marcus measures what's working.

- Cross-platform video cuts (9:16, 1:1, 16:9) with hook optimization
- A/B testing on landing pages, ad copy, and media mix allocation
- Social media autopilot with hashtag velocity tracking
- Real-time trend hijacking (meme detection → on-brand posts)
- Influencer ROI calculation and UGC authenticity scoring
- Crisis communications protocol (sentiment drop → instant PR response)

### 👥 Niche Facebook Community Management
Build and scale hyper-targeted Facebook Groups and Pages as lead generation engines. Clara handles the strategy, Niko creates the content calendar, and Marcus measures engagement velocity.

- Content calendar population based on optimal engagement times
- Audience segmentation mapping (demographic → psychographic)
- Viral loop optimization (referral coefficient tracking)
- Brand voice calibration across all touchpoints
- Community sentiment monitoring and crisis response

### 🏠 Real Estate & Auction Platform (Grand Bluff)
Build and operate auction platforms compliant with MN Stat 330/513.55. Viktor builds the real-time bidding engine, Elias ensures statutory compliance, Clara manages vendor contracts, and Niko produces the listing media.

- Zoning law interpretation for warehouse/commercial leases
- OSHA safety reporting for physical facilities
- Real estate acquisition compliance checks
- Dynamic pricing banners with scarcity messaging
- SEO-optimized property listing content

### 💰 Quantitative Finance & Trading
Marcus runs the math. Options pricing, portfolio beta, yield curves, credit risk — all computed locally on your own hardware. No cloud API dependencies for sensitive financial data.

- Black-Scholes options pricing and Greeks recalculation
- Monte Carlo risk simulation (millions of scenarios)
- High-frequency trade pattern analysis
- Yield curve modeling and bond market recalibration
- Credit risk scoring via logistic regression
- Corporate liquidity forecasting

### 🧬 Biotech & Research Lab
Run genomic pipelines, drug screening, and clinical trial analysis entirely on-premises. Marcus handles the computation, Elias enforces HIPAA/FDA compliance.

- DNA sequence alignment (FASTQ → reference genome)
- Genomic variant calling (SNP identification)
- Multi-omics integration (genomic + transcriptomic + proteomic)
- Biomarker discovery and Bayesian inference
- Clinical trial efficacy testing (hypothesis testing, ANOVA)
- HIPAA violation detection and FDA software validation

### 🌐 Web Development Agency
Viktor builds production Next.js/Node applications. Clara scopes the product, Niko designs the UI prototypes, Elias audits for security, and Marcus builds the data layer.

- Wireframe-to-HTML prototype generation
- UI animation curation (easing curves, motion design)
- Typography accessibility auditing (WCAG compliance)
- Database zero-downtime migrations
- WebSocket stream recovery and real-time state sync
- OAuth2 flow implementation

### 📊 SaaS Operations & Enterprise Consulting
Clara runs the enterprise brain — OKR alignment, vendor negotiations, shift optimization, and SaaS spend audits. Elias provides the compliance backbone.

- OKR cascade validation (department → enterprise alignment)
- SOC2 continuous compliance with evidence collection
- Vendor contract renewal with data-backed negotiation leverage
- Meeting deflation protocol (calendar density optimization)
- SaaS shadow IT discovery and license termination
- Policy drift detection and ISO 27001 mapping

### ⚖️ Legal & Compliance-as-a-Service
Elias operates as a standalone compliance engine. SEC filings, whistleblower triage, NDA enforcement — all automated with Nemotron 30B's 128K context for ingesting dense legal documents.

- Sarbanes-Oxley auditing and 10-Q/10-K drafting
- GDPR consent tracking and CCPA deletion verification
- Algorithmic bias detection (EU AI Act classification)
- KYC document verification and AML scanning
- Insider trading correlation analysis
- Whistleblower escalation with ethics board reporting

### 🎬 Video Production Studio
Niko handles the full post-production pipeline — from raw footage to platform-ready cuts with spatial audio and color grading.

- Podcast post-production (stem separation, show notes, promo clips)
- Automated storyboard generation from scripts
- Immersive audio design (spatial panning for VR/AR)
- Event B-roll curation from massive footage archives
- Color grading suggestions based on brand psychology
- Voiceover-to-video synchronization

---

## Org Chart

```
Clara Muse (CEO) ─── Nemotron 30B ─── Enterprise, Finance, Ops
├── Elias Redstone (CLO) ─── Nemotron 30B (shared) ─── Legal, Compliance, Risk
├── Marcus Christensen (CDS) ─── Qwen3 8B ─── Quant, Genomics, Data Science
├── Niko Relay (CD) ─── Gemma 4 E2B ─── Creative, Video, Social, Ad-Tech
└── Viktor Forge (CTO) ─── Qwen3.6-35B ─── GameDev, Roblox, Backend, Netcode
```

## Agent Details

| Agent | Title | True Model | Context | Skills |
|---|---|---|---|---|
| **Clara Muse** | CEO & Enterprise Leader | Nemotron 30B | 128K | 59 |
| **Elias Redstone** | Chief Legal & Risk Officer | Nemotron 30B (shared) | 128K | 60 |
| **Marcus Christensen** | Chief Data Scientist | Qwen3 8B | 16K | 60 |
| **Niko Relay** | Creative Director | Gemma 4 E2B | 4K | 59 |
| **Viktor Forge** | CTO | Qwen3.6-35B | 64K | 59 |

## Infrastructure

| Component | Detail |
|---|---|
| **GPU** | NVIDIA A100 80GB (TensorDock) |
| **Models** | 5 chat models + nomic-embed-text embeddings |
| **VRAM** | ~69GB / 80GB resident (no swapping) |
| **API** | OpenAI-compatible via Ollama |
| **Paperclip Server** | GCP `cloudagentics` project |
| **Roblox Bridge** | SSH tunnel to local Studio via WeppyRobloxMCP |

## How Nemotron Sharing Works

Clara (CEO) and Elias (CLO) both use `openai/gpt-4o` which routes to the **same** Nemotron 30B Ollama endpoint. The model is loaded once in VRAM (~30GB). Paperclip sees two separate agents with two separate system prompts. Zero additional VRAM cost.

## Available MCP Tools

Agents can access these MCP integrations when configured:

| Tool | Used By | Purpose |
|---|---|---|
| **WeppyRobloxMCP** | Viktor | Direct Roblox Studio manipulation (insert, script, playtest) |
| **Brave Search** | Clara, Niko, Marcus | Web research, competitive intelligence, trend monitoring |
| **Imagen / Image Gen** | Niko | Generate marketing visuals, thumbnails, social assets |
| **File System** | All | Read/write project files, configs, and data |

## Directory Structure

```
christensen-and-sons/
├── COMPANY.md              # Company metadata (agentcompanies/v1)
├── .paperclip.yaml         # Paperclip config (paperclip/v1)
├── README.md               # This file
├── LICENSE                  # MIT
├── .gitignore
├── agents/
│   ├── clara-muse/AGENTS.md
│   ├── elias-redstone/AGENTS.md
│   ├── marcus-christensen/AGENTS.md
│   ├── niko-relay/AGENTS.md
│   └── viktor-forge/AGENTS.md
└── skills/                 # 323 skill directories
    ├── gacha-pull-simulator/SKILL.md
    ├── monte-carlo-risk-simulator/SKILL.md
    ├── ... (297 new + 26 original)
    └── oauth2-flow-implementer/SKILL.md
```

---

Built for [Paperclip](https://github.com/paperclipai/paperclip) · Self-hosted on TensorDock · Christensen & Sons Holdings
