# 🛡️ SENTINEL

**Open-Source AI-Powered Market Protection Protocol**

> *"The best trade is sometimes no trade. Our AI is brave enough to say that."*

[![License: AGPL v3](https://img.shields.io/badge/License-AGPL%20v3-blue.svg)](https://www.gnu.org/licenses/agpl-3.0)
[![Discord](https://img.shields.io/discord/placeholder?color=7289da&label=Discord&logo=discord)](link-to-discord)
[![Contributors](https://img.shields.io/github/contributors/yourusername/sentinel)](link-to-contributors)

---

## The Problem

Sophisticated actors exploit information asymmetry to extract billions from retail participants daily. Detection tools exist—Arkham, Dune, Nansen—but they're either:

- **Institutional-priced** ($1k+/month)
- **Raw data firehoses** requiring expert interpretation  
- **Built to exploit patterns**, not avoid them

Meanwhile, AI agents optimize yield farming and automated trading. Almost none are built to say: *"Don't trade today. The conditions match [historical manipulation event]."*

**This is a coordination failure, not a technical one.**

---

## What We Build

An **always-on, community-governed immune system** for economic self-defense:

```
┌─────────────────────────────────────────────────────────────┐
│  LAYER 3: TRANSPARENCY                                       │
│  Public dashboards, open APIs, manipulation weather reports   │
│  "This is what's happening. This is what history says."       │
├─────────────────────────────────────────────────────────────┤
│  LAYER 2: COLLECTIVE INTELLIGENCE                            │
│  Community-validated patterns, decentralized knowledge graph  │
│  "We saw this before. We documented it. We learned."       │
├─────────────────────────────────────────────────────────────┤
│  LAYER 1: PERSONAL SENTINEL                                  │
│  Multi-agent AI, read-only wallet, contextual intervention    │
│  "This looks like Feb 5. Consider waiting 48 hours."         │
└─────────────────────────────────────────────────────────────┘
```

---

## Technical Architecture

### Multi-Agent Detection System

```python
# Simplified core loop
class SentinelAgent:
    def analyze(self, market_context):
        # Parallel agents
        on_chain = self.chain_agent.detect_anomalies(market_context.assets)
        sentiment = self.social_agent.detect_manipulation(market_context.assets)
        calendar = self.macro_agent.check_events(market_context.timestamp)

        # Fusion layer
        risk_score = self.consensus_engine.synthesize(
            [on_chain, sentiment, calendar],
            historical_patterns=self.knowledge_graph.query(market_context.fingerprint)
        )

        if risk_score.confidence > 0.8 and risk_score.severity == "critical":
            return Intervention(
                action="PAUSE",
                reasoning=risk_score.explanation,  # Always explainable
                historical_precedent=risk_score.similar_events
            )
```

### Stack

| Layer | Technology |
|-------|------------|
| **AI Core** | LangGraph / CrewAI + Grok/Claude APIs |
| **Data Sources** | Arkham API, Dune, Covalent, The Graph, Santiment, LunarCrush |
| **Delivery** | Telegram/Discord bots → Browser extension → Mobile |
| **Validation** | Community consensus + reputation staking |
| **Governance** | Snapshot (off-chain) → Optional Aragon (on-chain) |
| **Security** | AgentARC patterns, sandboxed execution, human-in-the-loop |

---

## Current Status

| Phase | Status | Target |
|-------|--------|--------|
| **0: Proof of Protection** | 🚧 In Progress | Single-pattern detection (Feb 5-style alerts) |
| **1: Personal Sentinel** | 📋 Planned | Multi-agent architecture, wallet integration |
| **2: Collective Intelligence** | 📋 Planned | Community validation, shared dashboards |
| **3: Protocol Maturity** | 📋 Planned | Browser extension, DAO governance |

---

## How to Contribute

We need **builders, not speculators**. No token to buy. No Discord roles to grind. Just build.

### Immediate Needs

| Role | What You'd Build | Skills |
|------|------------------|--------|
| **AI/ML Engineer** | Pattern detection agents for specific manipulation types | Python, LangChain/LangGraph, prompt engineering |
| **Data Engineer** | ETL pipelines from Arkham, Dune, social APIs | Python, SQL, Apache Airflow/dbt |
| **Security Researcher** | Harden agent architectures against adversarial attacks | Rust/Go, ML security, smart contract auditing |
| **Full-Stack Dev** | Telegram bot + dashboard for community signals | TypeScript, React, Node.js |
| **Smart Contract Dev** | Reputation/staking mechanisms for pattern validation | Solidity, Cairo, or Rust (Solana) |
| **DevOps Engineer** | Infrastructure for decentralized signal validation | Kubernetes, Terraform, Web3 infrastructure |

### First Steps

```bash
# 1. Clone
git clone https://github.com/yourusername/sentinel.git
cd sentinel

# 2. Setup (see /docs/setup.md for full guide)
cp .env.example .env
# Add your API keys: Arkham, Dune, Grok/Claude

# 3. Run the Feb 5 detection agent (our MVP)
python -m src.agents.feb5_pattern --demo

# 4. Check open issues
gh issue list --label "good first issue"
```

### Contribution Workflow

1. **Read** [`VISION.md`](./VISION.md) and [`CONTRIBUTING.md`](./CONTRIBUTING.md)
2. **Comment** on an issue to claim it (or propose a new one)
3. **Fork** and branch: `git checkout -b feature/your-feature-name`
4. **Test**: All code must include tests. All agents must include adversarial test cases.
5. **Document**: If you add a detection pattern, document the historical precedent.
6. **PR**: Reference the issue, explain the "why," include demo output.

---

## Repository Structure

```
sentinel/
├── src/
│   ├── agents/              # LangGraph implementations
│   │   ├── feb5_pattern.py  # MVP: Feb 5-style detection
│   │   ├── chain_agent.py   # On-chain anomaly detection
│   │   ├── sentiment_agent.py # Social manipulation detection
│   │   └── fusion.py        # Consensus engine
│   ├── data/
│   │   ├── connectors/      # Arkham, Dune, etc.
│   │   └── pipelines/       # ETL workflows
│   ├── delivery/
│   │   ├── telegram_bot.py
│   │   └── extension/       # Browser extension (Phase 1)
│   ├── security/
│   │   └── validation.py    # AgentARC-inspired hardening
│   └── contracts/           # Reputation/governance (Phase 2)
├── docs/
│   ├── architecture/        # System design
│   ├── patterns/            # Documented manipulation cases
│   │   ├── feb5_2024.md     # Case study: Feb 5 liquidation cascade
│   │   └── template.md      # How to document new patterns
│   └── api/                 # API documentation
├── tests/
│   ├── unit/
│   ├── integration/
│   └── adversarial/         # Tests that try to fool our agents
├── community/
│   ├── proposals/           # Governance proposals
│   └── signals/             # Validated community detections
└── research/                # Papers, post-mortems, references
```

---

## Principles (Non-Negotiable)

1. **Protection Over Profit**
   - If a feature encourages risky behavior, we don't build it
   - "Don't trade" is celebrated, not buried

2. **Radical Transparency**
   - All detection logic open-source
   - Every alert explains: *why this signal, why now, what history says*

3. **Community Sovereignty**
   - No VC control. Contributors govern.
   - Exit to community, not exit to liquidity

4. **Adversarial Robustness**
   - Assume attackers will poison our signals
   - Design for Byzantine environments from day one

---

## The Long Game

We're building **infrastructure for economic self-defense** that outlives any team, token, or market cycle.

When the next Feb 5 happens—and it will—we want thousands to receive: *"Your Sentinel detected the pattern. You're safe."*

We want the manipulation to fail because too many saw it coming.

---

## Connect

- **Discord**: [link] (dev coordination, signal validation)
- **Telegram**: [link] (bot testing, user feedback)
- **Discussions**: [GitHub Discussions](link) (architecture decisions, RFCs)
- **Twitter/X**: [handle] (public alerts, transparency reports)

---

## License

[AGPL-3.0](./LICENSE) — *If you use this to protect people, you must share how.*

---

**Ready to build the shield?**  
Open an issue. Fork the repo. Join the immune system.
