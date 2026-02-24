# Disaster Damage Assessment - Change Detection

## Project Overview
This repository contains a comprehensive framework for assessing disaster damage using change detection methodologies. It offers tools for analyzing satellite imagery before and after a disaster to determine the extent of damage and to support recovery efforts.

## Folder Structure
```
Disaster-damage-assessment/
├── src/                  # Source code for the project
│   ├── main.py          # Main application file
│   ├── utils.py         # Utility functions
│   ├── models/          # Model definitions
│   └── ...              # Other necessary code files
├── data/                 # Dataset storage
│   ├── raw/             # Raw data files
│   ├── processed/       # Processed data files
│   └── ...              # Other data-related folders
├── docs/                # Documentation files
├── README.md            # Project documentation
└── requirements.txt      # Required packages
```

## Installation Instructions
1. **Clone the repository**:
   ```bash
   git clone https://github.com/Piratheepan22/Disaster-damage-assessment_Change-detection.git
   ```
2. **Change directory**:
   ```bash
   cd Disaster-damage-assessment_Change-detection
   ```
3. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

## Model Architecture
The model architecture includes convolutional neural networks (CNNs) designed to extract features from satellite images. Key components include:
- Input layer 
- Multiple convolutional layers for feature extraction
- Pooling layers for down-sampling
- Fully connected layers for classification

## Dataset Details
The dataset consists of satellite images collected pre- and post-disaster, organized into the following categories:
- **Category A:** Images from natural disasters (e.g., floods, hurricanes)
- **Category B:** Images from human-made disasters (e.g., industrial accidents)

Dataset size: Approximately XX GB with XX images. 

## Features
- Robust change detection algorithms
- User-friendly interface for visualization of results
- API support for integration with other applications

## Usage Examples
1. **Running the Model**:
   ```bash
   python src/main.py --input data/raw/your_image.jpg
   ```
2. **Generating Reports**:
   Useful for assessing recovery needs after a disaster. 
   ```bash
   python src/report_generator.py --input data/processed/your_results.json
   ```

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments
- Thank you to the contributors who make this project possible.

---

For further queries or contributions, please reach out to the maintainers.