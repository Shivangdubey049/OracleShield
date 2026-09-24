# 🛡️ OracleShield

### AI-Powered Network Attack Detection, Forecasting & Security Audit

<p align="center">
  <b>OracleShield</b> is a predictive cybersecurity platform built for <b>SIH 2026 — Problem Statement 26153</b>.
  <br/>
  It combines machine-learning detection, temporal network-state modelling, forward threat forecasting,
  MITRE ATT&CK mapping, threat memory, explainability, and tamper-evident security auditing in one SOC-oriented dashboard.
</p>

<p align="center">
  <a href="https://oracleshield.streamlit.app/">
    <img src="https://img.shields.io/badge/🚀_Live_Demo-OracleShield-FF4B4B?style=for-the-badge" alt="Live Demo">
  </a>
  <a href="https://github.com/Shivangdubey049/OracleShield">
    <img src="https://img.shields.io/badge/GitHub-Repository-181717?style=for-the-badge&logo=github" alt="GitHub">
  </a>
</p>

---

## 🎯 The Idea

Traditional intrusion detection generally answers:

> **“What is happening right now?”**

OracleShield is designed to additionally ask:

> **“Given the current network state, how could the threat evolve next?”**

The system converts network observations into structured state representations, detects the current threat, models temporal behaviour, performs forward simulation, estimates progression risk, maps the result to security context, and records important events for audit.

### Core security loop

**Detect → Understand → Forecast → Explain → Audit**

---

## ✨ Key Capabilities

| Capability | What OracleShield does |
|---|---|
| 🔍 **AI Detection** | Random Forest-based classification of normal and network attack traffic |
| 🧠 **World Model** | Temporal modelling of network-state transitions using neural sequence models |
| 🔮 **Forward Forecasting** | Autoregressive multi-step rollout of possible future network states |
| 📈 **Risk Estimation** | Combines current threat information with forecasting signals to estimate progression risk |
| 🧬 **Threat Memory** | Maintains state prototypes, transitions, novelty and drift information |
| 🎯 **MITRE ATT&CK** | Maps detected behaviour to ATT&CK-oriented techniques/stages and defensive context |
| 💡 **Explainability** | Exposes state-feature drivers and SHAP-based detector evidence |
| 🔐 **Security Audit** | Cryptographically links security records and supports integrity/tamper verification |
| 🖥️ **SOC Dashboard** | Streamlit interface for detection, forecasting, evidence and audit workflows |
| 📡 **Network Telemetry** | Supports flow/packet-oriented processing, replay and PCAP-oriented workflows |
| 🔄 **Adaptive Memory** | Tracks changing network behaviour while keeping model adaptation controlled |

---

## 🏗️ Architecture

```text
                         ┌──────────────────────────┐
                         │     NETWORK TELEMETRY    │
                         │  Live / PCAP / Flow Data │
                         └────────────┬─────────────┘
                                      │
                                      ▼
                         ┌──────────────────────────┐
                         │   PREPROCESSING ENGINE   │
                         │ Cleaning • Scaling •      │
                         │ Feature / State Encoding │
                         └────────────┬─────────────┘
                                      │
                                      ▼
                         ┌──────────────────────────┐
                         │    DETECTION ENGINE      │
                         │     Random Forest        │
                         │ Normal / DoS / Probe /   │
                         │ R2L / U2R                │
                         └────────────┬─────────────┘
                                      │
                                      ▼
                    ┌──────────────────────────────────┐
                    │       TEMPORAL WORLD MODEL       │
                    │   LSTM / Transformer support     │
                    │                                  │
                    │  State t → State t+1 → ... → t+n│
                    └────────────────┬─────────────────┘
                                     │
                                     ▼
                         ┌──────────────────────────┐
                         │   FORECAST & RISK LAYER  │
                         │ Progression • Confidence │
                         │ Novelty • Drift • Risk   │
                         └────────────┬─────────────┘
                                      │
                    ┌─────────────────┼─────────────────┐
                    ▼                 ▼                 ▼
          ┌────────────────┐ ┌────────────────┐ ┌────────────────┐
          │ Threat Memory  │ │ MITRE ATT&CK   │ │ Explainability │
          │ State History  │ │ Mapping /      │ │ SHAP + Feature │
          │ & Transitions  │ │ Playbooks      │ │ Drivers        │
          └────────┬───────┘ └───────┬────────┘ └───────┬────────┘
                   └─────────────────┼──────────────────┘
                                     ▼
                         ┌──────────────────────────┐
                         │       AUDIT LEDGER       │
                         │ Hashing • Integrity •    │
                         │ Tamper Verification     │
                         └────────────┬─────────────┘
                                      │
                                      ▼
                         ┌──────────────────────────┐
                         │       SOC DASHBOARD      │
                         │ Detect → Forecast →      │
                         │ Explain → Audit          │
                         └──────────────────────────┘
```

