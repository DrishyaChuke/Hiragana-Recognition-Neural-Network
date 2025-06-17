# 📝 Handwritten Japanese Character Recognition — KMNIST Deep Learning Experiments

This repository contains my experiments and findings for handwritten Hiragana character recognition using the KMNIST dataset.  
I built and compared multiple fully connected neural network architectures to understand how model capacity and regularization affect performance.

---

## 📊 Dataset

- **Dataset:** KMNIST (70,000 grayscale 28×28 images)
  - 60,000 training samples
  - 10,000 test samples
- **Classes:** 10 Hiragana characters
- **Preprocessing:** 
  - Added explicit channel dimension  
  - Normalized pixel values to [0, 1]  
  - Flattened images for fully connected layers  
  - Labels handled as integer indices and one-hot vectors as needed

---

## 🧪 Experiments

### ✅ **Experiment 1 — Baseline Fully Connected Network**
- **Architecture:**
  - Input: 784-dim vector
  - Hidden Layers: [512 → Dropout(0.2) → 256 → Dropout(0.2)]
  - Output: 10 raw logits
- **Training:**
  - Optimizer: Adam (lr=0.001)
  - Loss: CrossEntropyLoss
  - Epochs: 50, Batch Size: 128
- **Results:**
  - **Test Accuracy:** 92.54%  
  - **Observation:** Good baseline. Near-zero training loss shows overfitting.

---

### ✅ **Experiment 2 — Weight Decay Regularization**
- **Same architecture** as Experiment 1
- **Change:** Added L2 weight decay (`1e-5`)
- **Validation split:** 20% of training set
- **Results:**
  - **Validation Accuracy:** 98.56%  
  - **Test Accuracy:** 92.48%  
  - **Observation:** Weight decay improved generalization on validation data.

---

### ✅ **Experiment 3 — Increased Capacity + Higher Dropout**
- **Architecture:**
  - Hidden Layers: [1024 → Dropout(0.5) → 512 → Dropout(0.5)]
- **Regularization:** Weight decay + higher dropout (0.5)
- **Results:**
  - **Validation Accuracy:** 96.78%  
  - **Test Accuracy:** 92.26%  
  - **Observation:** Larger model with aggressive dropout; slight drop in test performance — shows trade-off between capacity and over-regularization.

---

## 📈 Results Summary

| Experiment | Validation Accuracy | Test Accuracy |
|------------|---------------------|----------------|
| Exp 1      | —                   | **92.54%**     |
| Exp 2      | **98.56%**          | **92.48%**     |
| Exp 3      | **96.78%**          | **92.26%**     |

---

## 🔑 Key Takeaways

- **Baseline:** Simple networks can achieve solid results (~92%).
- **Regularization:** Weight decay helps generalization significantly.
- **Capacity vs Regularization:** Bigger networks need careful tuning of dropout and regularization to avoid under-utilizing model capacity.
- **Future Improvements:** Try CNNs, data augmentation, better hyperparameter tuning.

---
*Project Report (https://github.com/DrishyaChuke/Hiragana-Recognition-Neural-Network/blob/main/Report_PartB_25076922.pdf)
