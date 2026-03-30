<div align="center">

<h1>🤖 Embodied Multimedia</h1>
<h3><em>When Multimedia Meets Embodied Intelligence</em></h3>

<p>
  <a href="https://doi.org/10.1145/nnnnnnn.nnnnnnn">
    <img src="https://img.shields.io/badge/ACM%20CSUR-Submitted-blue?style=flat-square&logo=acm" alt="ACM CSUR"/>
  </a>
  <a href="https://arxiv.org/abs/xxxx.xxxxx">
    <img src="https://img.shields.io/badge/arXiv-Preprint-b31b1b?style=flat-square&logo=arxiv" alt="arXiv"/>
  </a>
  <img src="https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey?style=flat-square" alt="License"/>
  <img src="https://img.shields.io/badge/Status-Active-brightgreen?style=flat-square" alt="Status"/>
  <img src="https://img.shields.io/badge/Year-2026-orange?style=flat-square" alt="Year"/>
</p>

<p>
  <strong>Wei Zuo<sup>*1</sup> · Yang Liu<sup>*2</sup> · Weniang Yang<sup>1</sup> · Feng Wu<sup>1</sup> · Wei Zhou<sup>3</sup> · Jing Liu<sup>†4</sup> · Peng Sun<sup>5</sup> · Jing Cheng<sup>†6</sup> · Dingkang Yang<sup>†1</sup> · Xinhua Zeng<sup>†1</sup></strong>
</p>

<p>
  <sup>1</sup>Fudan University &nbsp;|&nbsp;
  <sup>2</sup>Tongji University &nbsp;|&nbsp;
  <sup>3</sup>Cardiff University &nbsp;|&nbsp;
  <sup>4</sup>University of British Columbia &nbsp;|&nbsp;
  <sup>5</sup>Duke Kunshan University &nbsp;|&nbsp;
  <sup>6</sup>East China Normal University
</p>

<p><sup>*</sup>Equal contribution &nbsp;&nbsp; <sup>†</sup>Corresponding authors</p>

---

<p>
  <a href="#-introduction">Introduction</a> •
  <a href="#-why-embodied-multimedia">Motivation</a> •
  <a href="#-architecture">Architecture</a> •
  <a href="#-key-technologies">Key Technologies</a> •
  <a href="#-evaluation">Evaluation</a> •
  <a href="#-open-challenges">Challenges</a> •
  <a href="#-citation">Citation</a>
</p>

</div>

---

## 📌 Introduction

The explosive rise of **Embodied Intelligence** — AI that perceives, reasons, and acts within the physical world — demands a fundamental rethink of how we create, transmit, and evaluate multimedia data.

Traditional multimedia was built for **human observers**: compressing what the eye cannot see, streaming what the ear can tolerate, and measuring quality by human perceptual standards. But when an **embodied agent** — a robot arm, an autonomous vehicle, a household assistant — relies on that same data to make real-time physical decisions, the entire pipeline breaks down.

> *"Multimedia data is no longer merely content for human consumption; it serves as the essential sensory foundation that bridges an agent's cognition and physical execution."*

This survey formally introduces **Embodied Multimedia**: a unified paradigm that re-engineers the entire multimedia stack — from data acquisition to communication to cognition to evaluation — to serve not human audiences, but **embodied intelligent agents**.

<div align="center">
  <img src="assets/framework.png" alt="Embodied Multimedia Framework Overview" width="85%"/>
  <br/>
  <em>Figure 1: The four-layer Embodied Multimedia architecture and survey organization.</em>
</div>

---

## 🔍 Why Embodied Multimedia?

Modern multimedia systems are fundamentally **misaligned** with the requirements of embodied agents. The mismatch spans every layer of the pipeline:

| Dimension | 🖥️ Traditional Multimedia | 🤖 Embodied Multimedia |
|---|---|---|
| **Target User** | Human observers | Embodied agents & robots |
| **Core Goal** | Optimize perceptual experience | Optimize task execution |
| **Data Acquisition** | Passive, fixed viewpoints | Active, dynamic, semantic-aware |
| **Data Processing** | Discard imperceptible details | Retain task-critical features |
| **Communication** | Bit-level reliable transmission | Task-oriented semantic communication |
| **Retrieval** | Static feature matching | Dynamic agent-based reasoning |
| **Generative Models** | Aesthetically pleasing content | Physically grounded, actionable outputs |
| **Evaluation** | PSNR, SSIM, FID | Task success rate, interaction safety |

