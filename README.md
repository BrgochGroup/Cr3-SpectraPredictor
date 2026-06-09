# Cr3+SpectraPredictor

![Graphical Overview](TOC-01.jpg)

## Predicting Emission Wavelength and FWHM of Cr³⁺-Substituted Phosphors

Cr3+SpectraPredictor is a machine-learning framework for predicting the emission peak wavelength (λem) and full width at half maximum (FWHM) of Cr³⁺-substituted phosphors using compositional and structural descriptors.

By combining the predicted λem and FWHM values with a Gaussian function, an estimated emission spectrum can be generated for a target Cr³⁺ phosphor.

---

## 📑 Table of Contents

- [Citation](#-citation)
- [Prerequisites](#️-prerequisites)
- [Shannon Ionic Radius Descriptors](#-shannon-ionic-radius-descriptors)
- [Usage](#-usage)
  - [1. Define Features for the Emission Model](#1-define-features-for-the-emission-model)
  - [2. Define Features for the FWHM Model](#2-define-features-for-the-fwhm-model)
  - [3. Predict Emission Wavelength (λem)](#3-predict-emission-wavelength-λem)
  - [4. Predict FWHM](#4-predict-fwhm)
  - [5. Generate a Gaussian Emission Spectrum](#5-generate-a-gaussian-emission-spectrum)
- [Authors](#-authors)

---

## 📚 Citation

If you use this repository, please cite:

**Amit Kumar et al.**  
*Machine Learning-Assisted Discovery of Cr³⁺-Based NIR Phosphors* (Submitted).

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
```

Install them using:

```bash
pip install pymatgen catboost scikit-learn pandas numpy matplotlib openpyxl shap
```

---

## 📏 Shannon Ionic Radius Descriptors

The `1/R²` and `R5` descriptors are calculated from the Shannon ionic radius (`R`, in Å) of the cation site substituted by Cr³⁺.

| Cation | R (Å) | 1/R² | R⁵ |
|---------|------:|------:|------:|
| Al³⁺ | 0.535 | 3.495 | 0.043830 |
| Sb⁵⁺ | 0.600 | 2.778 | 0.077760 |
| Ti⁴⁺ | 0.605 | 2.733 | 0.081054 |
| Ga³⁺ | 0.620 | 2.601 | 0.091613 |
| Nb⁵⁺ | 0.640 | 2.441 | 0.107374 |
| Sn⁴⁺ | 0.690 | 2.100 | 0.156403 |
| Hf⁴⁺ | 0.710 | 1.984 | 0.180423 |
| Mg²⁺ | 0.720 | 1.929 | 0.193492 |
| Sc³⁺ | 0.745 | 1.802 | 0.229499 |
| In³⁺ | 0.800 | 1.563 | 0.327680 |

where

- `1/R² = 1/(R²)`
- `R5 = R⁵`

*R denotes the Shannon ionic radius (CN = 6) of the cation site occupied by Cr³⁺.*

---

## 🚀 Usage

### 1. Define Features for the Emission Model

Prepare the following files in the same directory:

- `Feature_generator.xlsx` containing the formulas for which predictions are desired
- Corresponding CIF files (`*.cif`)
- `elements.xlsx`

Run:

```text
em_features.ipynb
```

The notebook generates:

```text
To_predict_em.xlsx
```

#### Additional Features Required

This notebook generates **15 of the 20 features** required by the emission model. To complete `To_predict_em.xlsx`, the following descriptors must be added manually:

- `max_metal_ligand_bond_length`
- `mean_metal_ligand_bond_length`
- `polyhedron volume`
- `distortion_index`
- `1/R²`

The `1/R²` descriptor should be calculated using the Shannon ionic radii listed above.

---

### 2. Define Features for the FWHM Model

Prepare the following files in the same directory:

- `Feature_generator.xlsx` containing the formulas for which predictions are desired
- Corresponding CIF files (`*.cif`)
- `elements.xlsx`

Run:

```text
fwhm_features.ipynb
```

The notebook generates:

```text
To_predict_fwhm.xlsx
```

#### Additional Features Required

This notebook generates **13 of the 18 features** required by the FWHM model. To complete `To_predict_fwhm.xlsx`, the following descriptors must be added manually:

- `max_metal_ligand_bond_length`
- `mean_metal_ligand_bond_length`
- `polyhedron volume`
- `x` (Cr³⁺ dopant concentration)
- `R5`

The `R5` descriptor should be calculated using the Shannon ionic radii listed above.

---

### 3. Predict Emission Wavelength (λem)

After preparing `To_predict_em.xlsx`, place it in the same directory as:

- `trainingset_em.xlsx`
- `em_model.py`

Run:

```bash
python em_model.py
```

The model generates:

```text
predicted_em.xlsx
```

containing the predicted emission wavelength (λem) values for all compounds listed in `To_predict_em.xlsx`.

---

### 4. Predict FWHM

After preparing `To_predict_fwhm.xlsx`, place it in the same directory as:

- `trainingset_fwhm.xlsx`
- `fwhm_model.py`

Run:

```bash
python fwhm_model.py
```

The model generates:

```text
predicted_fwhm.xlsx
```

containing the predicted FWHM values for all compounds listed in `To_predict_fwhm.xlsx`.

---

### 5. Generate a Gaussian Emission Spectrum

After obtaining the predicted λem and FWHM values, an approximate emission spectrum can be generated using a Gaussian profile:

\[
I(\lambda)=I_0 \exp\left[-4\ln(2)\left(\frac{\lambda-\lambda_{em}}{\mathrm{FWHM}}\right)^2\right]
\]

where:

- λ = wavelength
- λem = predicted emission peak wavelength
- FWHM = predicted full width at half maximum
- I₀ = peak intensity

The predicted λem and FWHM values can be combined with the Gaussian function above to generate an estimated emission spectrum for the target Cr³⁺ phosphor.

---

## 👨‍💻 Authors

**Amit Kumar**  
Department of Chemistry  
University of Houston

**Jakoah Brgoch**  
Department of Chemistry  
University of Houston
