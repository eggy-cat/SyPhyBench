# 🎬 PhysStyle-Bench: A Diagnostic Benchmark for Style-Physics Decoupling in Video Generation

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Status: Work in Progress](https://img.shields.io/badge/Status-WIP-orange.svg)]()

> **Is the "Physics Engine" in Video Generation Models entangled with their "Rendering Engine"?** > We introduce **PhysStyle-Bench**, a novel diagnostic benchmark designed to systematically evaluate the causal interaction between visual styles and physical instruction-following in modern Text-to-Video (T2V) models.

---

## 🚀 Visual Teaser
*(⚠️ Placeholder: Add your GIFs here to show the striking contrast!)*

| Prompt: "...stops motionless 20cm above the floor." | `live-action` (Realistic) | `3D cartoon animation` (Stylized) |
| :--- | :---: | :---: |
| **SVD (Base)** | ❌ *Fails: Drops to the ground (Prior Overrides Instruction)* | ✅ *Succeeds: Hovers in the air* |
| **Ours (with Phys-Adapter)** | ✅ *Succeeds: Hovers accurately* | ✅ *Succeeds: Hovers accurately* |

---

## 📖 Introduction

While recent benchmarks evaluate whether video models understand physical laws, **PhysStyle-Bench** asks a deeper question: **Does a model's willingness to execute anti-physical instructions depend heavily on the requested visual style?**

Current models often entangle physical rules (dynamics prior) with visual appearance (rendering prior) within their latent manifold. To diagnose this, we propose a rigorous **2×2 Orthogonal Counterfactual Framework**:
* **Styles**: `live-action` vs. `3D cartoon animation`
* **Physics Constraints**: `real physics` (e.g., falls to the ground) vs. `anti-physics` (e.g., hovers in mid-air)

Using a **Difference-in-Differences (DID)** statistical model, we quantify the true *Style-Physics Entanglement Effect (EE)*, eliminating basic renderability confounders.

## 📊 The 2x2 Causal Diagnostic Framework

Instead of relying solely on LLM-as-a-judge which suffers from hallucination, our **Core Scenes** are evaluated using **deterministic geometric metrics** (e.g., trajectory polarity, bounding box displacement):

1. **Gravity/Contact**: A steel sphere hovering vs. dropping.
2. **Buoyancy**: A helium balloon rising vs. dropping.
3. **Potential Energy**: A glass marble rolling up vs. down a ramp.

## 🏆 Leaderboard (Mini-Pilot)

| Model | Base Renderability (BRS) | Conditional Result Adherence (CRA) | Entanglement Effect (EE) |
| :--- | :---: | :---: | :---: |
| **Stable Video Diffusion (SVD)** | 0.85 | 0.22 | **+0.45** (Highly Coupled) |
| **VideoCrafter2** | 0.82 | 0.30 | **+0.38** (Coupled) |
| **[Your Model/Adapter]** | **0.90** | **0.85** | **+0.05** (Decoupled) |

*(Note: The above scores are illustrative placeholders from pilot testing.)*

## 🛠️ Quick Start & Evaluation Pipeline

### 1. Environment Setup
```bash
git clone [https://github.com/](https://github.com/)[YourName]/PhysStyle-Bench.git
cd PhysStyle-Bench
pip install -r requirements.txt