### 🚨 The Core Problems

- **Data Acquisition Gap** — Traditional compression standards (JPEG, HEVC) discard high-frequency texture and edge information that human eyes miss but machine vision critically needs. Fixed-viewpoint passive capture cannot resolve occlusions that block scene understanding.

- **Communication Bottleneck** — Shannon-theoretic bit-level transmission paradigms cannot meet millisecond-level spatio-temporal synchronization demands of real-time physical interaction. Centralized cloud processing introduces prohibitive latency.

- **Retrieval Limitation** — Static cross-modal retrieval lacks closed-loop reasoning, making it unable to support the ambiguous, long-horizon, knowledge-intensive tasks embodied agents routinely face.

- **Generative Grounding Failure** — GANs and diffusion models trained on aesthetic objectives lack physical law understanding. Embodied agents need models that generate actionable, physics-consistent outputs.

- **Evaluation Blindspot** — PSNR and SSIM measure pixel fidelity, not task utility. Visually degraded data may still perfectly support a successful robotic operation if semantic features are preserved — traditional metrics miss this entirely.

---

## 🏗️ Architecture

We propose a **unified four-layer Embodied Multimedia architecture** that covers the complete information processing workflow from sensory input to physical action:

```
┌─────────────────────────────────────────────────────────────┐
│                    EMBODIED ENVIRONMENT                     │
│              (Home · Hospital · Road · Factory)             │
└──────────────────────────┬──────────────────────────────────┘
                           │ Physical Interaction
        ┌──────────────────▼──────────────────┐
        │          EVALUATION LAYER           │  ← §7
        │  Perception · Cognition · Action    │
        └──────────────────┬──────────────────┘
                           │ Feedback
        ┌──────────────────▼──────────────────┐
        │          COGNITIVE LAYER            │  ← §6
        │  Retrieval · World Model · VLN · VLA│
        └──────────────────┬──────────────────┘
                           │ Semantic Features
        ┌──────────────────▼──────────────────┐
        │        COMMUNICATION LAYER          │  ← §5
        │   Semantic Comm. · Edge-Cloud ECC   │
        └──────────────────┬──────────────────┘
                           │ Raw/Compressed Data
        ┌──────────────────▼──────────────────┐
        │            DATA LAYER               │  ← §4
        │  Acquisition · Enhancement · Codec  │
        └─────────────────────────────────────┘
                           ▲
                    Multimodal Sensors
               (Camera · LiDAR · Touch · IMU)
```

### 📊 Layer-by-Layer Summary

#### 🗃️ Data Layer
The perceptual foundation of the entire system. Covers:
- **Adaptive Acquisition** — Active perception theory; event cameras; semantic curiosity-driven exploration
- **Tactile Sensing** — Piezoresistive, capacitive, and vision-based tactile sensors for cross-modal fusion
- **Digital Human Motion Generation** — MDM, ReMoDiffuse, InterGen, T2M-GPT, MotionGPT, MoMask
- **Semantic-Guided Enhancement** — SAM-/CLIP-/Diffusion-prior guided restoration (DA-CLIP, CoSeR, SeeSR)
- **End-to-End Compression** — VAE-based image codecs, DVC, DCVC, MobileNVC for on-device deployment

#### 📡 Communication Layer
The neural pathway connecting edge perception to cloud cognition. Covers:
- **Semantic Communication** — DeepSC (text), DeepSC-S (audio), GAN/NTSCC (image), MU-DeepSC (multimodal)
- **Goal-Oriented Communication** — GO-COM / GOS-VAE for task-driven transmission
- **Edge-Cloud Computing** — EECC architecture; "Big Cloud + Small Edge" synergy; federated foundation models