---

## 🧠 How the Forecasting Works

OracleShield does not stop at a classification result.

For a sequence of network states:

```text
Sₜ → Sₜ₊₁ → Sₜ₊₂ → Sₜ₊₃ → ...
```

the World Model learns temporal relationships and predicts the next state.

The forecast can then be rolled forward:

```text
Current State
     │
     ▼
Predict Next State
     │
     ▼
Feed Prediction Back
     │
     ▼
Predict Future State
     │
     ▼
Repeat for Multiple Steps
     │
     ▼
Progression / Risk Estimate
```

This enables OracleShield to represent a threat as an **evolving process**, rather than treating every network observation as an isolated event.

---

## 🧪 Detection Layer

The current detection workflow supports the following categories:

- `normal`
- `DoS`
- `Probe`
- `R2L`
- `U2R`

The dashboard exposes more than a single accuracy value, including:

- Accuracy
- Macro Precision
- Macro Recall
- Macro F1
- Weighted F1
- Per-class precision / recall / F1
- Train/test class distribution

The current prototype uses an NSL-KDD-based dataset containing **148,517 records**, while preserving the original train/test membership.

---

## 🔮 Temporal World Model

OracleShield includes a temporal modelling layer for network-state forecasting.

### Supported modelling approach

- LSTM-based state-transition modelling
- Transformer / multi-head self-attention support in the implementation
- Sequence-based state windows
- Next-state prediction
- Attack-stage prediction
- Multi-step autoregressive rollout
- Cumulative progression-risk estimation

The goal is to move from:

```text
Attack Detected
```

toward:

```text
Attack Detected
      ↓
Current Network State
      ↓
Behavioural Change
      ↓
Possible Next State
      ↓
Future Progression Risk
```

---

## 🎯 MITRE ATT&CK Integration

OracleShield includes a MITRE-oriented security context layer.

The implementation exposes technique information such as:

- Technique ID
- Technique name
- Tactic
- Description
- Recommended automated action
- Mitigation / playbook context

Example technique mappings represented by the current implementation include:

| Technique | Context |
|---|---|
| `T1046` | Network Service Scanning |
| `T1498` | Network Denial of Service |
| `T1110` | Brute Force |
| `T1041` | Exfiltration Over C2 Channel |

> **Important:** MITRE mappings should be interpreted according to the evidence available from the underlying telemetry. Dataset attack labels are not automatically equivalent to ground-truth ATT&CK technique IDs.

---

## 🧬 Threat Memory

OracleShield maintains behavioural memory instead of treating every observation independently.

The memory layer can track:

- Persistent network-state prototypes
- State transitions
- Novelty
- Behavioural drift
- Historical threat context
- Adaptive state information

This helps the system distinguish between familiar behaviour and behaviour that is changing or becoming unusual.

---

## 💡 Explainability

A cybersecurity model is more useful when analysts can understand **why** an alert was produced.

OracleShield exposes:

- Network-state feature drivers
- Detector evidence
- SHAP-based explanations
- Predicted attack category
- Risk/progression information
- MITRE-oriented security context

The objective is to give analysts evidence alongside the prediction rather than presenting an unexplained score.

---

## 🔐 Security Audit & Integrity

Security decisions need an auditable trail.

OracleShield records security events using cryptographic integrity mechanisms.

The audit workflow supports:

```text
Security Event
      ↓
Cryptographic Record
      ↓
Previous-Record Link
      ↓
Integrity Verification
      ↓
Tamper Detection
```

