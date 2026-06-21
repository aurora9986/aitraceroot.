---
AIGC:
    Label: "1"
    ContentProducer: 001191440300708461136T1XGW3
    ProduceID: 407dc6b6268ee64cc703ded1ecc0430e_6264173c6db711f1a0095254002afed2
    ReservedCode1: WBoAXGyhMEiW2sbY5R3Bb7KbBDhF/rTZlJ32k78HpnYQ2DXgQEQNsN4Xs4MEBMGZUFQYJ1N9lPMlHRk4XZPx/rqy5G+Hxdl5ik03kSGf1LWI7IJzb5nwbUmoHoytQARiPElITHGs2CTJsqgKrf/94s7X8cecqE9BwmWdtsHaPuOL8oT2vWLo87bd2wU=
    ContentPropagator: 001191440300708461136T1XGW3
    PropagateID: 407dc6b6268ee64cc703ded1ecc0430e_6264173c6db711f1a0095254002afed2
    ReservedCode2: WBoAXGyhMEiW2sbY5R3Bb7KbBDhF/rTZlJ32k78HpnYQ2DXgQEQNsN4Xs4MEBMGZUFQYJ1N9lPMlHRk4XZPx/rqy5G+Hxdl5ik03kSGf1LWI7IJzb5nwbUmoHoytQARiPElITHGs2CTJsqgKrf/94s7X8cecqE9BwmWdtsHaPuOL8oT2vWLo87bd2wU=
---

# Soulbound Wallet

