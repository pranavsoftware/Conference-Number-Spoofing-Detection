<div align="center">

<!-- Hero Banner -->
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 900 180" width="900" height="180">
  <defs>
    <linearGradient id="bg" x1="0%" y1="0%" x2="100%" y2="100%">
      <stop offset="0%" style="stop-color:#0f0c29"/>
      <stop offset="50%" style="stop-color:#302b63"/>
      <stop offset="100%" style="stop-color:#24243e"/>
    </linearGradient>
    <linearGradient id="accent" x1="0%" y1="0%" x2="100%" y2="0%">
      <stop offset="0%" style="stop-color:#f953c6"/>
      <stop offset="100%" style="stop-color:#b91d73"/>
    </linearGradient>
    <filter id="glow">
      <feGaussianBlur stdDeviation="3" result="coloredBlur"/>
      <feMerge><feMergeNode in="coloredBlur"/><feMergeNode in="SourceGraphic"/></feMerge>
    </filter>
  </defs>
  <rect width="900" height="180" fill="url(#bg)" rx="12"/>
  <!-- Decorative circles -->
  <circle cx="820" cy="30" r="60" fill="#f953c6" opacity="0.08"/>
  <circle cx="80" cy="150" r="80" fill="#302b63" opacity="0.5"/>
  <circle cx="450" cy="10" r="40" fill="#b91d73" opacity="0.07"/>
  <!-- Accent line -->
  <rect x="40" y="130" width="180" height="3" fill="url(#accent)" rx="2"/>
  <!-- Icon: shield with signal -->
  <g transform="translate(42, 28)" filter="url(#glow)">
    <path d="M30 0 L60 12 L60 36 C60 52 46 64 30 68 C14 64 0 52 0 36 L0 12 Z" fill="none" stroke="#f953c6" stroke-width="2.5" opacity="0.9"/>
    <circle cx="30" cy="34" r="5" fill="#f953c6"/>
    <path d="M18 24 Q30 14 42 24" fill="none" stroke="#f953c6" stroke-width="2" opacity="0.7"/>
    <path d="M12 18 Q30 4 48 18" fill="none" stroke="#f953c6" stroke-width="2" opacity="0.4"/>
  </g>
  <!-- Title -->
  <text x="120" y="56" font-family="'Segoe UI', Arial, sans-serif" font-size="26" font-weight="700" fill="#ffffff" letter-spacing="0.5">Conference Number Spoofing Detection</text>
  <text x="121" y="88" font-family="'Segoe UI', Arial, sans-serif" font-size="14" fill="#c9b8f0" letter-spacing="0.3">Zero-Trust · Multimodal AI · Real-Time Telecom Fraud Intelligence Pipeline</text>
  <!-- Stats pills -->
  <rect x="120" y="106" width="95" height="22" fill="#f953c6" opacity="0.18" rx="11"/>
  <text x="167" y="121" font-family="Arial" font-size="11" fill="#f9a8d4" text-anchor="middle">90.05% Accuracy</text>
  <rect x="224" y="106" width="85" height="22" fill="#7c3aed" opacity="0.22" rx="11"/>
  <text x="266" y="121" font-family="Arial" font-size="11" fill="#c4b5fd" text-anchor="middle">0.7243 ROC-AUC</text>
  <rect x="318" y="106" width="75" height="22" fill="#0891b2" opacity="0.22" rx="11"/>
  <text x="355" y="121" font-family="Arial" font-size="11" fill="#7dd3fc" text-anchor="middle">49,999 CDRs</text>
  <rect x="402" y="106" width="70" height="22" fill="#059669" opacity="0.22" rx="11"/>
  <text x="437" y="121" font-family="Arial" font-size="11" fill="#6ee7b7" text-anchor="middle">5-Layer AI</text>
</svg>

<br/>

