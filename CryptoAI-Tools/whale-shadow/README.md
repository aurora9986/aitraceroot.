---
AIGC:
    Label: "1"
    ContentProducer: 001191440300708461136T1XGW3
    ProduceID: 407dc6b6268ee64cc703ded1ecc0430e_6338f0af6db711f18805525400d9a7a1
    ReservedCode1: +IMQEsH9hl7wU1ugpRwxNrtEnfE698bwndAO+hnv9wqkr/X6a74Lz9PJa+g99mqC9pXI7vttkt2fc1CcFgLfZwnMaH4n2mwr8Wm41ATSfRG062CLgpJRKKPkngHV9R0zht0IfsApKUbHlBgLRPVahU7ywb3WYn+iYIcAxXg/4PY3jH+N9KFp5NPSMzk=
    ContentPropagator: 001191440300708461136T1XGW3
    PropagateID: 407dc6b6268ee64cc703ded1ecc0430e_6338f0af6db711f18805525400d9a7a1
    ReservedCode2: +IMQEsH9hl7wU1ugpRwxNrtEnfE698bwndAO+hnv9wqkr/X6a74Lz9PJa+g99mqC9pXI7vttkt2fc1CcFgLfZwnMaH4n2mwr8Wm41ATSfRG062CLgpJRKKPkngHV9R0zht0IfsApKUbHlBgLRPVahU7ywb3WYn+iYIcAxXg/4PY3jH+N9KFp5NPSMzk=
---

# Whale Shadow

