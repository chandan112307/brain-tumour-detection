# Brain Tumor Detection – Fix Plan

## Core Problem
This repository currently behaves as a demo system, not a real AI model. The model is not trained, no real dataset is used, and inference does not use learned weights.

---

## Required Fixes

### 1. Use Trained Model Weights
- Train model using real dataset
- Save weights (best_model.pth)
- Load weights in backend/main.py
- Set model to evaluation mode

---

### 2. Remove Fake Segmentation
- Delete _make_demo_mask()
- Remove all rule-based segmentation logic
- Only use model predictions

---

### 3. Replace Synthetic Data
- Remove artificial tumor generation
- Use BraTS dataset (MRI scans)

---

### 4. Implement Real Dataset Loader
- Load .nii / .nii.gz files
- Extract 4 modalities (T1, T1c, T2, FLAIR)
- Stack into 4-channel tensor
- Load segmentation masks

---

### 5. Fix Input Mismatch
Option A (recommended):
- Use 4-channel MRI input

Option B:
- Modify model to accept 1 channel
- Retrain model

---

### 6. Connect Training and Inference
- Ensure train.py saves model
- Ensure main.py loads same model

---

### 7. Remove Fake Metrics
- Remove Dice score from inference
- Compute Dice only during training/validation using ground truth

---

### 8. Clean Inference Pipeline
Final flow:
input → preprocessing → model → output mask

Remove:
- thresholding
- brightness logic
- manual masks

---

## Final Outcome
After fixes:
- Real deep learning model
- Real MRI-based segmentation
- Valid predictions
- Meaningful evaluation
