# Regression-and-Classification-with-MultiArchitecture-Deep-Neural-Networks
A repo for deep learning works for Jena Climate data and MNIST data
### Overview
This project applies and compares multiple deep neural network (DNN) architectures to two well-known benchmark problems:

Regression — forecasting hourly air temperature 24 hours ahead using the Jena Climate dataset (2009–2016)
Classification — multi-class digit recognition using the MNIST dataset
All models are implemented in R using keras3 and tensorflow frameworks, and the analysis is written in Quarto (.qmd), rendered to PDF.

### Project Structure
.
├── DNN_project1.qmd                          # Main Quarto analysis file
├── DNN_project1.pdf                          # Rendered PDF report
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

### Dataset Summary
Jena Climate Dataset
Meteorological time series recorded at the Max Planck Institute for Biogeochemistry, Jena, Germany
Original resolution: every 10 minutes (2009–2016)
Resampled to hourly for modelling
14 features including temperature, pressure, humidity, wind speed, etc.
Task: Predict temperature 24 hours ahead (regression); classify temperature into quartile-based categories — Cold / Cool / Mild / Warm (classification)
Split: Training (2009–2014) | Validation (2015) | Test (2016)

## MNIST Dataset
70,000 grayscale images of handwritten digits (0–9), 28×28 pixels
Split: 50,000 training | 10,000 validation | 10,000 test
Task: Multi-class digit classification (10 classes)
Dataset is approximately class-balanced (~10% per class)

### Methodology
Baseline or Naive Models
Jena Climate: Naive model that predicts the current temperature as the future temperature — achieves MAE ≈ 0.30 (scaled units)
MNIST: Random prediction baseline — achieves ~10% accuracy

Neural Network Architectures Compared
Jena Climate (Regression & Classification)

#### Baseline DNN (no regularization)
DNN with Dropout
DNN with L2 (Weight Decay) regularization
Recurrent architectures (GRU / LSTM variants)

#### MNIST (Classification)
Densely connected (MLP) networks
Convolutional Neural Networks (CNNs)
Variants with Batch Normalization, Dropout, and data augmentation

#### Training Details
Optimizer: Adam (lr = 0.001)
Loss: MAE for regression; Categorical Cross-Entropy for classification
Early stopping with patience and best-weight restoration
Custom time-series data generator (sliding window, lookback = 120 hours, delay = 24 hours)

### Requirements
R Packages
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

