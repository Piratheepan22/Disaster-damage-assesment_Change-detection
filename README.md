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
├── data/                  # Dataset Directory
│   ├── raw/               # Original Sentinel-2 scenes (GEE exports)
│   ├── processed/         # Preprocessed 6-channel tensors
│   └── annotations/       # Ground truth labels & masks
├── requirements.txt       # Python dependencies
├── .gitignore             # Git ignore file
└── README.md              # Project Documentation
```

---

## 📋 Installation & Setup

### Prerequisites
- Python 3.9+
- CUDA 11.8+ (for GPU acceleration)
- Git

### Step 1: Clone the Repository
```bash
git clone https://github.com/Piratheepan22/Disaster-damage-assesment_Change-detection.git
cd Disaster-damage-assesment_Change-detection
```

### Step 2: Create Virtual Environment
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### Step 3: Install Dependencies
```bash
pip install -r requirements.txt
```

### Step 4: Set Up Google Earth Engine API (Optional for data export)
```bash
earthengine authenticate
```

---

## 🚀 Quick Start

### Training the Model
```bash
python src/train.py --epochs 50 --batch_size 32 --learning_rate 0.001
```

### Running Inference
```bash
python src/evaluate.py --model_path outputs/models/best_model.pth --test_image path/to/image.tif
```

### Starting the Web Dashboard
```bash
python web/app.py
# Access at http://localhost:5000
```

---

## 📊 Dataset Information

### Data Source
- **Provider:** Google Earth Engine (Sentinel-2 MSI)
- **Temporal Coverage:** 2020-2024
- **Spatial Resolution:** 10m per pixel
- **Spectral Bands:** RGB (B4, B3, B2) + NIR (B8) for pre/post-disaster pairs

### Dataset Structure
```
data/
├── raw/
│   ├── pre_disaster/      # Before event satellite images
│   └── post_disaster/     # After event satellite images
├── processed/
│   └── train_val_test/    # 6-channel fused tensors
└── annotations/
    ├── flood_masks/       # Binary flood damage masks
    └── landslide_masks/   # Binary landslide damage masks
```

### Dataset Access
- Custom annotation tool available in `data/annotation_tool/`
- Currently curating 400+ bi-temporal scenes (active development phase)

---

## 📝 Usage Guide

### 1. Data Preparation
```bash
# Place raw GEE exports in data/raw/
# Run preprocessing pipeline
python src/dataset.py --input data/raw/ --output data/processed/
```

### 2. Model Training
Edit `src/train.py` to configure:
- Batch size
- Learning rate
- Number of epochs
- Model checkpoint intervals

### 3. Inference & Visualization
```bash
# Generate change detection map
python src/evaluate.py --model outputs/models/checkpoint.pth --input data/processed/test/
```

---

## 🔬 Model Architecture Details

**Input:** 6-channel tensor (B, 6, H, W)
- Channels 0-2: Pre-disaster RGB
- Channels 3-5: Post-disaster RGB

**Processing Pipeline:**
1. ViT-Base patch embedding (16×16 patches)
2. Transformer encoder with self-attention
3. CNN decoder for upsampling
4. Binary segmentation head (changed/unchanged)

**Output:** Change detection map (B, 1, H, W)

---

## 🛠️ Development Status

### ✅ Completed
- [x] Hybrid ViT + CNN architecture design
- [x] 6-channel early fusion pipeline
- [x] Custom annotation tool
- [x] Google Earth Engine data pipeline
- [x] Flask API backend structure

### 🚧 In Progress
- [ ] Full model training on 400+ dataset
- [ ] Hyperparameter tuning & optimization
- [ ] Web GIS dashboard frontend refinement
- [ ] Model evaluation & validation metrics
- [ ] Performance benchmarking

### 📅 Upcoming
- [ ] Real-time inference deployment
- [ ] Advanced visualization features
- [ ] API documentation & tutorials
- [ ] Docker containerization
- [ ] Model versioning & experiment tracking

---

## 📧 Contact & Author

**Project Lead:** Piratheepan22
- GitHub: [@Piratheepan22](https://github.com/Piratheepan22)
- Project Repository: [Disaster-damage-assesment_Change-detection](https://github.com/Piratheepan22/Disaster-damage-assesment_Change-detection)

**Final Year Project**
- Institution: *[University Name]*
- Supervisor: *[Supervisor Name]*

---

## 📜 License
This project is developed as an academic final-year engineering project. License details to be determined.

---

## 🙏 Acknowledgments
- **Google Earth Engine** for satellite imagery access
- **Hugging Face Transformers** for Vision Transformer implementations
- **PyTorch** community for deep learning tools
- Remote sensing research community for methodological inspiration