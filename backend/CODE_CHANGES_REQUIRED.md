# Code Changes (Direct Implementation Guide)

## main.py (Inference Fix)

### Add weight loading after model init
- Load: backend/models/best_model.pth
- Move model to device
- Set model.eval()

### Remove completely
- _make_demo_mask()
- Any fallback logic
- Any thresholding / brightness masking

### Final flow must be:
- preprocess input
- pass through model
- apply sigmoid/softmax
- return mask

---

## train.py (Training Fix)

### Remove
- Synthetic data generation (ellipses, fake tumors)

### Add
- Real dataset loader (BraTS)
- Validation loop
- Save best model:
  torch.save(model.state_dict(), "backend/models/best_model.pth")

---

## model.py (Input Fix)

### Ensure consistency

Option A (recommended):
- input channels = 4

Option B:
- change first layer to 1 channel
- retrain model

---

## Dataset (New Requirement)

Create loader:
- Read .nii/.nii.gz
- Extract 4 modalities
- Normalize
- Stack → [4, H, W]
- Load mask

---

## Remove Fake Metrics

- Delete Dice score from main.py
- Keep Dice only in training with ground truth

---

## Final Expected Behavior

- No output without model
- No fake masks
- No rule-based logic
- Output strictly from trained model