The current implementation also includes a controlled tamper-simulation workflow and multi-node ledger/consensus components.

> **Prototype note:** The audit layer is intended to demonstrate tamper-evident security logging and distributed-ledger concepts. Production deployment would require hardened infrastructure, key management, node identity, persistent storage, and operational security controls.

---

## 🖥️ Dashboard

The Streamlit application is organized around security operations workflows including:

### 🚨 Command Center
Real-time/replayed telemetry, detection metrics, current threat state, progression risk and network defence status.

### 🧠 World Model
Network-state dynamics, temporal model information, next-state prediction and forecasting metrics.

### 🔐 Blockchain Audit
Security-event records, cryptographic integrity checks and tamper simulation.

### 📊 Evidence & Data
Detection metrics, per-class results, train/test distribution, MITRE technique information and implementation coverage.

---

## 📊 Prototype Evaluation

The current prototype exposes evaluation metrics directly in the dashboard rather than relying only on a headline accuracy figure.

Reported evaluation includes:

- Detection accuracy
- Macro precision
- Macro recall
- Macro F1
- Weighted F1
- Per-class metrics
- World-model metrics
- Next-state prediction error

The NSL-KDD-based prototype currently contains **148,517 records** and reports approximately **73.7% detection accuracy** on the difficult evaluation setting used by the project.

> Metrics are dataset- and evaluation-setting-specific. They should not be interpreted as real-world SOC detection rates.

---

## ⚠️ Research & Dataset Limitation

A major limitation is intentionally documented rather than hidden:

**NSL-KDD does not provide genuine timestamped packet telemetry for learning real chronological attacker progression.**

Therefore, temporal ordering in the current prototype is used as a reproducible modelling setup.

For stronger real-world forecasting, the next evaluation stage should use timestamped network telemetry such as:

- CIC-IDS2018
- CTU-13
- PCAP-derived traffic
- Flow records with real timestamps

This would allow the forecasting layer to learn richer temporal signals such as:

- Inter-arrival timing
- TCP behaviour
- Retransmissions
- Flow duration
- Traffic bursts
- Real attack timelines

---

## 🚀 Quick Start

### 1. Clone the repository

```bash
git clone https://github.com/Shivangdubey049/OracleShield.git
cd OracleShield
```

### 2. Create a virtual environment

#### Windows

```bash
python -m venv .venv
.venv\Scripts\activate
```

#### Linux / macOS

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Launch the Streamlit application

```bash
streamlit run app.py
```

Then open the local URL shown by Streamlit, usually:

```text
http://localhost:8501
```

> If your local checkout uses a different Streamlit entry file, run the project's configured application entry point instead.

---

## 🌐 Live Demo

Try the deployed prototype:

**https://oracleshield.streamlit.app/**

The dashboard is designed to demonstrate the complete security workflow:

```text
Telemetry
   ↓
Detection
   ↓
Threat Understanding
   ↓
Forecasting
   ↓
MITRE / Explainability
   ↓
Audit
```

---

## 🛠️ Technology Stack

| Layer | Technology |
|---|---|
| Language | Python |
| Web / SOC UI | Streamlit |
| Classical ML | scikit-learn |
| Detection Model | Random Forest |
| Temporal AI | PyTorch LSTM |
| Attention Model | Multi-Head Self-Attention Transformer support |
| Data Processing | Pandas, NumPy |
| Explainability | SHAP |
| Network Capture | Scapy / tshark-oriented workflows |
| Flow Processing | Flow tracking / state encoding |
| Security Context | MITRE ATT&CK |
| Audit | Cryptographic hashing / ledger components |
| Visualization | Streamlit charts / Plotly-oriented dashboard components |

---

## 📁 Repository Concept

The project is organized around the following logical components:

```text
OracleShield/
│
├── Application / Streamlit UI
├── Detection Engine
├── Preprocessing & State Encoding
├── World Model
├── Forecast / Rollout Engine
├── Threat Memory
├── MITRE Mapping
├── Explainability
├── Audit / Ledger
├── Data & Model Artifacts
├── Documentation
└── Configuration / Requirements
```

