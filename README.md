# Cocoa Bean Contamination Detection

A computer vision system for detecting diseased cocoa beans using YOLOv8 object detection. Identifies three classes: Anthracnose (fungal disease), CSSVD (Cocoa Swollen Shoot Virus Disease), and healthy beans.

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

## Pretrained Model

The best performing model weights (`best.pt`) are included in this repository:

```bash
# Download the pretrained model
wget https://github.com/WoDauKuro/cocoa-disease-prediction/raw/main/best.pt