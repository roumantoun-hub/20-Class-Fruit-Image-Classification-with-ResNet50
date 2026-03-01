# 🍎 20-Class Fruit Image Classification with ResNet50

This project implements a deep learning pipeline for multi-class fruit image classification using transfer learning with ResNet50.

---

## 📦 Dataset

**Source:** Fruits-360 (Kaggle – moltean/fruits)  
**Original dataset:** 131,030 images, 251 classes  
**Selected subset:** 20 classes  
**Total images used:** 16,081  

### Dataset Split

| Split | Images |
|-------|--------|
| Train | 9,645 |
| Validation | 2,422 |
| Test | 4,014 |

Images are resized to **224×224**.

---

## 🧠 Model Architecture

### Structure

```text
Input (224, 224, 3)
  ↓
ResNet50 (include_top=False, pretrained, frozen)
  ↓
GlobalAveragePooling2D
  ↓
Dense(20, softmax)
```


### Parameters

- **Total parameters:** 23,628,692  
- **Trainable parameters:** 40,980  
- **Frozen parameters:** 23,587,712  

Only the final classification layer is trained.

---

## ⚙️ Training Configuration

- Optimizer: SGD (lr=0.001, momentum=0.9)  
- Loss: sparse_categorical_crossentropy  
- Batch size: 32  
- Epochs: 15  
- Callback: ModelCheckpoint (best by val_loss)  

### Data Augmentation

Training data includes:

- Random horizontal flip  
- Random rotation (0.35)  
- Random translation (0.25)  
- Random zoom (0.35)  
- Random contrast (0.45)  
- Color jitter  
- Gaussian noise  

Validation and test datasets are not augmented.

---

## 📊 Performance

Test results:

- **Accuracy:** 0.9195  
- **Macro Precision:** 0.9338  
- **Macro Recall:** 0.9202  
- **Macro F1-score:** 0.9162  

Most errors occur between visually similar fruit variants.

---

## 🚀 How to Run

### 1) Install Dependencies
```bash
pip install tensorflow matplotlib scikit-learn kaggle
```

### 2) Download the Dataset (Kaggle)
```bash
kaggle datasets download -d moltean/fruits
```

### 3) Extract the Archive
```bash
unzip fruits.zip
```

### 4) Run the Notebook
Open the notebook and execute the cells sequentially.

---

## ⚠️ Note

The trained model file (`best.keras`) is not included due to GitHub size limits.  
You can reproduce results by running the notebook.
