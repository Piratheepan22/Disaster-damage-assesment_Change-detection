# AI-Powered Satellite Change Detection 🌍🛰️

Developed as a final-year engineering project, it leverages **Vision Transformers (ViT)** and **Remote Sensing** data to map flood and landslide impacts in Sri Lanka using bi-temporal Sentinel-2 imagery.

---

## 🚀 Project Highlights
* **Hybrid AI Architecture:** Combines a Transformer's global context with a CNN's spatial precision.
* **Custom Dataset:** Curated 400+ bi-temporal satellite scenes across Sri Lanka using Google Earth Engine.
* **Full-Stack Deployment:** A live Web GIS dashboard for real-time inference and damage visualization.
* **Data Engineering:** Custom-built annotation tool to resolve spatial registration and labeling bottlenecks.

---

## 🧠 Methodology & AI Architecture

### 1. Hybrid Vision Transformer (ViT)
The core of the system is a **ViT-Base** backbone pre-trained on the **EuroSAT** dataset. Unlike traditional CNNs that use local sliding windows, the Transformer uses **Self-Attention** to capture global spatial dependencies across the satellite tile.



### 2. 6-Channel Early Fusion
To detect change, the model must "see" the before and after states simultaneously. 
* **Input:** Two RGB images (3 channels each) are concatenated into a single **6-channel tensor**.
* **Benefit:** This allows the model's initial attention layers to learn temporal correlations directly from the raw spectral data.

### 3. CNN Decoder (The "Refiner")
While the ViT is excellent at understanding *what* changed, it processes images in 16x16 pixel "patches." We engineered a custom **CNN Decoder** to upsample these features, recovering sharp boundaries for precise pixel-level flood mapping.

### 4. Transfer Learning Strategy
* **Backbone:** Frozen EuroSAT weights to maintain foundational geospatial knowledge.
* **Fine-tuning:** Unfrozen top layers and decoder to adapt to the specific spectral signatures of Sri Lankan disasters.

---

## 🛠️ Tech Stack
| Component | Technology |
| :--- | :--- |
| **Deep Learning** | PyTorch, `timm` (PyTorch Image Models) |
| **Satellite Data** | Google Earth Engine (GEE) API, Sentinel-2 (MSI) |
| **Backend** | Flask (Python), Gunicorn |
| **Frontend** | Leaflet.js, JavaScript (ES6), HTML5/CSS3 |
| **Deployment** | AWS EC2 / Render |

---

## 📂 Project Structure
```text
DisasterVisionPro/
├── src/                   # AI Core
│   ├── model.py           # Hybrid ViT + CNN Decoder architecture
│   ├── dataset.py         # 6-channel fusion & Data loading logic
│   ├── train.py           # Training pipeline with validation
│   └── evaluate.py        # Metrics: IoU, F1-Score, Confusion Matrix
├── web/                   # Web Application
│   ├── app.py             # Flask API & Model Inference
│   ├── static/            # Map logic (Leaflet.js) & UI Styling
│   └── templates/         # Dashboard (index.html)
├── outputs/               # Research Artifacts
│   ├── reports/           # Loss curves & Confusion matrices
│   └── models/            # .pth Model weights (ignored by git)
└── README.md              # Project Documentation
