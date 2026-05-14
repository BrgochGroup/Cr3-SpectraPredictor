# Cr3+-SpectraPredictor

## Predicting Emission Wavelength and FWHM of Cr³⁺-Substituted Phosphors

This repository provides machine learning models for predicting the photoluminescence emission wavelength (λem) and full width at half maximum (FWHM) of Cr³⁺-substituted phosphors using compositional and structural descriptors.

The models were trained on experimentally reported Cr³⁺ emission data and use reduced feature sets selected from a larger descriptor pool. The final λem model uses the top 20 selected features, while the final FWHM model uses the top 16 selected features.

---

## 📑 Table of Contents

- 📚 Citations
- ⚙️ Prerequisites
- 🚀 Usage
- 📄 Define Composition Features
- 🏗️ Define Structural Features
- 📄 Define the Prediction Set
- 🔮 Predict λem and FWHM
- 👨‍💻 Authors

---

## 📚 Citations

To cite the Cr³⁺ emission and FWHM prediction models, please reference the following work:

Amit Kumar, et al., “Machine Learning-Assisted Discovery of Cr³⁺-Based NIR Phosphors” (Submitted).

---

## ⚙️ Prerequisites

This package requires the following Python libraries:

```text
pymatgen
catboost
scikit-learn
pandas
numpy
matplotlib
openpyxl
shap
