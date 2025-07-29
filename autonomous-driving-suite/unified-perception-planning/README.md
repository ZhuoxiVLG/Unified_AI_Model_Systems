

# Unified Perception and Planning (UPP)

**UPP** (Unified Perception and Planning) is a learning-based framework designed to address the growing demand for **integrated perception, prediction, and planning** in autonomous driving. As autonomous systems evolve from controlled environments to open, real-world traffic scenarios, the need for a unified, responsive, and robust architecture has become more urgent than ever.

![logo](logo.png)

## 🔍 Background

With the rapid advancement of artificial intelligence and autonomous driving technologies, systems are increasingly required to operate in **dynamic, unstructured environments**. This shift imposes stringent requirements on the **completeness, timeliness, and robustness** of environmental understanding.

However, most existing autonomous driving stacks still follow a **modular architecture**, where feature extraction, perception, prediction, and planning are developed as isolated modules. This modularity leads to several core challenges:

- **Semantic disconnection** between perception and decision-making.
- **Inconsistent objectives** across modules, limiting global optimization.
- **Redundant computation**, increased latency, and error accumulation.
- **Weak system responsiveness** in complex or rapidly changing environments.

## 🎯 Project Goal

**UPP** aims to break down these boundaries by creating a **unified model** that tightly integrates the following four key components:

### 1. Feature Extraction

Lightweight yet expressive encoding of multi-modal sensor inputs, ensuring that extracted features are directly aligned with the needs of downstream perception and decision-making tasks.

### 2. Perception

Joint object detection and scene understanding using a task-driven architecture that supports effective fusion of heterogeneous information, enabling robust environmental modeling in real time.

### 3. Environment Prediction

Incorporation of interaction-aware forecasting, allowing the system to anticipate multi-agent behaviors with high fidelity, especially in dense or ambiguous traffic conditions.

### 4. Decision & Planning

Unified end-to-end learning from perception to trajectory generation. Replaces hand-crafted rules with adaptive policies capable of responding to diverse driving contexts and intentions.
