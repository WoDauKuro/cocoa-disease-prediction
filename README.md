# Cocoa Bean Contamination Detection

A computer vision system for detecting diseased cocoa beans using YOLOv8 object detection. Identifies three classes: Anthracnose (fungal disease), CSSVD (Cocoa Swollen Shoot Virus Disease), and healthy beans.

## 🧠 Project Overview

This project is part of the [Amini Cocoa Contamination Challenge](https://zindi.africa/competitions/amini-cocoa-contamination-challenge), which focuses on identifying visual symptoms of cocoa diseases — **Anthracnose** and **CSSVD** — using object detection techniques. The goal is to support early disease detection to improve cocoa crop yield and farmer outcomes.

## 📂 Dataset

The dataset used in this project is available from these sources:

- **Zindi Africa**: [Amini Cocoa Contamination Challenge](https://zindi.africa/competitions/amini-cocoa-contamination-challenge/data)
- **Kaggle**: [Amini Cocoa Contamination Dataset](https://www.kaggle.com/datasets/ohagwucollinspatrick/amini-cocoa-contamination-dataset)

## 📊 Results

### Model Performance (After 50 epochs)

| Class          | Images | Instances | Precision | Recall | mAP@0.5 | mAP@0.5-0.95 |
|----------------|--------|-----------|-----------|--------|---------|--------------|
| **all**        | 830    | 1556      | 0.752     | 0.671  | 0.743   | 0.505        |
| anthracnose    | 252    | 385       | 0.768     | 0.655  | 0.738   | 0.502        |
| cssvd          | 306    | 465       | 0.755     | 0.673  | 0.733   | 0.514        |
| healthy        | 272    | 706       | 0.733     | 0.686  | 0.758   | 0.500        |

### Validation Metrics

| Class          | Precision | Recall | mAP@0.5 | mAP@0.5-0.95 |
|----------------|-----------|--------|---------|--------------|
| **all**        | 0.757     | 0.665  | 0.742   | 0.504        |
| anthracnose    | 0.772     | 0.647  | 0.736   | 0.500        |
| cssvd          | 0.759     | 0.671  | 0.733   | 0.515        |
| healthy        | 0.741     | 0.677  | 0.758   | 0.499        |

### Final Submission Distribution

| Class          | Count |
|----------------|-------|
| healthy        | 1433  |
| cssvd          | 958   |
| anthracnose    | 733   |
| None           | 17    |

## 🔧 Potential Improvements

While the model achieved promising results within the allowed training time, there are several areas for potential improvement:

- **Extended Training Time**: The challenge permitted up to ~9 hours for model training, but this implementation only used approximately **2 hours and 20 minutes** on a Kaggle Notebook with a **P100 GPU**. Utilizing the full training window could allow for:
  - More training epochs
  - Improved convergence
  - Better generalization

- **Data Augmentation**: Additional augmentation techniques such as MixUp, Mosaic, CutMix, or random erasing could help the model become more robust to variations in bean appearance and backgrounds.

- **Hyperparameter Tuning**: Exploring different learning rates, batch sizes, and image sizes may yield performance improvements.

- **Model Architecture**: While YOLOv8 performed well, experimenting with larger YOLOv8 variants (e.g., `yolov8m` or `yolov8l`) or alternative architectures (like Faster R-CNN or EfficientDet) could enhance accuracy — given more compute time.

- **Ensembling**: Combining predictions from multiple models trained with different seeds or architectures could improve final predictions.


## Dataset Preparation

### Dataset structure:

    dataset/
    ├── images/
    │   ├── train/
    │   ├── val/
    │   └── test/
    └── labels/
        ├── train/
        └── val/

## Training Configuration

    # data.yaml
    path: /path/to/dataset
    train: images/train
    val: images/val
    test: images/test
    nc: 3
    names: ['anthracnose', 'cssvd', 'healthy']

## 💻 Training Environment

The model was trained on [Kaggle Notebooks](https://www.kaggle.com/code) using a **P100 GPU accelerator**. Training took approximately **2 hours and 20 minutes** for 50 epochs.

## Pretrained Model

The best performing model weights (`best.pt`) are included in this repository:

```bash
# Download the pretrained model
wget https://github.com/WoDauKuro/cocoa-disease-prediction/blob/main/best.pt