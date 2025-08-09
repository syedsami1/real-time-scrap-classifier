# Real-Time Scrap Classifier & Robotic Pick Simulation

Lightweight, end-to-end computer vision mini-project for automated scrap material sorting, built with **YOLOv8**, **OpenCV**, and a subset of **TrashNet** dataset, optimized for running in Google Colab (CPU).

---

## 📌 Overview

This project simulates an **AI-powered sorting system** for recyclable materials on a conveyor belt. The goal is to detect scrap objects in real time, classify them into categories, and determine precise **pick points** where a robotic arm could grab them.

It is **not a production-grade system**, but a **mini proof-of-concept** that covers all stages of a vision pipeline — dataset preparation, model training, inference, and visualization — while staying lightweight enough for students and quick demos.

---

## 🎯 Objectives

- **Dataset Prep**: Use a small public dataset (TrashNet subset) and generate annotations
- **Object Detection**: Train/fine-tune YOLOv8 Nano on scrap categories
- **Simulation**: Mimic a conveyor belt environment with sequential images
- **Pick-Point Generation**: Calculate center coordinates for robot grasping
- **Latency Logging**: Measure and display inference speed
- **Lightweight Design**: Runs on CPU with <100 images for fast demonstrations

---

## 🏗 System Workflow

```
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   TrashNet      │───▶│  Preprocessing   │───▶│  YOLOv8 Nano    │
│   Dataset       │    │  & Annotation    │    │  Training       │
└─────────────────┘    └──────────────────┘    └─────────────────┘
                                                          │
                                                          ▼
┌─────────────────┐    ┌──────────────────┐    ┌─────────────────┐
│   OpenCV        │◀───│   Pick Points    │◀───│   Real-time     │
│   Display       │    │   + Crosshairs   │    │   Inference     │
└─────────────────┘    └──────────────────┘    └─────────────────┘
```

### Detailed Pipeline Flow
```
Input Images → YOLOv8 Detection → Bounding Boxes → Pick Point Calculation → OpenCV Display
     ↓              ↓                   ↓                ↓                    ↓
  640x640px    Confidence Scores    Center Coords    Crosshair Overlay   Frame Display
```

---

## 🛠 Technology Stack

| Component | Tool | Purpose |
|-----------|------|---------|
| **Object Detection** | YOLOv8 Nano | Lightweight model for CPU inference |
| **Computer Vision** | OpenCV | Image processing and visualization |
| **Dataset** | TrashNet subset | 60 images across 6 categories |
| **Training** | Ultralytics | Model training and inference |
| **Platform** | Google Colab | CPU-optimized environment |

---

## 🔍 Implementation Details

### Data Processing
- **Dataset**: TrashNet subset (10 images per class: cardboard, glass, metal, paper, plastic, trash)
- **Annotations**: Full-image bounding boxes as simplified labels
- **Augmentation**: Rotation, scaling, color shifts to improve generalization

### Model Training
- **Architecture**: YOLOv8 Nano (3.2M parameters, 6.2MB model)
- **Training**: 15 epochs with data augmentation
- **Optimization**: Balanced for speed/accuracy on CPU hardware

### Real-time Simulation
- **Conveyor Simulation**: Sequential image display mimicking belt movement
- **Processing Pipeline**: Detection → Classification → Pick Point → OpenCV Display
- **Performance Monitoring**: Real-time latency measurement printed to console

---

## 📊 Performance Results

### Detection Accuracy
| Class | Avg Confidence | Detection Rate |
|-------|----------------|----------------|
| Cardboard | 0.68 | 85% |
| Metal | 0.72 | 80% |
| Glass | 0.45 | 60% |
| Plastic | 0.52 | 65% |
| Paper | 0.41 | 55% |
| Trash | 0.38 | 50% |

### System Performance
- **Inference Speed**: 78ms per frame (~13 FPS)
- **Model Size**: 6.2MB (deployment-ready)
- **Memory Usage**: ~150MB during inference
- **Platform**: Google Colab CPU environment

---

## ⚠️ Challenges & Learnings

### Technical Challenges
- **Small dataset** led to overfitting on specific visual patterns
- **Full-image bounding boxes** don't represent real object detection complexity
- **Confidence threshold tuning** critical for balancing precision vs. recall
- **CPU constraints** required careful model and parameter selection

### Key Takeaways
- Data quality and annotation precision are crucial for robust detection
- Lightweight models can achieve reasonable performance with proper optimization
- Real-time processing requires careful balance of accuracy and speed
- Proof-of-concept demonstrations need clear scope and limitation documentation

---

## 🚀 Future Enhancements

- Use precise bounding box annotations for improved localization accuracy
- Deploy on edge hardware (Jetson Nano, Coral TPU) for better performance
- Add object tracking to smooth detection consistency across frames

---
