# VISUALine

VISUALine is a modular AI framework for automated video enhancement and visual editing. It combines multiple state-of-the-art computer vision models into flexible, node-based pipelines for tasks such as background blur, privacy redaction, smart reframing, slow motion generation, super-resolution, and old video restoration.

Designed for consumer GPUs, VISUALine features efficient model caching, mixed-precision inference, and a lightweight execution engine to deliver high-quality results with optimized memory usage.

**Keywords:** Computer Vision, Video Processing, Local AI, Modular Pipelines, Video Enhancement, Prompt-Based Editing, Super Resolution

---

# Workflows

## Cinematic Prompt Blur (Fast)

Fast subject-aware background blur using open-vocabulary object detection.

**Pipeline**

```text
PromptBoxDetectionNode
        ↓
SoftBoxMaskNode
        ↓
BokehBlurNode
```

---

## Cinematic Prompt Blur (HQ SAM2)

High-quality background blur using prompt detection and SAM2 video tracking for more accurate masks.

**Pipeline**

```text
PromptBoxDetectionNode
        ↓
SAM2TrackingNode
        ↓
BokehBlurNode
```

---

## Privacy Redaction

Detects sensitive regions such as people or faces and applies a redaction effect.

**Pipeline**

```text
PromptBoxDetectionNode
        ↓
BoxRedactionNode
```

---

## Old Video Enhancement (Fast)

Lightweight enhancement with denoising, sharpening, contrast correction, saturation adjustment, and gamma correction.

**Pipeline**

```text
VideoEnhanceNode
```

---

## Old Video Enhancement (SPAN x4)

Advanced restoration using AI super-resolution.

**Pipeline**

```text
VideoEnhanceNode
        ↓
SPANNode
        ↓
VideoEnhanceNode
```

---

## Smart Vertical Reframe

Automatically crops and tracks a prompted subject for vertical video formats.

**Pipeline**

```text
PromptBoxDetectionNode
        ↓
SmartReframeNode
```

---

## Slow Motion (RIFE x2)

Generates smooth slow-motion videos using AI frame interpolation.

**Pipeline**

```text
RIFENode
```

---

# Installation

## Clone the repository

```bash
git clone https://github.com/<username>/VISUALine.git
cd VISUALine
```

## Create a virtual environment

```bash
python -m venv .venv
```

### Windows

```bash
.venv\Scripts\activate
```

### Linux / macOS

```bash
source .venv/bin/activate
```

## Install dependencies

```bash
pip install -r requirements.txt
```

## Download model weights

Download the required pretrained weights and place them inside the `weights/` directory.

| Model         | Purpose                         | Link     |
| ------------- | ------------------------------- | -------- |
| GroundingDINO | Prompt-based detection          | Add link |
| SAM2          | Video segmentation and tracking | Add link |
| RIFE          | Frame interpolation             | Add link |
| SPAN x4       | Super resolution                | Add link |

## Automatic weight download

The required models can also be downloaded automatically using the provided scripts.

```bash
python scripts/download_weights.py
```

Or download individual models:

```bash
python scripts/download_groundingdino.py
python scripts/download_sam2.py
python scripts/download_rife.py
python scripts/download_span.py
```

---

# Quick Start

```bash
python main.py
```

Or launch the GUI:

```bash
python app.py
```

---

# Architecture

VISUALine follows a node-based architecture where each processing stage is encapsulated as a reusable module. Nodes consume and produce tensor-based data, making workflows modular, scalable, and easy to extend.

Features:

* Modular processing pipelines
* GPU acceleration
* Mixed-precision inference
* LRU model caching
* Consumer GPU optimization
* Image and video support
* Programmatic and interactive interfaces
