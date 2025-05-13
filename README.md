# 🚗 Level 4 Autonomous Vehicle Perception System
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.9](https://img.shields.io/badge/Python-3.9-3776AB.svg)](https://www.python.org/)
[![TensorFlow 2.15](https://img.shields.io/badge/TensorFlow-2.15-FF6F00.svg)](https://www.tensorflow.org/)
[![Edge TPU](https://img.shields.io/badge/Coral%20Edge%20TPU-Supported-success.svg)](https://coral.ai/)

**Real-Time Object Detection for Autonomous Navigation**  
Edge-optimized perception pipeline using EfficientDet-Lite models accelerated by Coral USB

---

## 🌟 Project Overview

This repository contains the complete perception stack for a **Level 4 Autonomous Vehicle** prototype developed as part of Queen's University's Engineering Design course. The system enables:

> *"Real-time detection and classification of road objects using edge-optimized deep learning models for autonomous navigation decisions."*

### Key Purpose
- 🚦 **Road Sign Recognition**: Identify regulatory/warning signs for path planning
- 🚸 **Pedestrian Detection**: Ensure safety in urban environments
- 🛣️ **Lane Obstacle Detection**: Navigate around static/dynamic obstacles

### Core Components
1. **Dataset Pipeline**: Tools for processing Pascal VOC annotations
2. **Model Training**: Colab-based workflow for EfficientDet-Lite models
3. **Edge Deployment**: Coral TPU-accelerated inference on Raspberry Pi
4. **Validation Suite**: Performance benchmarking tools

### Technical Highlights
```plaintext
┌───────────────────────┐
│   Frame Input         │  ← Raspberry Pi Camera
├───────────────────────┤
│   Object Detection    │  ← EfficientDet-Lite + Coral TPU
├───────────────────────┤
│   Decision Output     │  ← Navigation System Interface
└───────────────────────┘

```
---
## 📁 Project Structure

### 📦 Dataset

- **`signs_dataset`**  
  A folder containing the dataset in Pascal VOC format. It includes images and their corresponding XML annotation files for training the road sign detector. Make sure you zip the content within the folder after downloading the dataset.

### 🧪 Scripts

- **`split_dataset.py`**  
  Splits the dataset into training, validation, and test sets. Ensures proper evaluation of the model on unseen data.

- **`train_signs_model.py`**  
  Main training script (used in Google Colab). It:
  - Prepares and loads the dataset
  - Defines and trains an EfficientDet-lite model
  - Converts and exports the model as `.tflite` for deployment

- **`test_signs_model.py`**  
  Loads and tests the trained model on a sample image to verify inference before deployment.

- **`detect_signs.py`**  
  Deploys the trained model on a Raspberry Pi using the Coral TPU. Captures live video feed and detects road signs in real-time, drawing bounding boxes.

## 🚀 Getting Started

### ▶️ Training in Google Colab


1. Open the [Google Colab Notebook](https://colab.research.google.com/drive/1Kx320hERKWzCzEK7I96HtujaYpVlPO9D) or download the `.ipynb` notebook from this repository `Training of EfficientDet-Lite Detector for the Coral TPU (TF2) - Road Signs.ipynb` and import it into a newly created notebook in Google Colab
3. Upload the following files to the runtime:
   - `train_signs_model.py`
   - `split_dataset.py`
   -  `test_signs_model.py`
   -  `detect_signs.py`
   - `signs_dataset.zip` (after zipping the folder)
4. Follow the notebook to:
   - Train the model
   - Export a `.tflite` file (with or without EdgeTPU optimization)
      - With EdgeTPU optimization: `efficientdet-lite-signs_edgetpu.tflite`
      - Without EdgeTPU optimization: `efficientdet-lite-signs.tflite`
### 🤖 Deployment on Raspberry Pi

1. Copy the `.tflite` model and `signs-labels.txt` to a directory of your choice (in the Raspberry Pi)
2. Save `detect_signs.py` to another directory of your choice (in the Raspberry Pi)
3. Run the detection script:
```bash
python3 detect_signs.py
```


---

### Notebook Development Approach

This Jupyter Notebook (.ipynb) builds upon the tutorial materials provided in the Engineering Design course. While not a direct fork, the original notebook served as a template and reference for structuring the foundation of the object detection model's notebook. Key modifications include:

- Adapting the framework for autonomous vehicle-specific use cases.

- Implementing custom data pipelines, models, and visualizations.

- Expanding functionality to address [specific project goals, e.g., sensor integration, path planning, etc.].


Credit and gratitude to the original authors for the foundational structure.