<!-- Badges -->
![Python](https://img.shields.io/badge/Python-3.9%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![Scikit-Learn](https://img.shields.io/badge/scikit--learn-1.3-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)
![SHAP](https://img.shields.io/badge/SHAP-Explainability-ff6b6b?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-22c55e?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Research%20Prototype-a855f7?style=for-the-badge)

</div>

---

## 🧭 Overview

Conference bridge numbers are quietly becoming one of the most exploited surfaces in telecom fraud. An attacker who spoofs a well-known enterprise dial-in number can inject fraudulent audio, harvest participant credentials, or silently record sessions — all while appearing to come from a legitimate source.

Existing caller-authentication standards like **STIR/SHAKEN** handle general caller-ID spoofing but leave a blind spot when the abused number belongs to a real conferencing service. This project fills that gap.

**Conference Number Spoofing Detection** is a research-grade, notebook-first pipeline that combines five independent detection layers — zero-trust authentication, voice analytics, network routing forensics, NLP transcript analysis, and caller reputation — into a single fused risk score that drives real-time response decisions.

> 📄 A 6-page IEEE conference paper based on this work is available in [`conference_paper/`](./conference_paper/spoofing_detection_paper.pdf).

---

## ✨ What Makes This Different

| Aspect | This Project |
|--------|-------------|
| 🔍 **Detection approach** | Multimodal fusion — no single signal, five independent layers |
| 🔒 **Trust model** | Zero-trust by default; every call is scored, not just flagged ones |
| 🤖 **Explainability** | Per-call SHAP explanations with ranked risk drivers |
| ⚡ **Response** | Four-tier automated action (ALLOW → WARN → QUARANTINE → BLOCK) |
| 📋 **Auditability** | SHA-256 fingerprinted audit log; NIST SP 800-92 aligned |
| 📊 **Honest evaluation** | Data leakage-free features; realistic 90.05% accuracy, not inflated 100% |

---

## 📐 System Architecture

```
┌──────────────────────────────────────────────────────────────────┐
│                   INCOMING CALL / CDR EVENT                       │
└─────────────────────────────┬────────────────────────────────────┘
                              │
            ┌─────────────────▼─────────────────┐
            │  LAYER 1 · Event Ingestion         │
            │  CDR normalization · timestamps    │
            │  session IDs · gateway fields      │
            └─────────────────┬─────────────────┘
                              │
            ┌─────────────────▼─────────────────┐
            │  LAYER 2 · Zero-Trust Verification │
            │  STIR/SHAKEN · TLS · device attest │
            │  caller-ID match · geo mismatch    │
            │  ──────────────────────────────    │
            │  session_trust_score  ∈ [0,1]      │
            └─────────────────┬─────────────────┘
                              │
  ┌───────────────────────────▼───────────────────────────────┐
  │               LAYER 3 · AI Intelligence Engine            │
  │                                                           │
  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐      │
  │  │  Behavior   │  │    Voice    │  │   Network   │      │
  │  │  Anomaly    │  │  Deepfake   │  │   Pattern   │      │
  │  │ (IsoForest) │  │ (Rand.Forest│  │ (Rand.Forest│      │
  │  └──────┬──────┘  └──────┬──────┘  └──────┬──────┘      │
  │         │                │                │               │
  │  ┌──────▼──────┐  ┌──────▼──────┐         │               │
  │  │  NLP / Text │  │  Reputation │         │               │
  │  │  TF-IDF+LR  │  │  Blacklist  │◄────────┘               │
  │  └──────┬──────┘  └──────┬──────┘                        │
  │         └────────┬────────┘                               │
  │              ┌───▼──────────────────┐                     │
  │              │  RISK FUSION ENGINE  │                     │
  │              │  GradientBoosting    │                     │
  │              │  + SHAP Explainer    │                     │
  │              └───┬──────────────────┘                     │
  └──────────────────┼────────────────────────────────────────┘
                     │
            ┌────────▼────────────────────┐
            │  LAYER 4 · Response Actions  │
            │  ALLOW · WARN · QUARANTINE  │
            │  BLOCK · Incident Tickets   │
            │  Dynamic Blacklist Updates  │
            └────────┬────────────────────┘
                     │
            ┌────────▼────────────────────┐
            │  LAYER 5 · Governance       │
            │  Immutable Audit Log (SHA)  │
            │  Model Metadata · Drift     │
            │  SHAP Reports · Compliance  │
            └─────────────────────────────┘
```

---

## 📊 Key Results

<div align="center">

| Metric | Value |
|--------|-------|
| 📦 **Dataset size** | 49,999 CDR records |
| 🎯 **Fraud prevalence** | 10.41% (5,204 fraud events) |
| ✅ **Overall accuracy** | **90.05%** |
| 🎯 **Fraud precision** | **72.08%** |
| 📈 **ROC-AUC** | **0.7243** |
| 🛡️ **BLOCK actions** | 5,754 calls (11.5%) |
| ⚠️ **QUARANTINE actions** | 5,997 calls (12.0%) |
| 🔔 **WARN actions** | 8,893 calls (17.8%) |
| ✔️ **ALLOW actions** | 29,355 calls (58.7%) |
| 📋 **Incident tickets** | 300 auto-generated |
| 🚫 **Blacklist candidates** | 2,500 numbers |

</div>

### Fusion Formula

The fused risk score combines all six signal streams:

```
R = 0.15 × trust_risk
  + 0.20 × behavior_risk
  + 0.20 × voice_risk
  + 0.15 × network_risk
  + 0.15 × reputation_risk
  + 0.15 × transcript_risk
```

Risk tiers are set dynamically using **percentile-based thresholds** (p60 / p80 / p95) computed from the actual score distribution — so the system self-calibrates and always produces meaningful tier splits regardless of score drift.

---

## 🗂️ Project Structure

```
conference no. spoofing/
│
├── 📓 notebooks/
│   └── telecom_spoofing_detection.ipynb   ← Main pipeline (47 cells, runs end-to-end)
│
├── 📊 results/
│   ├── png/                               ← All charts and visualisations
│   │   ├── confusion_matrix.png
│   │   ├── roc_curve.png
│   │   ├── shap_summary.png
│   │   ├── feature_importance.png
│   │   ├── layer3_model_scores.png
│   │   ├── layer4_response_actions.png
│   │   ├── alert_volume_dashboard.png
│   │   └── risk_distribution.png
│   ├── json/                              ← Structured decision artifacts
│   │   ├── model_metadata.json
│   │   ├── scored_calls.json
│   │   ├── explanations.json
│   │   ├── incidents.json
│   │   ├── blacklist_updates.json
│   │   └── trust_summary.json
│   ├── csv/                               ← Tabular outputs for analysis
│   │   ├── scored_calls.csv
│   │   ├── audit_log.csv
│   │   ├── action_summary.csv
│   │   ├── feature_table.csv
│   │   ├── trust_features.csv
│   │   └── drift_summary.csv
│   └── reports/
│       └── executive_summary.md
│
├── 🤖 model/
│   ├── artifacts/
│   │   ├── behavior_anomaly_model.pkl     ← Isolation Forest (200 estimators)
│   │   ├── voice_risk_model.pkl           ← Random Forest (150 estimators)
│   │   ├── network_pattern_model.pkl      ← Random Forest (150 estimators)
│   │   ├── nlp_risk_model.pkl             ← TF-IDF + Logistic Regression
│   │   └── risk_fusion_model.pkl          ← Gradient Boosting meta-classifier
│   ├── explainers/
│   │   └── shap_explainer.pkl
│   └── thresholds/
│       └── thresholds.json
│
├── 📄 conference_paper/
│   ├── spoofing_detection_paper.tex       ← IEEE LaTeX source (6 pages)
│   ├── spoofing_detection_paper.pdf       ← Compiled paper
│   └── IEEEtran.cls
│
├── 📝 project.md                          ← Full system design specification
└── 📖 README.md                           ← You are here
```

---

## 🚀 Getting Started

### Prerequisites

```bash
pip install pandas numpy scikit-learn matplotlib seaborn shap joblib
```

> **Python 3.9+** is required. All dependencies are available on PyPI.

### Run the Notebook

```bash
# Clone or download the project folder, then:
cd "conference no. spoofing"

# Open in Jupyter
jupyter notebook notebooks/telecom_spoofing_detection.ipynb

# Or run headlessly
python -m nbconvert --to notebook --execute \
  --ExecutePreprocessor.timeout=600 \
  --output-dir notebooks \
  notebooks/telecom_spoofing_detection.ipynb
```

The notebook runs **end-to-end** in a single pass. All 47 code cells execute without errors. Outputs are saved automatically under `results/` and `model/`.

### Data

The pipeline loads from the **Kaggle CDR Fraud Detection dataset** ([jakefurgoson/fraud-detection-using-call-detail-records](https://www.kaggle.com/datasets/jakefurgoson/fraud-detection-using-call-detail-records)). Place `CDR-Call-Details.csv` in the `dataset/` folder before running. If the file is absent, the notebook gracefully generates a synthetic dataset.

---

## 🧠 Detection Modules

### 🏃 Layer 1 — Event Ingestion
Raw CDR fields are parsed, normalized, and enriched with temporal features (hour of day, night-call flag) and session-level velocity aggregates.

### 🔐 Layer 2 — Zero-Trust Verification
Every call receives a **Session Trust Score** derived from eight signals: STIR/SHAKEN attestation level, TLS validity, device attestation, caller-ID match, carrier verification, geographic origin mismatch, number reuse frequency. The trust risk `(1 - trust_score)` feeds directly into the fusion engine.

### 🤖 Layer 3 — AI Intelligence (5 sub-models)

| Sub-model | Algorithm | Input features |
|-----------|-----------|----------------|
| 🔊 Voice Deepfake | Random Forest (150 est.) | voice embedding shift, pitch variance, spectral flatness, synthetic voice prob |
| 🌐 Network Pattern | Random Forest (150 est.) | gateway hops, route entropy, carrier switches, fan-out ratio, bridge reuse |
| 🧠 Behavior Anomaly | Isolation Forest (200 est.) | calls/hour, unique callees/24h, avg duration, night ratio, burstiness index |
| 📝 NLP / Transcript | TF-IDF + Logistic Regression | urgency keywords, payment requests, credential solicitation flags |
| ⭐ Caller Reputation | Rule-based composite | blacklist hit, complaint count, reputation score, carrier risk band |

### ⚡ Layer 4 — Response Orchestration
A **Gradient Boosting meta-classifier** (150 est., depth 4, lr 0.08) fuses all six risk components plus auxiliary signals (blacklist flag, attestation level, geo mismatch, call velocity) to produce a final fraud probability. Calls are routed to one of four tiers based on dynamic percentile thresholds.

### 📋 Layer 5 — Governance & Audit
- **Immutable audit log** with SHA-256 fingerprints on every decision
- **SHAP explainability** — top-3 risk drivers surfaced per flagged call
- **Data drift monitoring** across 7 feature streams (zero drift detected)
- **Incident auto-ticketing** for BLOCK/QUARANTINE events

---

## 🔬 Explainability Sample

Every flagged call produces a structured explanation payload:

```json
{
  "call_id": "CALL-253A40FC",
  "fused_risk_score": 0.4058,
  "risk_level": "CRITICAL",
  "top_risk_factors": [
    { "factor": "transcript_risk", "score": 0.5405 },
    { "factor": "network_risk",    "score": 0.5189 },
    { "factor": "reputation_risk", "score": 0.5176 }
  ],
  "trust_failures": [
    "Geographic origin mismatch",
    "Number on blacklist"
  ],
  "transcript_snippet": "This is IRS. You owe back taxes. Pay with gift cards or face arrest.",
  "recommended_action": "AUTO-BLOCK"
}
```

---

## 📌 Design Decisions

### Why percentile-based thresholds?
After removing data leakage, fused risk scores cluster in a realistic `0.25–0.40` range — very different from inflated scores seen when features encode the target label. Hardcoded thresholds (`>= 0.60`) would produce zero flagged calls. Percentile-based thresholds (`p60 / p80 / p95`) self-calibrate to the actual distribution and always produce non-trivial tier assignments.

### Why not 100% accuracy?
An earlier version of the pipeline achieved 100% accuracy — but only because synthetic features (call velocity, transcript content) were generated *conditioned on the fraud label*, which is a textbook data leakage problem. The current pipeline generates all features independently of labels. The resulting 90.05% accuracy and 0.7243 ROC-AUC are **honest** numbers.

### Why Gradient Boosting for fusion?
The meta-classifier needs to handle non-linear interactions between sub-model scores (e.g., high reputation risk combined with low trust is more alarming than either alone). Gradient Boosting captures these interactions naturally and integrates well with SHAP for tree-based explanations.

---

## 📄 Conference Paper

A full IEEE-format 6-page paper based on this pipeline is available in [`conference_paper/`](./conference_paper/).

**Title:** *Zero-Trust Multimodal Detection of Conference Number Spoofing in Telecommunications Networks*

The paper covers the complete five-layer architecture, honest experimental evaluation, comparison against related single-modality approaches, adversarial robustness considerations, and future work directions.

---

## 👩‍💻 Authors

<div align="center">

| | Author | Role |
|---|--------|------|
| 🎓 | **Rayban Pranav** | Lead developer, pipeline architecture, data leakage analysis |
| 🎓 | **Mahesh** | Feature engineering, zero-trust layer design |
| 🎓 | **Karishma Rahaman** | NLP module, transcript risk scoring |
| 🎓 | **Marmik Pradip Kaila** | Network pattern analysis, routing forensics |
| 🎓 | **Ajitesh Sharma** | Response orchestration, governance layer |
| 🏫 | **Dr. Jaishree Jaikrishnan** | Faculty advisor |
| 🏫 | **Dr. Nupur Manasi** | Faculty advisor |

📧 **Contact:** [raybanpranav@gmail.com](mailto:raybanpranav@gmail.com)

</div>

---

## 📜 License

This project is released under the **MIT License**. The dataset is subject to its original Kaggle terms of use.

---

## 🙏 Acknowledgments

- The open-source community behind the [Kaggle CDR Fraud Detection dataset](https://www.kaggle.com/datasets/jakefurgoson/fraud-detection-using-call-detail-records) for enabling reproducible telecom research.
- The authors of [SHAP](https://github.com/slundberg/shap) for making model explainability accessible.
- IEEE and the IEEEtran LaTeX class maintainers.

---

<div align="center">

<!-- Footer SVG -->
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 800 50" width="800" height="50">
  <defs>
    <linearGradient id="fgrad" x1="0%" y1="0%" x2="100%" y2="0%">
      <stop offset="0%" style="stop-color:#f953c6;stop-opacity:0"/>
      <stop offset="50%" style="stop-color:#b91d73;stop-opacity:1"/>
      <stop offset="100%" style="stop-color:#f953c6;stop-opacity:0"/>
    </linearGradient>
  </defs>
  <rect y="22" width="800" height="1" fill="url(#fgrad)"/>
  <text x="400" y="42" font-family="'Segoe UI', Arial, sans-serif" font-size="11" fill="#9ca3af" text-anchor="middle">
    Built with ❤️ for telecom security research · 2026
  </text>
</svg>

</div>