#### 🧠 Cognitive Layer
The decision-making core. Covers:
- **Agent-based Retrieval** — Four-phase closed loop: Task Analysis → Retrieval Execution → Result Optimization → Strategy Iteration
- **World Models** — Generative (Genie, WorldDreamer, Drive-WM, Navigation World Models) and Representation-Predictive (V-JEPA 2, DreamerV3, OccWorld)
- **Vision-Language-Navigation (VLN)** — Environment model-based (DUET, MapGPT, VER, NavMorph) and reasoning-based (NavGPT, NaVid, NaviLLM)
- **Vision-Language-Action (VLA)** — Action token (RT-1, RT-2, π₀, FAST, OpenVLA); Affordance/trajectory (SayCan, VoxPoser); Code/reasoning (Code as Policies, Inner Monologue)

#### 📏 Evaluation Layer
A multi-dimensional assessment framework. Covers:
- **Perception Evaluation** — Machine Preference Database (2.25M samples); RA-MIQA for region-aware quality
- **Cognitive Evaluation** — EQA, ScanQA, SQA3D, PhysBench, EmbodiedEval, IS-Bench, AGENTSAFE
- **Action Evaluation** — R2R, ALFRED, BEHAVIOR, OVMM, RLBench, ManiSkill, CALVIN, Open X-Embodiment

---

## 🔬 Key Technologies

### Agent-based Retrieval
Moving beyond static cross-modal embedding matching (CCA, VSE, CLIP) toward **dynamic retrieval agents** with four key phases:

1. 🧩 **Task Analysis** — query decomposition, sub-query routing, multimodal alignment
2. 🔍 **Retrieval Execution** — sparse (BM25) + dense (DPR) hybrid; multi-granularity tree retrieval (RAPTOR); ReACT/CoT dynamic triggering
3. ✅ **Result Optimization** — reranking, FILCO/FiD-Light context filtering, feedback-driven adaptation
4. 🔄 **Strategy Iteration** — CRAG dynamic switching; continuous alignment between retrieval and generation

### World Models
Two major paradigms for equipping agents with the ability to *imagine* the future:

| Paradigm | Representative Works | Key Strength |
|---|---|---|
| Generative | Genie, WorldDreamer, Drive-WM, DriveDreamer2, Navigation World Models | High-fidelity video generation, physical law internalization |
| Representation-Predictive | V-JEPA 2, TD-MPC2, DreamerV3, DayDreamer, OccWorld | Computational efficiency, noise robustness, latent planning |

### Vision-Language-Action (VLA)
End-to-end mapping from multimodal perception to physical control:

- **Action Tokenization** — RT-1 → RT-2 → π₀ (Flow Matching) → FAST (DCT tokenization) → OpenVLA-OFT
- **Affordance & Trajectory** — SayCan, CLIPort, VoxPoser, RT-Trajectory, DriveVLM
- **Code & Reasoning** — Code as Policies, ProgPrompt, Inner Monologue

---

## 📐 Evaluation

### A New Paradigm: Machine Preference

Traditional metrics (PSNR, SSIM, FID) measure how good data *looks* to humans. We review a new paradigm measuring how well data *serves machines*:

- **Machine Preference Database (MPD)** — 2.25M annotated samples showing the divergence between human and machine quality preferences
- **RA-MIQA** — Region-Aware Machine Image Quality Assessment; identifies machine sensitivity to specific degraded regions (e.g., background blur)

### Action Benchmarks at a Glance

| Benchmark | Year | Environment | Task Type |
|---|---|---|---|
| R2R | 2018 | Matterport3D | Navigation |
| ALFRED | 2020 | AI2-THOR | Navigation + Manipulation |
| RLBench | 2020 | CoppeliaSim | Manipulation |
| BEHAVIOR | 2022 | iGibson | Navigation + Manipulation |
| CALVIN | 2022 | PyBullet | Long-horizon Manipulation |
| OVMM | 2023 | Habitat | Open-vocab Manipulation |
| Open X-Embodiment | 2024 | — | Cross-platform Manipulation |

---

## 🚧 Open Challenges

### Research Challenges

| Challenge | Description |
|---|---|
| 🎯 **Multimodal Spatiotemporal Alignment** | Millisecond-level alignment across RGB, LiDAR, tactile, IMU with vastly different sampling rates |
| 🔩 **Physical Semantic Gaps** | Most datasets lack task-relevant physical attributes: friction, mass, material compliance |
| 📦 **Data Scarcity** | Interaction-rich datasets with causal signals and long-tail scenarios are prohibitively costly |
| ⚡ **On-Device Inference** | VLA and world models demand compute that conflicts with robot power/latency budgets |
| 📶 **Network Unreliability** | Edge-cloud offloading is fragile under bandwidth fluctuations and packet loss |
| 🌉 **Sim-to-Real Transfer** | Physics simulation fidelity gaps severely constrain physical generalization |

