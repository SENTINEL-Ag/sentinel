# Contributing to Sentinel

Thank you for considering contributing to economic self-defense infrastructure.

## Quick Start

1. Read [`VISION.md`](./VISION.md) — understand *why* we build
2. Check [`docs/architecture/`](./docs/architecture/) — understand *how* we build
3. Find an issue labeled `good first issue` or `help wanted`
4. Comment to claim it. Wait for assignment (prevents duplicate work).

## Development Setup

### Prerequisites

- Python 3.11+
- Node.js 18+ (for extension work)
- API keys: Arkham, Dune, Grok/Claude (see `.env.example`)

### Installation

```bash
# Clone your fork
git clone https://github.com/YOUR_USERNAME/sentinel.git
cd sentinel

# Python environment
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt
pip install -r requirements-dev.txt

# Pre-commit hooks (enforced in CI)
pre-commit install
```

### Verify Setup

```bash
# Run the Feb 5 detection demo (no API keys needed for demo mode)
python -m src.agents.feb5_pattern --demo

# Run tests
pytest tests/ -v

# Run with your API keys (live data)
cp .env.example .env
# Edit .env with your keys
python -m src.agents.feb5_pattern --live --asset BTC
```

## Contribution Areas

### 1. Detection Agents (`src/agents/`)

Building new manipulation pattern detection:

```python
# Template: src/agents/your_pattern.py
from typing import Dict, List
from dataclasses import dataclass

from .base import BaseAgent, Signal, RiskLevel

@dataclass
class YourPatternSignal(Signal):
    # Define your specific signal fields
    anomaly_score: float
    historical_precedents: List[str]

class YourPatternAgent(BaseAgent):
    """
    Detects [specific manipulation pattern].

    Historical precedent: [Date, Event, Link to docs/patterns/]
    """

    def analyze(self, context: MarketContext) -> YourPatternSignal:
        # Implementation
        pass

    def validate(self, signal: YourPatternSignal) -> bool:
        # Self-validation logic
        pass
```

**Requirements:**
- Must include historical precedent documentation in `docs/patterns/`
- Must include adversarial test cases (how could this be fooled?)
- Must return explainable output (no black box scores)

### 2. Data Connectors (`src/data/connectors/`)

Adding new data sources:

```python
# Must implement BaseConnector interface
class NewExchangeConnector(BaseConnector):
    def fetch_flows(self, asset: str, window: timedelta) -> DataFrame:
        pass

    def validate_data(self, raw_data: Any) -> bool:
        # Check for data poisoning, stale data, anomalies
        pass
```

### 3. Security Hardening (`src/security/`)

- AgentARC pattern implementations
- Prompt injection defenses
- Sandboxed execution environments

### 4. Documentation (`docs/`)

- `docs/patterns/`: New manipulation case studies
- `docs/architecture/`: System design updates
- `docs/api/`: API documentation

## Code Standards

### Python

- **Formatter**: Black (88 char line length)
- **Linter**: Ruff
- **Type Hints**: Required for all public functions
- **Testing**: pytest, minimum 80% coverage, 100% for security-critical code

### AI Agent Specific

1. **Explainability**: Every risk score must include `reasoning` field
2. **Confidence Calibration**: Scores must be calibrated (80% confidence = 80% historical accuracy)
3. **Adversarial Testing**: Every agent must have tests attempting to fool it

Example:
```python
def test_feb5_agent_resists_fake_whale_signal():
    """Test that agent isn't fooled by single large transfer without context."""
    fake_context = create_context(
        single_large_transfer=True,
        no_sentiment_spike=True,
        weekday=True  # Feb 5 was weekend
    )
    result = agent.analyze(fake_context)
    assert result.confidence < 0.3  # Low confidence due to missing context
```

### Git Workflow

```bash
# Branch naming
feature/your-feature-name      # New features
fix/issue-description          # Bug fixes
docs/what-you-documented       # Documentation
security/vulnerability-desc    # Security fixes

# Commits (conventional commits)
feat: add liquidation cascade detection
fix: correct whale wallet labeling
docs: add Feb 5 case study
security: add prompt injection defense for sentiment agent

# PR requirements
- Reference issue number
- Include test output
- For agents: include sample alert output
- Update relevant documentation
```

## Review Process

1. **Automated Checks**: CI runs tests, linting, type checking
2. **Peer Review**: Minimum 1 approval from maintainer
3. **Security Review**: Required for any code touching:
   - Wallet connections
   - Agent decision-making
   - Reputation/staking mechanisms

## Recognition

Contributors are tracked in:

- `CONTRIBUTORS.md` (all contributors)
- Release notes (significant features)
- Agent documentation (pattern authors credited)

No token allocations. No NFT rewards. Reputation here is earned by protecting others.

## Questions?

- **Technical**: Open a Discussion with `[RFC]` prefix
- **Security**: Email security@sentinel-protocol.org (PGP key in repo)
- **General**: Discord #dev channel

## Code of Conduct

See [`CODE_OF_CONDUCT.md`](./CODE_OF_CONDUCT.md).

**tl;dr**: Be respectful. Assume good faith. No financial advice. No token shilling.

---

Thank you for building the shield.
