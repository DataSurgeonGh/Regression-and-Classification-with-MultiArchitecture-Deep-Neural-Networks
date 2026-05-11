# Regression and Classification with Multi-Architecture Deep Neural Networks

> A deep learning project in R exploring temperature forecasting and digit classification using multiple neural network architectures — built as part of a PhD-level Algorithms for Data Science course.

---

## Overview

This project applies and compares multiple deep neural network (DNN) architectures to two well-known benchmark problems:

- **Regression** — forecasting hourly air temperature 24 hours ahead using the [Jena Climate dataset]Can be found at this url: (https://www.kaggle.com/datasets/mnassrib/jena-climate) (2009–2016)
- **Classification** — multi-class digit recognition using the [MNIST dataset] MNIST R dataset

All models are implemented in **R** using `keras3` and `tensorflow`, and the analysis is written in **Quarto** (`.qmd`), rendered to PDF.

---

## Project Structure

```
.
├── DNN_project1.qmd                          # Main Quarto analysis file
├── DNN-project1.pdf                          # Rendered PDF report
├── Regression and Classification with
│   MultiArchitecture (Deep) Neural
│   Networks.qmd                              # Additional Quarto document
├── datasets/                                 # Dataset files
├── images/                                   # Figures and plots
├── DNN_project1_files/figure-pdf/            # Auto-generated figures
├── DNN_project1_cache/                       # Quarto render cache
├── renv/                                     # R package environment (renv)
├── renv.lock                                 # Locked package versions
├── _quarto.yml                               # Quarto project config
└── .Rprofile                                 # R session config
```

---

## Datasets

### Jena Climate Dataset
- Meteorological time series recorded at the Max Planck Institute for Biogeochemistry, Jena, Germany
- Original resolution: every **10 minutes** (2009–2016)
- Resampled to **hourly** for modelling
- 14 features including temperature, pressure, humidity, wind speed, etc.
- **Task:** Predict temperature 24 hours ahead (regression); classify temperature into quartile-based categories — Cold / Cool / Mild / Warm (classification)
- **Split:** Training (2009–2014) | Validation (2015) | Test (2016)

### MNIST Dataset
- 70,000 grayscale images of handwritten digits (0–9), 28×28 pixels
- Split: 50,000 training | 10,000 validation | 10,000 test
- **Task:** Multi-class digit classification (10 classes)
- Dataset is approximately class-balanced (~10% per class)

---

## Methods

### Baseline / Naive Models
- **Jena Climate:** Naive model that predicts the current temperature as the future temperature — achieves MAE ≈ 0.30 (scaled units)
- **MNIST:** Random prediction baseline — achieves ~10% accuracy

### Neural Network Architectures Compared

**Jena Climate (Regression & Classification)**
- Baseline DNN (no regularization)
- DNN with Dropout
- DNN with L2 (Weight Decay) regularization
- Recurrent architectures (GRU / LSTM variants)

**MNIST (Classification)**
- Densely connected (MLP) networks
- Convolutional Neural Networks (CNNs)
- Variants with Batch Normalization, Dropout, and data augmentation

### Training Details
- Optimizer: Adam (lr = 0.001)
- Loss: MAE for regression; Categorical Cross-Entropy for classification
- Early stopping with patience and best-weight restoration
- Custom time-series data generator (sliding window, lookback = 120 hours, delay = 24 hours)

---

## Requirements

### R Packages

```r
library(keras3)
library(tensorflow)
library(reticulate)
library(ggplot2)
library(dplyr)
library(lubridate)
library(forecast)
library(corrplot)
library(tidyr)
library(reshape2)
library(gridExtra)
library(knitr)
library(kableExtra)
library(janitor)
```

This project uses `renv` for reproducible package management. To restore the exact environment:

```r
renv::restore()
```

### Python / Conda Environment

A conda environment named `r-tensorflow` is required for Keras/TensorFlow backend:

```r
library(reticulate)
use_condaenv("r-tensorflow", required = TRUE)
```

### Software
- R ≥ 4.x
- Quarto ≥ 1.x
- Python ≥ 3.9 with TensorFlow installed in the `r-tensorflow` conda environment

---

## Getting Started

1. **Clone the repository**

```bash
git clone https://github.com/DataSurgeonGh/Regression-and-Classification-with-MultiArchitecture-Deep-Neural-Networks.git
cd Regression-and-Classification-with-MultiArchitecture-Deep-Neural-Networks
```

2. **Restore R packages**

```r
renv::restore()
```

3. **Set up your conda environment** (if not already done)

```bash
conda create -n r-tensorflow python=3.10
conda activate r-tensorflow
pip install tensorflow
```

4. **Update the dataset path** in `DNN_project1.qmd`

```r
path <- "path/to/your/jena_climate_2009_2016.csv"
```

5. **Render the Quarto document**

```bash
quarto render DNN_project1.qmd
```

---

## Key Results

| Task | Model | Metric | Baseline | Best DNN |
|------|--------|--------|----------|----------|
| Jena Regression | DNN variants | MAE | ~0.30 | TBD |
| Jena Classification | DNN variants | Accuracy | Random | TBD |
| MNIST Classification | MLP / CNN | Accuracy | ~10% | TBD |

> Results are documented in full in [`DNN-project1.pdf`](./DNN-project1.pdf).

---

## Course Information

- **Course:** Algorithms for Data Science — Neural Networks Module (PhD Level)
- **Author:** Chanik Kwao-Agboado
- **Instructor:** William O. Agyapong, PhD

---
## References
> James, G., Witten, D., Hastie, T., & Tibshirani, R. (2021). 
> *An introduction to statistical learning: With applications in R* (2nd ed.).

Willian Agyapong,(2026, April). Neural Networks and Deep Neural Nets [Lecture notes]. Department of Mathematical Statistics, Kwame Nkrumah University of Science and Technology

---
## License

This project is for academic and educational purposes.
