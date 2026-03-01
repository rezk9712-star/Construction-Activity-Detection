# Construction Activities Detection – YOLOv8 (FMP8 v2)

## Project Overview
This project trains a YOLOv8 object detection model to recognize construction activities using a Roboflow dataset with 9 classes: Concrete, Concrete Float, Concrete Mixer Truck, Concrete Pump Hose, Concrete Pump Truck, Concrete Trowel, Excavation, Steel-Reinforcement, and Excavator.

---

## Final Model Metrics (YOLOv8m – Validation Set)

| Metric              | Value  |
|---------------------|--------|
| **Mean Precision**  | 0.7934 |
| **Mean Recall**     | 0.3613 |
| **mAP50**           | 0.4536 |
| **mAP50-95**        | 0.3074 |

### Per-Class Breakdown

| Class                | Precision | Recall | mAP50  | mAP50-95 |
|----------------------|-----------|--------|--------|----------|
| Concrete             | 0.817     | 0.769  | 0.772  | 0.578    |
| Concrete Pump Hose   | 1.000     | 0.000  | 0.017  | 0.002    |
| Concrete Pump Truck  | 0.999     | 0.667  | 0.913  | 0.575    |
| Excavation           | 0.432     | 0.154  | 0.205  | 0.069    |
| Steel-Reinforcement  | 0.602     | 0.123  | 0.200  | 0.123    |
| Excavator            | 0.910     | 0.455  | 0.616  | 0.496    |

---

## Evidence (all files flat in /results/evidence/)

| File | Description |
|------|-------------|
| `annotation_examples_01.png` – `annotation_examples_05.png` | Ground-truth bounding box overlays |
| `val_predictions_01.png` – `val_predictions_10.png` | Model predictions on validation images |
| `unseen_predictions_01.png` – `unseen_predictions_05.png` | Model predictions on new/unseen images |

---

## Notes
- Model: YOLOv8m (medium), trained for 50 epochs on Roboflow dataset `construction-activities-fmp8 v2`
- Dataset: 125 train images, 25 validation images
- Hardware: Google Colab T4 GPU
- Best weights: `/content/runs/detect/train2/weights/best.pt`