The exact file layout may evolve as the implementation develops.

---

## 🔄 End-to-End Workflow

```text
        ┌───────────────┐
        │ Network Data  │
        └───────┬───────┘
                ↓
        ┌───────────────┐
        │ Preprocessing │
        └───────┬───────┘
                ↓
        ┌───────────────┐
        │ 16-D Network  │
        │ State Vector  │
        └───────┬───────┘
                ↓
        ┌───────────────┐
        │ Random Forest │
        │   Detection   │
        └───────┬───────┘
                ↓
        ┌───────────────┐
        │ World Model   │
        │ LSTM / Trans. │
        └───────┬───────┘
                ↓
        ┌───────────────┐
        │ Multi-Step    │
        │ Forward Roll  │
        └───────┬───────┘
                ↓
        ┌───────────────┐
        │ Risk + Stage  │
        │  Forecasting  │
        └───────┬───────┘
                ↓
   ┌────────────┼────────────┐
   ↓            ↓            ↓
Threat       MITRE       Explainability
Memory       ATT&CK       / SHAP
   └────────────┼────────────┘
                ↓
        ┌───────────────┐
        │ Audit Ledger  │
        └───────┬───────┘
                ↓
        ┌───────────────┐
        │ SOC Dashboard │
        └───────────────┘
```

---

## 🧪 Development Roadmap

### Current / Prototype

- [x] ML-based network attack detection
- [x] Network-state representation
- [x] Temporal world-model architecture
- [x] Forward simulation / rollout
- [x] Threat memory
- [x] MITRE ATT&CK integration
- [x] Explainability layer
- [x] Security-event auditing
- [x] Streamlit SOC dashboard
- [x] Evidence and evaluation dashboard

### Next

- [ ] Large-scale timestamped network telemetry
- [ ] Stronger chronological forecasting validation
- [ ] Expanded PCAP/live-flow evaluation
- [ ] Analyst-verified adaptive learning
- [ ] Shadow-model evaluation and gated model promotion
- [ ] Richer ATT&CK technique evidence
- [ ] Production-grade distributed audit deployment
- [ ] Continuous monitoring and deployment automation

---

## 🔬 Research Direction

OracleShield is based around a simple research direction:

> **Network security should move from detecting isolated events toward modelling how network behaviour evolves over time.**

The project therefore combines four complementary ideas:

**Detection**
→ What is happening?

**Memory**
→ Have we seen similar behaviour?

**Forecasting**
→ How could the current state evolve?

**Audit**
→ Can the security decision and evidence be verified later?

---

## 🏆 SIH 2026

**Problem Statement:** `SIH26153`

**Title:**  
**AI based Network Attack Forecasting from Network Traffic Data**

**Team:** CyberOracle

**Project:** OracleShield

OracleShield was developed as a Smart India Hackathon 2026 solution focused on proactive network defence through AI-based attack forecasting.

---

## 📚 References

The project research and presentation reference work around:

- Network attack prediction and stream analytics
- Cyberattack development forecasting using Markov models
- Network intrusion detection architectures
- MITRE Enterprise ATT&CK threat modelling
- Kitsune online network intrusion detection
- KDD Cup 99 / NSL-KDD intrusion-detection datasets

Additional research material and project documentation are maintained with the project resources.

---

## ⚖️ Disclaimer

OracleShield is a research/prototype cybersecurity project.

It is **not** a replacement for a production SOC, EDR, SIEM, IDS/IPS, firewall, or incident-response process.

Model outputs are probabilistic and depend on the quality, distribution and temporal characteristics of the input telemetry.

The project should be evaluated and hardened with representative timestamped network data before being used for operational security decisions.

---

## 👥 Team

### CyberOracle

**OracleShield — AI-Based Network Attack Forecasting**

Built for **Smart India Hackathon 2026 · PS 26153**

---

<p align="center">
  <b>Don't just detect the attack.</b><br/>
  <b>Forecast where it goes next. 🛡️</b>
</p>

<p align="center">
  <a href="https://oracleshield.streamlit.app/">Live Demo</a>
  •
  <a href="https://github.com/Shivangdubey049/OracleShield">GitHub</a>
</p>
