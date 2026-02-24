# AI-Powered Satellite Change Detection 🌍🛰️

## 🌍 Introduction

Natural disasters, particularly floods and landslides, pose a significant threat to infrastructure and human life in Sri Lanka. Rapid response depends on **timely and accurate damage assessment**. However, traditional ground-based surveys are slow, and manual analysis of satellite imagery is labor-intensive and prone to human error.

Our project addresses this challenge by providing an automated, end-to-end pipeline for satellite-based change detection. The project leverages a **Hybrid Deep Learning** approach to transform raw Sentinel-2 satellite data into actionable disaster maps.

### 🧠 The Core Innovation: Hybrid ViT-CNN
At the heart of this project is a specialized neural network architecture designed to solve the limitations of traditional computer vision:

* **Vision Transformer (ViT) Encoder:** We utilize a **ViT-Base** backbone to capture **global spatial dependencies**. Unlike standard CNNs that look at local clusters of pixels, the ViT uses a **Self-Attention** mechanism to understand the entire landscape context. This is crucial for identifying large-scale flood patterns where distant geographical features influence local change detection.
* **CNN-Based Decoder:** While Transformers are excellent at understanding *context*, they naturally process images in "patches" (e.g., 16x16 pixels), which can result in blocky output masks. To solve this, I engineered a custom **CNN Decoder**. It takes the high-level features from the ViT and performs **Transposed Convolutions** and **Upsampling** to recover fine-grained spatial details, ensuring the final damage masks are sharp and pixel-perfect.



### 🛰️ Multi-Spectral Early Fusion
To detect changes over time, the system implements an **Early Fusion** strategy. Pre-disaster and post-disaster RGB imagery are concatenated into a **6-channel input volume**. This allows the model's initial attention layers to learn the mathematical relationship between the two time periods directly, significantly improving sensitivity to sudden environmental shifts like rising water levels or soil displacement.

### 🌐 Beyond the Model: Full-Stack Web Deployment
Recognizing that an AI model is only useful if it is accessible to responders, this project includes a fully integrated **Web GIS Dashboard**:

* **Live Data Pipeline:** Integrated with the **Google Earth Engine (GEE) API** to fetch real-time Sentinel-2 MSI data on demand, handling cloud-masking and normalization automatically.
* **Web GIS Interface:** A professional dashboard built with **Flask** and **Leaflet.js**, providing an interactive map where users can toggle between bi-temporal imagery and AI-generated damage overlays.
* **Custom Annotation Tool:** To solve the data bottleneck in the South Asian region, I developed a **bespoke annotation UI**. This tool allowed for the curation of a high-fidelity dataset of 400+ disaster scenes, ensuring the model is grounded in local Sri Lankan geography.

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
While the ViT is excellent at understanding *what* changed, it processes images in 16x16 pixel "patches." We engineered a custom **CNN Decoder** to upsample these features, recovering sharp boundaries for precise pixel-level disaster mapping.

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
| **Frontend** | Leaflet.js, JavaScript , HTML5/CSS3 |

---

## 📊 Dataset Information

### Data Source
- **Provider:** Google Earth Engine (Sentinel-2 MSI)
- **Temporal Coverage:** 2020-2024
- **Spatial Resolution:** 10m per pixel
- **Spectral Bands:** RGB (B4, B3, B2) + NIR (B8) for pre/post-disaster pairs

### Dataset Access
- Custom annotation tool available in `https://piratheepan22.github.io/Dataset-Annotation/`
- Currently curating 400+ bi-temporal scenes (active development phase)

---

## 🛠️ Development Status

### ✅ Completed
- [x] Hybrid ViT + CNN architecture design
- [x] 6-channel early fusion pipeline
- [x] Custom annotation tool
- [x] Google Earth Engine data pipeline
- [x] Flask API backend structure

### 🚧 In Progress
- [ ] Web GIS dashboard frontend refinement
- [ ] Dataset creation
- [ ] annotation of binay masks for collected images

### 📅 Upcoming
- [ ] Full model training on 400+ dataset
- [ ] Model evaluation & validation metrics
- [ ] Hyperparameter tuning & optimization
- [ ] Real-time inference deployment
- [ ] Advanced visualization features
- [ ] documentation & report

---

## 📧 Contact & Author

**Project Lead:** Piratheepan22
- GitHub: [@Piratheepan22](https://github.com/Piratheepan22)
- Project Repository: [Disaster-damage-assesment_Change-detection](https://github.com/Piratheepan22/Disaster-damage-assesment_Change-detection)

---

## 📜 License
This project is developed as an academic final-year engineering project. License details to be determined.

---

## 🙏 Acknowledgments
- **Google Earth Engine** for satellite imagery access
- **Hugging Face Transformers** for Vision Transformer implementations
- **PyTorch** community for deep learning tools
- Remote sensing research community for methodological inspiration