[![Concept](https://img.shields.io/badge/status-concept-orange)](https://github.com/crypto-ai-tools/soulbound-wallet)
[![License](https://img.shields.io/badge/license-MIT-blue)](LICENSE)
[![Discussions](https://img.shields.io/badge/discussions-welcome-green)](https://github.com/crypto-ai-tools/soulbound-wallet/discussions)

### The First On-Chain Immortal Agent

> *Not your keys, not your crypto. Not your soul, not your legacy.*

A **Soulbound Wallet** is not a wallet — it is an AI personality permanently bonded to a blockchain address. It trades like you. It protects like you. And when you're gone, it keeps going.

---

## Table of Contents

- [The Problem](#the-problem)
- [What is a Soulbound Wallet?](#what-is-a-soulbound-wallet)
- [Architecture](#architecture)
- [Core Modules](#core-modules)
- [Immortality Protocol](#immortality-protocol)
- [Installation & Quick Start](#installation--quick-start)
- [Usage Examples](#usage-examples)
- [API Reference](#api-reference)
- [Security Model](#security-model)
- [Use Cases](#use-cases)
- [Comparison](#comparison)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [FAQ](#faq)

---

## The Problem

Every crypto wallet today is a **dead object** — a deterministic signer that does exactly what it's told, nothing more.

- Your wallet won't stop you from signing a phishing contract at 3 AM.
- Your wallet won't claim an airdrop you're eligible for but forgot about.
- Your wallet won't manage your portfolio while you sleep.
- Your wallet won't outlive you.

Meanwhile, AI can already learn your risk appetite, trading patterns, and conviction thresholds — and act on them autonomously. But no one has bound that intelligence to a **non-custodial, on-chain identity**.

---

## What is a Soulbound Wallet?

```
┌──────────────────────────────────────────────────┐
│                   YOU (Human)                     │
│                        │                          │
│                Train / Authorize                  │
│                        ▼                          │
│   ┌──────────────────────────────────────────┐   │
│   │           SOULBOUND AGENT                 │   │
│   │                                           │   │
│   │   ┌──────────┐ ┌────────┐ ┌──────────┐   │   │
│   │   │ Persona  │ │ Guard  │ │  Trade   │   │   │
│   │   │ Engine   │ │ Mode   │ │  Engine  │   │   │
│   │   └──────────┘ └────────┘ └──────────┘   │   │
│   │                                           │   │
│   │           ▲ MPC / TEE Signing ▲           │   │
│   └──────────────────────────────────────────┘   │
│                        │                          │
│                Signs transactions                 │
│                        ▼                          │
│   ┌──────────────────────────────────────────┐   │
│   │           ON-CHAIN ADDRESS                │   │
│   │       (Soulbound, non-transferable)       │   │
│   └──────────────────────────────────────────┘   │
└──────────────────────────────────────────────────┘
```

---

## Architecture

### Three-Layer Design

```
┌────────────────────────────────────────────────────────┐
│                     LAYER 3: UI                         │
│  ┌──────────┐  ┌──────────┐  ┌──────────────────┐     │
│  │   CLI    │  │  Web App │  │  Telegram Bot    │     │
│  └────┬─────┘  └────┬─────┘  └────────┬─────────┘     │
├───────┼─────────────┼─────────────────┼───────────────┤
│                     LAYER 2: AGENT                     │
│  ┌────────────────────────────────────────────────┐   │
│  │              Soulbound Agent Core               │   │
│  │                                                 │   │
│  │  ┌────────────┐ ┌──────────┐ ┌──────────────┐  │   │
│  │  │  Persona   │ │  Guard   │ │   Trade      │  │   │
│  │  │  Engine    │ │  Mode    │ │   Engine     │  │   │
│  │  └─────┬──────┘ └────┬─────┘ └──────┬───────┘  │   │
│  │        │              │               │         │   │
│  │  ┌─────┴──────────────┴───────────────┴──────┐  │   │
│  │  │           Memory & State Store             │  │   │
│  │  │  (Vector DB + Redis + PostgreSQL)          │  │   │
│  │  └────────────────────────────────────────────┘  │   │
│  └───────────────────────┬──────────────────────────┘   │
├──────────────────────────┼──────────────────────────────┤
│                          │                              │
│                     LAYER 1: SIGNING                    │
│  ┌──────────────────────────────────────────────────┐  │
│  │          MPC / TEE Signing Module                 │  │
│  │  ┌──────────┐  ┌──────────────┐  ┌────────────┐  │  │
│  │  │ MPC Node │  │ TEE Enclave  │  │ HSM Backup │  │  │
│  │  └──────────┘  └──────────────┘  └────────────┘  │  │
│  └──────────────────────────────────────────────────┘  │
└────────────────────────────────────────────────────────┘
```

### Transaction Data Flow

```
User Action ──▶ Persona Engine (evaluate intent) ──▶ Guard Mode (risk check)
                                                        │
                                            ┌───────────┴───────────┐
                                            ▼                       ▼
                                        ALLOW                   BLOCK
                                            │                       │
                                            ▼                       ▼
                                    Trade Engine            Alert User
                                            │              (explain why)
                                            ▼
                                    MPC Signing ──▶ On-Chain TX
```

---

## Core Modules

### 1. Persona Engine —— *Your On-Chain DNA*

The Persona Engine learns who you are as a trader by ingesting your complete on-chain history.

**Input Signals**:

| Signal Category | Features Extracted |
|---|---|
| **Transaction History** | Token preferences, DEX usage pattern, trade size distribution, holding duration |
| **Time Patterns** | Active trading hours, timezone inference, weekend vs. weekday behavior |
| **Risk Behavior** | Maximum leverage used, liquidation history, stop-loss discipline |
| **Social Graph** | Counterparty analysis, contract interaction clusters, MEV exposure |
| **PnL Profile** | Win rate, profit factor, max drawdown tolerance, FOMO pattern detection |

**Output**: A 768-dimensional **Soulprint Vector** — a compressed mathematical representation of your trading personality.

```python
# Conceptual: Generating a Soulprint
from soulbound.persona import PersonaEngine

engine = PersonaEngine(rpc_url="https://eth-mainnet.g.alchemy.com/v2/YOUR_KEY")
soulprint = engine.analyze(address="0xYourWallet...")

print(f"Risk tolerance:  {soulprint.risk_score}/100")
print(f"HODL conviction: {soulprint.hold_conviction}/100")
print(f"MEME degeneracy:  {soulprint.meme_score}/100")
print(f"Vector:           {soulprint.vector[:5]}...")
```

### 2. Guard Mode —— *Your On-Chain Firewall*

Guard Mode is a real-time transaction firewall that evaluates every outgoing transaction before signing. It **cannot** be disabled — that's the point.

**Detection Capabilities**:

| Threat Type | Detection Method | Response Time |
|---|---|---|
| **Phishing Contracts** | Address reputation DB + bytecode similarity to known scams | <50ms |
| **Honeypot Tokens** | Simulate sell execution on fork before real approval | <200ms |
| **Rugpull Detection** | LP lock status check + deployer history + ownership renounce | <100ms |
| **Sandwich Attack** | Mempool scan for bundler patterns targeting your TX | <100ms |
| **Unusual Value** | Amount deviation from historical mean (Z-score > 3) | <10ms |
| **Untrusted Target** | First-time interaction with unknown contract + high value | <10ms |
| **Drunk Trade** | Time anomaly + high value + low conviction pair | <10ms |

```python
# Conceptual: Guard Mode in action
from soulbound.guard import GuardMode

guard = GuardMode(soulprint=soulprint, strictness="paranoid")

tx = {
    "to": "0xUnverifiedContract...",
    "value": 5.0,   # ETH
    "data": "0xa9059cbb...",
    "time": "03:17 AM"
}

result = guard.evaluate(tx)
# >>> {
# >>>   "verdict": "BLOCKED",
# >>>   "reasons": [
# >>>     "Unverified contract on Etherscan",
# >>>     "Late-night anomaly: outside normal trading window",
# >>>     "High value: exceeds typical 3AM transaction size"
# >>>   ],
# >>>   "override_available": False
# >>> }
```

### 3. Trade Engine —— *Your Autonomous Trader*

Executes strategies within user-defined guardrails. Does not blindly copy-trade — only follows smart money that matches your risk profile.

**Execution Modes**:

| Mode | Description | User Involvement |
|---|---|---|
| **Manual** | User initiates every trade. Agent provides Guard Mode only. | Full |
| **Advisory** | Agent suggests trades with reasoning. User approves or rejects. | Approve/Reject |
| **Semi-Autonomous** | Agent executes within limits. Flags large trades for approval. | Threshold-based |
| **Full Autonomous** | Agent trades freely within risk parameters. No approval. | None (Immortality Mode) |

```python
# Conceptual: Semi-autonomous trading
from soulbound.trade import TradeEngine, RiskProfile

risk = RiskProfile(
    max_position_size=5.0,
    max_daily_volume=20.0,
    max_leverage=2.0,
    allowed_tokens=["ETH", "USDC", "WBTC", "LINK"],
    stop_loss_pct=15.0,
    require_approval_above=2.0
)

engine = TradeEngine(soulprint=soulprint, risk=risk)
engine.start()
```

---

## Immortality Protocol

How does an Agent keep signing after the human is gone?

```
Human Alive                    Human Deceased
─────────────                  ───────────────
     │                               │
     │ Heartbeat signal              │ Heartbeat stops
     │ (daily on-chain tx)           │
     ▼                               ▼
┌─────────────┐               ┌─────────────────┐
│   ACTIVE    │──────────────▶│   IMMORTALITY   │
│   MODE      │   30d no tx   │   MODE           │
│             │               │                  │
│  Agent asks │               │  Agent acts      │
│  for confirm│               │  autonomously    │
└─────────────┘               └─────────────────┘
```

### Stage-by-Stage

| Day | Event |
|---|---|
| **Day 0** | Human makes daily heartbeat TX. All normal. |
| **Day 1-6** | Heartbeat missed. Agent logs warning internally. |
| **Day 7** | Agent escalates: sends email, Telegram DM, on-chain message to emergency contacts. |
| **Day 8-29** | Continued silence. Agent reduces position sizes, moves to conservative mode. |
| **Day 30** | **Immortality Mode activated.** Agent executes Last Will Contract from IPFS. |

### Last Will Contract

```solidity
// Conceptual: Last Will Contract structure
struct LastWill {
    address[] beneficiaries;
    uint256[] allocations;      // Percentage per beneficiary
    bool continue_trading;
    RiskProfile immortal_profile;
    uint256 charity_pct;
    address charity_address;
    string ipfs_memoir;          // IPFS hash of farewell message
}
```

> *"When I die, my wallet keeps trading. It will donate 5% of monthly profits to cancer research. It will never sell my genesis NFT. I'm not immortal — but my strategy is."*

---

## Installation & Quick Start

### Prerequisites

| Dependency | Version | Purpose |
|---|---|---|
| Python | ≥3.11 | Core runtime |
| Node.js | ≥20 LTS | Web dashboard |
| Docker | ≥24 | Containerized deployment |
| PostgreSQL | ≥15 | State persistence |
| Redis | ≥7 | Caching & pub/sub |

### Install

```bash
git clone https://github.com/crypto-ai-tools/soulbound-wallet.git
cd soulbound-wallet
pip install -r requirements.txt
cd dashboard && npm install && cd ..
cp .env.example .env
docker compose up -d
python -m soulbound.cli init
```

### First Run

```bash
soulbound persona analyze 0xYourWalletAddress...

# Output:
#   Soulprint generated: soulprints/0xYourWallet...json
#   Risk tolerance: 72/100
#   Top DEX: Uniswap V3 (64% of volume)
#   Active hours: 09:00-23:00 UTC+8
#   MEME degeneracy score: 34/100

soulbound guard start --strictness cautious
soulbound trade start --mode advisory --risk-profile conservative
```

---

## Usage Examples

### Phishing Protection

```bash
$ soulbound guard simulate --tx 0xabcdef...

╔══════════════════════════════════════════════╗
║           GUARD MODE — SIMULATION             ║
╠══════════════════════════════════════════════╣
║                                                ║
║  To:     0x1234...UnverifiedContract            ║
║  Value:  2.5 ETH                                ║
║                                                ║
║  🔴 Contract unverified on Etherscan            ║
║  🔴 Bytecode similarity to known scam: 94%      ║
║  🔴 Domain registered 3 days ago                ║
║  🔴 No previous interactions in your history    ║
║                                                ║
║  VERDICT: 🚫 BLOCKED                            ║
║  This matches "ZerionClaim.eth" phishing.      ║
║  You just saved 2.5 ETH.                        ║
╚══════════════════════════════════════════════╝
```

### Portfolio Rebalancing

```bash
$ soulbound trade rebalance --target "40% ETH, 30% USDC, 20% BTC, 10% LINK"

Analyzing current portfolio...
  ETH: 62.3% (target 40%) → SELL 2.8 ETH
  USDC: 8.1% (target 30%)  → BUY 21,900 USDC
  BTC: 18.5% (target 20%)  → BUY 0.15 BTC
  LINK: 11.1% (target 10%) → SELL 110 LINK

Simulating execution...
  Expected slippage: 0.12%
  Estimated gas: 0.008 ETH

Execute? [y/N]
```

---

## API Reference

| Endpoint | Method | Description |
|---|---|---|
| `/api/v1/persona/analyze` | POST | Generate Soulprint from address |
| `/api/v1/persona/{address}` | GET | Get existing Soulprint |
| `/api/v1/persona/compare` | POST | Compare two Soulprints (cosine similarity) |
| `/api/v1/guard/evaluate` | POST | Evaluate transaction before signing |
| `/api/v1/guard/simulate` | POST | Simulate TX execution on fork |
| `/api/v1/guard/rules` | GET | List active guard rules |
| `/api/v1/guard/history` | GET | Blocked transaction history |
| `/api/v1/trade/start` | POST | Start trading engine |
| `/api/v1/trade/stop` | POST | Stop trading engine |
| `/api/v1/trade/status` | GET | Engine status and open positions |
| `/api/v1/trade/approve/{tx_id}` | POST | Approve pending trade |

---

## Security Model

### Threat Model

| Attack Vector | Mitigation |
|---|---|
| **Agent key compromise** | MPC signing — no single key exists. Split across 3 independent nodes. |
| **TEE side-channel attack** | Regular TEE firmware updates. Attestation verification on every signing. |
| **Model poisoning** | Persona Engine uses only historical data, not live adversarial inputs. |
| **Sybil heartbeat spoofing** | Heartbeat requires hardware wallet + specific nonce. Cannot be replayed. |
| **Forced Immortality** | Only activates after 30 days. Emergency contacts notified at day 7. |
| **Agent takeover** | Risk parameters immutable once set. Cannot increase position sizes or add tokens. |

⚠️ **This is a conceptual project. Do not use with real funds until fully audited.**

---

## Comparison

| | MetaMask | Gnosis Safe | Bananagun | **Soulbound** |
|---|---|---|---|---|
| Custody | Self | Multi-sig | Bot | Self |
| AI-powered | No | No | No | **Yes** |
| Phishing protection | No | Partial | No | **Full AI firewall** |
| Personality learning | No | No | No | **Learns from history** |
| Posthumous operation | No | No | No | **Yes** |
| Transferable | Yes | Yes | Yes | **No** |
| Open source | Yes | Yes | No | **Yes** |

---

## Roadmap

| Phase | Milestone | ETA |
|---|---|---|
| **Phase 1: Soulprint** | On-chain behavior profiling. CLI tool. Public API. | Concept |
| **Phase 2: Guardian** | MPC/TEE signer + AI firewall. Phishing detection. | Concept |
| **Phase 3: Autopilot** | Trade Engine. Semi-autonomous mode. | Concept |
| **Phase 4: Immortality** | Heartbeat + Last Will Contract. Emergency contacts. | Concept |
| **Phase 5: DAO** | Token-gated Agent customization. Plugin marketplace. | Concept |

---

## Contributing

We welcome cryptographers, AI/ML engineers, smart contract devs, and security researchers.

```bash
git clone https://github.com/crypto-ai-tools/soulbound-wallet.git
cd soulbound-wallet
pip install -r requirements-dev.txt
pre-commit install
docker compose -f docker-compose.dev.yml up -d
pytest tests/
```

Areas seeking contributors: **MPC key management**, **on-chain behavior clustering**, **gas-optimized Last Will Contract**, **threat modeling**, **dashboard UX**.

---

## FAQ

**Q: Can someone force my Agent to send funds?**
A: No. Risk parameters are immutable once set. Neither you nor the Agent can override them.

**Q: What if the AI makes a bad trade?**
A: Same as when you do. But the AI doesn't FOMO, revenge-trade, or ape into rugs at 3 AM.

**Q: Is this a smart contract wallet?**
A: Wallet-agnostic. Works with MetaMask, Ledger, Trezor, or any MPC wallet.

**Q: Can I kill my Agent?**
A: Yes. Revoke signing permission, and the Agent is dead forever.

**Q: Can I transfer to a new address?**
A: No. "Soulbound" means permanently bonded. Create a new Agent on the new address.

---

## License

MIT — see [LICENSE](LICENSE).

---

*The body dies. The wallet never does.*
*（内容由AI生成，仅供参考）*
