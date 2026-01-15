# ECG PVC Arrhythmia Detection Using Discrete Wavelet Transform

**Author:** Laurie Camila Hernández Pacheco

---

## 📋 Project Overview

This project implements an automated ECG arrhythmia detection system using **Discrete Wavelet Transform (DWT)** for feature extraction and **k-Nearest Neighbors (k-NN)** for classification. The system focuses on distinguishing between normal heartbeats and **Premature Ventricular Contractions (PVCs)** using the MIT-BIH Arrhythmia Database.

The project demonstrates how a mathematically rigorous yet computationally simple approach can achieve clinically relevant performance, making it a promising solution for resource-constrained healthcare settings requiring immediate arrhythmia screening.

---

## 🎯 Objectives

- Extract discriminative features from ECG signals using multi-resolution wavelet decomposition
- Identify statistically significant features through rigorous hypothesis testing
- Build and optimize a lightweight k-NN classifier for real-time arrhythmia detection
- Validate model performance using patient-level data splitting to ensure generalizability

---

## 🔬 Methodology

### 1. **Data Collection**
- **Dataset:** MIT-BIH Arrhythmia Database (48 records)
- **Classes:** Normal beats (N) and Ventricular ectopic beats (V/PVCs)
- **Sample Size:** 50 normal + 50 PVC beats randomly sampled across multiple patients

### 2. **Signal Processing Pipeline**
```
ECG Signal → Preprocessing → Beat Segmentation → DWT Decomposition → Feature Extraction
```

- **Preprocessing:** Baseline wander removal (0.5 Hz high-pass Butterworth filter) and normalization
- **Segmentation:** 300ms windows centered on R-peaks
- **DWT:** 4-level decomposition using Daubechies-4 (db4) wavelet
- **Features:** Energy, mean, standard deviation, maximum, and Shannon entropy for each decomposition level

### 3. **Statistical Analysis**
- Normality testing using Shapiro-Wilk test
- Hypothesis testing with t-tests (parametric) and Mann-Whitney U tests (non-parametric)
- Feature ranking based on statistical significance (p-values)

### 4. **Classification**
- **Algorithm:** k-Nearest Neighbors (k-NN)
- **Feature Selection:** Top N most discriminative features (optimized through experiments)
- **Validation:** Patient-level train/test split (70/30) to prevent data leakage
- **Optimization:** Cross-validation for hyperparameter tuning

---

## 📊 Key Results

### Final Model Performance

The optimized model uses only **two features** from the detail coefficient level 4 (cD4):
- `cD4_max`: Maximum wavelet coefficient (captures sharp QRS features)
- `cD4_entropy`: Shannon entropy (quantifies signal irregularity)

| Metric        | Value   |
|---------------|---------|
| **Accuracy**  | 82.76%  |
| **Precision** | 89.47%  |
| **Recall**    | 85.00%  |
| **Specificity** | 77.78% |
| **F1-Score**  | 87.18%  |

### Key Insights

✅ **High Precision (89.47%)**: When the model predicts a PVC, it is correct ~90% of the time, minimizing false alarms  
✅ **Strong Recall (85%)**: Successfully identifies 85% of actual PVC events—critical for clinical safety  
✅ **Minimal Feature Set**: Using only 2 features improves computational efficiency and reduces overfitting risk  
✅ **Patient-Level Generalization**: Model validated on entirely new patients, ensuring real-world applicability  
✅ **Frequency Band Insight**: Most discriminative information lies in the 11-22 Hz range (cD4), corresponding to QRS complex morphology

---

## 🧮 Why Discrete Wavelet Transform?

Unlike Fourier Transform (global frequency analysis), DWT provides:
- **Multi-resolution analysis**: Captures both time and frequency information
- **Localized features**: Detects transient morphological changes in heartbeats
- **Physiological alignment**: Decomposition levels correspond to ECG wave components
  - cD3 (22-45 Hz): QRS complex energy
  - cD4 (11-22 Hz): QRS + P/T waves
  - cA (0-11 Hz): Baseline trends

This makes DWT particularly well-suited for identifying arrhythmias with distinct morphological signatures like PVCs (wide, distorted QRS complexes).

---

## 📁 Repository Structure
```
├── ecg_arrhythmia_detection.ipynb   # Main Jupyter notebook
├── README.md                         # This file
├── requirements.txt                  # Python dependencies
└── report/                           # LaTeX report (coming soon)
```

---

## 🛠️ Technologies Used

- **Python 3.11+**
- **Signal Processing:** `pywt` (PyWavelets), `scipy`
- **Machine Learning:** `scikit-learn`
- **Data Handling:** `numpy`, `pandas`
- **Visualization:** `matplotlib`, `seaborn`
- **ECG Data:** `wfdb` (PhysioNet)

---

## 📈 Future Improvements

- **Increase specificity**: Address false positive rate (currently 22%) through ensemble methods or additional features
- **Multi-class classification**: Extend to other arrhythmia types (atrial fibrillation, bundle branch blocks, etc.)
- **Wavelet family comparison**: Experiment with Symlet, Coiflet, and Biorthogonal wavelets
- **Deep learning integration**: Explore hybrid DWT-CNN architectures for improved performance
- **Real-time deployment**: Optimize for embedded systems and wearable ECG monitors

---

## 🎓 Educational Value

This project demonstrates:
- Deep understanding of wavelet mathematics and signal processing
- Rigorous statistical methodology (normality testing, hypothesis testing, p-values)
- Proper machine learning practices (data leakage prevention, patient-level splitting, cross-validation)
- Interpretable feature engineering for medical applications
- End-to-end ML pipeline development

Ideal for:
- Data science portfolio projects
- Biomedical signal processing coursework
- Introduction to wavelet-based feature extraction
- Healthcare AI applications

---

## 📝 Citation

If you use this code or methodology in your research, please cite:
```
Hernández, L. (2026). ECG PVC Arrhythmia Detection Using Discrete Wavelet Transform. 
GitHub repository: https://github.com/lhdz12/PVC-Arrhythmia-Detection-DWT-KNN
```

---

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

---

## 🙏 Acknowledgments

- **MIT-BIH Arrhythmia Database** (PhysioNet) for providing open-access ECG data
- **PyWavelets** community for wavelet transform implementation
- Research papers on DWT-based arrhythmia detection that inspired this work

---

## 📧 Contact

**Laurie Hernández**  
Data Science and Mathematics Engineering Student  
📧 [lauriehernandez.1208@gmail.com]  
🔗 [LinkedIn](https://www.linkedin.com/in/lhdz12/)  
🔗 [GitHub](https://github.com/lhdz12)

---

**Note:** Detailed mathematical derivations, methodology, and comprehensive analysis are available in the accompanying LaTeX report (coming soon).