### Future Directions

- 🔭 **Multimodal Active Sensing & Generation** — Physics-informed synthetic data with tactile and dynamic properties
- 🪶 **Lightweight Embodied Foundation Models** — Model compression, parameter-efficient fine-tuning for on-device deployment
- 🔀 **Adaptive Edge-Cloud Collaboration** — Context-aware routing between lightweight on-device inference and large cloud models
- ⚙️ **Physics-Aware World Models** — Latent representations capturing geometry, material, and temporal dynamics
- 🧩 **Causal Reasoning in VLA** — Distinguishing correlation from physical causation for sim-to-real generalization
- 📊 **Task- and Safety-Centric Evaluation** — Standardized benchmarks explicitly covering interaction safety and hardware transferability

---

## 📚 Survey Coverage

<div align="center">

| Domain | Scope | Multimodal Perception | Communication | Cognition & Learning | Physical Action | Unified Architecture |
|---|---|:---:|:---:|:---:|:---:|:---:|
| Embodied AI | PCB + LLMs | ✅ | — | ✅ | — | — |
| Embodied AI | Morphology + Action | ✅ | — | ✅ | ✅ | — |
| Multimedia | CBIR, generative, video | ✅ | ✅ | ✅ | — | — |
| **Ours (Cross-domain)** | **Full 4-layer pipeline** | **✅** | **✅** | **✅** | **✅** | **✅** |

</div>

---

## 🗂️ Repository Structure

```
embodied-multimedia/
├── README.md
├── assets/
│   ├── framework.png          # Four-layer architecture figure
│   ├── comparison_table.png   # Traditional vs. Embodied Multimedia
│   └── publication_trend.png  # Research landscape 2015–2025
├── paper/
│   └── embodied_multimedia.pdf
└── resources/
    ├── datasets.md            # Curated dataset list
    ├── benchmarks.md          # Benchmark summary
    └── awesome_papers.md      # Paper collection by topic
```

---

## 📖 Citation

If you find this survey useful for your research, please consider citing:

```bibtex
@article{zuo2026embodied,
  title        = {Embodied Multimedia: When Multimedia Meets Embodied Intelligence},
  author       = {Zuo, Wei and Liu, Yang and Yang, Weniang and Wu, Feng and
                  Zhou, Wei and Liu, Jing and Sun, Peng and Cheng, Jing and
                  Yang, Dingkang and Zeng, Xinhua},
  journal      = {ACM Computing Surveys},
  volume       = {1},
  number       = {1},
  pages        = {1--35},
  year         = {2026},
  month        = {March},
  publisher    = {Association for Computing Machinery},
  address      = {New York, NY, USA},
  doi          = {10.1145/nnnnnnn.nnnnnnn},
  url          = {https://doi.org/10.1145/nnnnnnn.nnnnnnn},
  note         = {Manuscript submitted to ACM}
}
```

---

## 📬 Contact

For questions, discussions, or collaboration inquiries, please reach out to the corresponding authors:

- **Jing Liu** — [jing.liu@ieee.org](mailto:jing.liu@ieee.org) — University of British Columbia
- **Jing Cheng** — [jcheng@phy.ecnu.edu.cn](mailto:jcheng@phy.ecnu.edu.cn) — East China Normal University
- **Dingkang Yang** — [dkyang20@fudan.edu.cn](mailto:dkyang20@fudan.edu.cn) — Fudan University
- **Xinhua Zeng** — [xhzeng@fudan.edu.cn](mailto:xhzeng@fudan.edu.cn) — Fudan University

Or open a GitHub [Issue](../../issues) for technical discussions and suggestions.

---

<div align="center">

⭐ **Star this repo** if you find it helpful — it helps us reach more researchers in the community!

<br/>

<img src="https://img.shields.io/github/stars/yourorg/embodied-multimedia?style=social" alt="Stars"/>
&nbsp;
<img src="https://img.shields.io/github/forks/yourorg/embodied-multimedia?style=social" alt="Forks"/>

</div>
