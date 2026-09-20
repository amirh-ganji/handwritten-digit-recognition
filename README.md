# ✍️ Handwritten Digit Recognition

Comparison of four classifiers (Random Forest, SVM, ANN, KNN) on the scikit-learn handwritten digits dataset, implemented in a Jupyter notebook.

## 🗂️ Dataset

- **Source:** Optical Recognition of Handwritten Digits, loaded via `sklearn.datasets.load_digits`
- **Size:** 1,797 samples, each an 8×8 grayscale image (64 features, pixel values 0–16)
- **Task:** Multi-class classification into 10 classes (digits 0–9)

## ⚙️ Preprocessing

- Stratified 70/30 train/test split with `random_state=42` (1,257 train / 540 test samples)
- Min-Max scaling to [0, 1], fitted on the training data only and applied to the test data

## 🤖 Models

| Model | Main settings |
| ----- | ------------- |
| Random Forest (RF) | `n_estimators=256`, `max_depth=128`, `random_state=42` |
| SVM | defaults (RBF kernel) |
| ANN (MLPClassifier) | `hidden_layer_sizes=256`, `max_iter=500`, `random_state=42` |
| K-Nearest Neighbors (KNN) | `n_neighbors=8` |

## 📈 Evaluation Metrics

- Accuracy on the train and test sets
- Precision and recall on the test set, weighted by class support (for a multi-class problem, weighted recall is mathematically equal to accuracy)
- Stratified 5-fold cross-validation with accuracy and macro F1

## 📊 Results

### Single train/test split

| Model | Train Acc. | Test Acc. | Precision | Recall |
| ----- | ---------- | --------- | --------- | ------ |
| RF | 1.0000 | 0.9648 | 0.9662 | 0.9648 |
| SVM | 0.9984 | 0.9907 | 0.9909 | 0.9907 |
| ANN | 1.0000 | 0.9833 | 0.9836 | 0.9833 |
| KNN | 0.9873 | 0.9796 | 0.9803 | 0.9796 |

### Stratified 5-fold cross-validation

The scaler is part of the pipeline, so it is fitted on the training folds only.

| Model | CV Accuracy (mean ± std) | CV Macro F1 (mean ± std) |
| ----- | ------------------------ | ------------------------ |
| RF | 0.9783 ± 0.0048 | 0.9783 ± 0.0049 |
| SVM | 0.9878 ± 0.0042 | 0.9877 ± 0.0042 |
| ANN | 0.9833 ± 0.0035 | 0.9833 ± 0.0035 |
| KNN | 0.9827 ± 0.0064 | 0.9827 ± 0.0064 |

### Notes

- SVM has the highest accuracy in both evaluations and Random Forest the lowest. The gaps among SVM, ANN and KNN are within about one standard deviation in cross-validation.
- Random Forest and ANN reach (almost) 100% training accuracy, so the gap between train and test accuracy is largest for them.
- Hyperparameters were set by hand and were not tuned.

## 🚀 How to Run

```
git clone https://github.com/amirh-ganji/handwritten-digit-recognition.git
cd handwritten-digit-recognition
pip install scikit-learn matplotlib jupyter
jupyter notebook computer_vision.ipynb
```

Run all cells from top to bottom. Results are seeded, but small differences can appear across scikit-learn versions.

## 📁 Structure

```
├── computer_vision.ipynb   # Data loading, preprocessing, models, comparison, cross-validation
├── LICENSE
└── README.md
```

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