[![Concept](https://img.shields.io/badge/status-concept-orange)](https://github.com/crypto-ai-tools/whale-shadow)
[![License](https://img.shields.io/badge/license-MIT-blue)](LICENSE)
[![Discussions](https://img.shields.io/badge/discussions-welcome-green)](https://github.com/crypto-ai-tools/whale-shadow/discussions)

### On-Chain Intelligence Radar — Know Before It Moves

> *The whale doesn't DM you. But its shadow is visible.*

Whale Shadow is a real-time on-chain intelligence radar. It does not tell you what to buy. It does not copy-trade any address. It simply shows you what's happening **before** the chart moves.

---

## Table of Contents

- [The Problem](#the-problem)
- [What Whale Shadow Does](#what-whale-shadow-does)
- [Architecture](#architecture)
- [Signal Categories](#signal-categories)
- [Anomaly Detection Engine](#anomaly-detection-engine)
- [Installation & Quick Start](#installation--quick-start)
- [Usage Examples](#usage-examples)
- [API Reference](#api-reference)
- [Comparison](#comparison)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [FAQ](#faq)

---

## The Problem

Every crypto trader lives with one anxiety: *someone knows something I don't.*

- A whale moves 8,000 ETH to Binance at 2 AM. You find out 4 hours later on Twitter.
- A liquidity pool suddenly drains 60% of its TVL. You see the red candle first, then try to figure out why.
- A CEX cold wallet silent for 3 years suddenly wakes up. You never notice.

The information exists on-chain. The problem is **nobody is watching everything, everywhere, all at once.**

---

## What Whale Shadow Does

```
┌──────────────────────────────────────────────────────────────┐
│                     WHALE SHADOW                              │
│                                                               │
│   ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│   │   Ethereum  │  │   Solana    │  │    Base     │  ...     │
│   └──────┬──────┘  └──────┬──────┘  └──────┬──────┘         │
│          │                │                │                  │
│          └────────────────┼────────────────┘                  │
│                           ▼                                   │
│              ┌────────────────────────┐                      │
│              │    AI ANOMALY ENGINE   │                      │
│              │  • Whale movements     │                      │
│              │  • LP changes          │                      │
│              │  • CEX flows           │                      │
│              │  • Significance score  │                      │
│              └───────────┬────────────┘                      │
│                          ▼                                    │
│              ┌────────────────────────┐                      │
│              │   LIVE DASHBOARD        │                      │
│              │   Whale Activity Feed   │                      │
│              │   LP Health Monitor     │                      │
│              │   CEX Flow Map          │                      │
│              │   Anomaly Heat Map      │                      │
│              └────────────────────────┘                      │
└──────────────────────────────────────────────────────────────┘
```

---

## Architecture

### System Overview

```
┌─────────────────────────────────────────────────────────────┐
│                    DATA INGESTION LAYER                       │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐    │
│  │Eth Node  │  │Sol Node  │  │Base Node │  │Arb Node  │... │
│  │(WebSocket)│ │(WebSocket)│ │(WebSocket)│ │(WebSocket)│   │
│  └────┬─────┘  └────┬─────┘  └────┬─────┘  └────┬─────┘    │
├───────┼─────────────┼─────────────┼─────────────┼──────────┤
│                    STREAM PROCESSING                          │
│  ┌──────────────────────────────────────────────────────┐   │
│  │                Apache Kafka / Redpanda                │   │
│  │  ┌──────────┐ ┌──────────┐ ┌──────────┐              │   │
│  │  │TX Stream │ │Log Stream│ │Block Stream│            │   │
│  │  └────┬─────┘ └────┬─────┘ └────┬─────┘              │   │
│  └───────┼────────────┼────────────┼────────────────────┘   │
├──────────┼────────────┼────────────┼────────────────────────┤
│                    DETECTION ENGINE                           │
│  ┌──────────────────────────────────────────────────────┐   │
│  │  ┌────────────┐  ┌───────────┐  ┌──────────────┐    │   │
│  │  │  Address   │  │  Pattern  │  │  Statistical │    │   │
│  │  │  Labeler   │  │  Matcher  │  │  Anomaly     │    │   │
│  │  └─────┬──────┘  └─────┬─────┘  └──────┬───────┘    │   │
│  │        └───────────────┼───────────────┘             │   │
│  │                        ▼                              │   │
│  │              ┌──────────────────┐                    │   │
│  │              │  Anomaly Scorer  │                    │   │
│  │              │  (1-100 scale)   │                    │   │
│  │              └────────┬─────────┘                    │   │
│  └───────────────────────┼──────────────────────────────┘   │
├──────────────────────────┼──────────────────────────────────┤
│                          ▼                                   │
│                    ALERT & UI LAYER                          │
│  ┌──────────┐ ┌──────────────┐ ┌────────────┐ ┌─────────┐ │
│  │   CLI    │ │ Web Dashboard│ │Discord Bot │ │Telegram │ │
│  └──────────┘ └──────────────┘ └────────────┘ └─────────┘ │
└─────────────────────────────────────────────────────────────┘
```

---

## Signal Categories

### 1. Whale Movement Tracking

| Signal | Data Source | Refresh Rate | Significance Weight |
|---|---|---|---|
| Top-100 holder transfers | Etherscan Labels API | Real-time | 85/100 |
| Exchange deposit >$1M | Internal TX traces | Real-time | 78/100 |
| CEX cold wallet activation | Custom address DB | Real-time | 92/100 |
| Bridge volume spike (>3σ) | Bridge contract events | Per block | 65/100 |
| Dormant whale awakening (>2yr) | Historical activity DB | Real-time | 88/100 |

### 2. LP Health Monitoring

| Signal | Detection | Significance |
|---|---|---|
| TVL drop >20% in 1h | Time-series anomaly detection | 75/100 |
| Single LP removing >50% | Event log analysis | 82/100 |
| LP concentration risk (>1 holder >40%) | Ownership analysis | 60/100 |
| Fee tier migration | Factory contract events | 40/100 |

### 3. Smart Money & Deployer Activity

| Signal | Method | Significance |
|---|---|---|
| Known rug deployer creates contract | Deployer reputation DB | 95/100 |
| Smart money accumulation pattern | Time-series clustering | 70/100 |
| Insider wallet activity before announcement | Cross-reference with news events | 90/100 |
| Flash loan >$10M detected | Event signature matching | 72/100 |

---

## Anomaly Detection Engine

### How It Works

Whale Shadow's AI engine is not a simple threshold system. It uses a combination of techniques:

1. **Statistical Profiling**: Every tracked address has a behavioral baseline — mean transaction size, frequency, counterparty set, time-of-day patterns.
2. **Z-score Triggering**: When a transaction exceeds 3σ from the address's historical mean, it's flagged.
3. **Cross-Reference Scoring**: A whale moving to Binance at 2 AM scores higher than the same move at 2 PM.
4. **Graph Propagation**: An anomaly on one address propagates risk scores to its known counterparties.

```python
# Conceptual: Anomaly scoring pipeline
from whaleshadow.engine import AnomalyEngine, Alert

engine = AnomalyEngine(
    chains=["ethereum", "solana", "base"],
    threshold=50  # Only alert on score >= 50
)

@engine.on_anomaly
def handle_alert(alert: Alert):
    print(f"[{alert.chain}] Score {alert.score}/100: {alert.summary}")
    # >>> [ethereum] Score 88/100: Whale 0xABC... moved
    #     12,500 ETH to Binance at 02:17 UTC
    #     (Last move: 347 days ago, avg size: 450 ETH)

engine.start()
```

### Score Interpretation

| Score Range | Meaning | Action |
|---|---|---|
| 1-30 | Noise — normal activity | Ignore |
| 31-50 | Minor deviation — worth noting | Log only |
| 51-70 | Significant anomaly — unusual behavior | Push notification |
| 71-90 | Major anomaly — likely market-moving | Alert + sound |
| 91-100 | Critical — potential black swan event | All channels |

---

## Installation & Quick Start

### Prerequisites

| Dependency | Version | Purpose |
|---|---|---|
| Python | ≥3.11 | Core engine |
| Node.js | ≥20 LTS | Web dashboard |
| Docker | ≥24 | Kafka + DB containers |
| PostgreSQL | ≥15 | Historical data |
| Redis | ≥7 | Real-time cache |

### Install

```bash
git clone https://github.com/crypto-ai-tools/whale-shadow.git
cd whale-shadow
pip install -r requirements.txt
cp .env.example .env
# Edit .env: add RPC URLs (Alchemy, Infura, Helius for Solana, etc.)
docker compose up -d
python -m whaleshadow.cli init
```

### First Run

```bash
# Start monitoring Ethereum mainnet
whaleshadow watch ethereum

# You should see streaming output:
# [14:32:01] Chain: ETH | Block: 19,847,231 | Processing...
# [14:32:03] 🔔 Score 72 | 0xAbC... → Binance | 4,200 ETH ($16.2M)
# [14:32:05] 🔔 Score 55 | Uniswap V3 ETH/USDC pool: TVL -18% in 1h
# [14:32:08] 🔴 Score 91 | CEX Cold Wallet dormant 1,247 days → ACTIVE
```

---

## Usage Examples

### CLI: Watch Mode

```bash
# Monitor all chains, score threshold 60
whaleshadow watch --chains eth,sol,base --threshold 60

# Monitor only whale movements, score threshold 40
whaleshadow watch --signal whale --threshold 40

# Export alerts to JSON
whaleshadow watch --chains eth --threshold 50 --output alerts.jsonl
```

### CLI: Query Historical Anomalies

```bash
# Get last 24h of anomalies for Ethereum
whaleshadow history --chain eth --hours 24

# Get anomalies involving a specific address
whaleshadow history --address 0xYourWallet...

# Get top-10 anomalies this week
whaleshadow history --chain eth --days 7 --limit 10 --sort score
```

### Web Dashboard

The dashboard provides four views:

- **Whale Activity Feed**: Real-time timeline, filterable by chain, size, type.
- **LP Health Monitor**: Visual grid — Green (stable), Yellow (pulling), Red (draining). Each tile shows TVL, 24h Δ, risk score.
- **CEX Flow Map**: Sankey diagram of capital flows between CEX wallets, bridges, and known whale addresses.
- **Anomaly Heat Map**: Everything weird right now, ranked by significance.

### Discord / Telegram Alerts

```yaml
# alerts.yaml
discord:
  webhook_url: "https://discord.com/api/webhooks/..."
  channels:
    - name: whale-alerts
      threshold: 70
    - name: lp-health
      threshold: 50

telegram:
  bot_token: "123456:ABC-DEF..."
  chat_id: "-1001234567890"
  threshold: 60
```

---

## API Reference

| Endpoint | Method | Description |
|---|---|---|
| `/api/v1/anomalies` | GET | List recent anomalies (paginated) |
| `/api/v1/anomalies/live` | WebSocket | Stream live anomalies |
| `/api/v1/anomalies/{id}` | GET | Get anomaly details |
| `/api/v1/whales` | GET | List tracked whale addresses |
| `/api/v1/whales/{address}` | GET | Get whale profile + history |
| `/api/v1/whales/{address}/subscribe` | POST | Subscribe to whale alerts |
| `/api/v1/pools` | GET | List monitored liquidity pools |
| `/api/v1/pools/{address}/health` | GET | Get pool health metrics |
| `/api/v1/heatmap` | GET | Current anomaly heatmap data |
| `/api/v1/chains` | GET | List supported chains and status |

---

## Comparison

| | Nansen | Arkham | DexScreener | Whale Alert | **Whale Shadow** |
|---|---|---|---|---|---|
| Focus | Smart money labels | Entity de-anon | Token charts | TX reporting | **Anomaly-first radar** |
| Real-time | Yes | Yes | Yes | Delayed | **Yes, multi-chain** |
| AI anomaly detection | Limited | No | No | No | **Full ML engine** |
| LP monitoring | No | No | Yes | No | **Yes, real-time** |
| Configurable alerts | Some | No | No | No | **Threshold-based** |
| Free | No ($150/mo) | No | Yes | Yes | **Yes, open source** |
| Self-hosted | No | No | No | No | **Yes** |

---

## Roadmap

| Phase | Name | Features | ETA |
|---|---|---|---|
| **1** | Shadow | Multi-chain whale tracking. Basic anomaly detection. Terminal UI. | Concept |
| **2** | Depth | LP health monitoring. CEX flow mapping. ML anomaly scoring. Discord/Telegram bots. | Concept |
| **3** | Predator | Predictive alerts. Cross-chain pattern recognition. Historical anomaly replay. | Concept |
| **4** | Ecosystem | Community-contributed alert rules. Plugin system. Custom signal definitions. Mobile app. | Concept |

---

## Contributing

```bash
git clone https://github.com/crypto-ai-tools/whale-shadow.git
cd whale-shadow
pip install -r requirements-dev.txt
pre-commit install
docker compose -f docker-compose.dev.yml up -d
pytest tests/
```

We need: **multi-chain RPC integration**, **ML model training on whale behavior**, **real-time dashboard frontend**, **Discord/Telegram bot development**, **address labeling and entity clustering**.

---

## FAQ

**Q: How is this different from Whale Alert?**
A: Whale Alert reports what already happened, often delayed. Whale Shadow watches in real-time and surfaces anomalies *before* they become news. Also tracks LP changes, contract activity, and patterns Whale Alert ignores.

**Q: Do I need to run a full node?**
A: No. Connect to public RPC endpoints (Alchemy, Infura, Helius). Free tiers work for personal use.

**Q: Is this just a blockchain explorer with filters?**
A: No. Explorers show raw data. Whale Shadow's AI engine learns "normal" and only surfaces deviations. You don't scroll blocks; you see the 3 things that matter.

**Q: How many chains are supported?**
A: Phase 1 targets Ethereum, Solana, and Base. Arbitrum, Optimism, Polygon, and Avalanche in Phase 2.

**Q: Can I add custom signals?**
A: Phase 4 will support a plugin system for community-contributed signal definitions. Until then, all signals are built-in.

---

## License

MIT — see [LICENSE](LICENSE).

---

*The whale moves in silence. Its shadow doesn't.*
*（内容由AI生成，仅供参考）*
