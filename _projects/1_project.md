---
layout: page
title: Gearbox fault diagnosis
description: Short IFD project done on a publicly available dataset.
img: assets/img/gearbox.jpg
importance: 1
category: work
related_publications: false
---
## Introduction

This project explores the application of Machine Learning (ML) in the field of mechanical engineering, specifically for gearbox fault diagnosis. The goal is to develop models that can accurately determine whether a gearbox is healthy or faulty based on vibration data from accelerometers. The comparison focuses on two ML models: Support Vector Machine (SVM) and Multilayer Perceptron (MLP).

## Problem statement

In many industrial processes, halting machinery for inspection can lead to significant losses. Thus, a reliable ML model capable of diagnosing gearbox faults using vibration data could prevent unnecessary downtimes. The dataset comprises accelerometer readings from gearboxes under various loads, labeled as 'Healthy' or 'Broken'. The challenge is to predict the gearbox condition based on these readings.

## Methodology

### Dataset Description:

Sourced from Kaggle, the dataset includes vibration data from four accelerometers placed on gearboxes under different loads. It contains 20 files: 10 for healthy gearboxes and 10 for gearboxes with a broken tooth, each under different load conditions (0% - 90%).

### Data Preprocessing:

Data points were segmented into windows and labeled. Fast Fourier Transform (FFT) was applied to reduce noise and enhance signal features. Data was split into training (70%) and test (30%) sets.
Model Implementation:

### Multilayer Perceptron (MLP):

Utilized scikit-learn's MLPClassifier with logistic loss and hyperbolic tan activation functions. MLP was chosen for its capability to handle nonlinear relationships in time-series data.

### Support Vector Machine (SVM):

Implemented using scikit-learn's SVC with a sigmoid kernel function. Kernel SVM was selected for its ability to construct high-dimensional features and separate data points non-linearly.

## Results
Both models performed perfectly on preprocessed data, achieving a test accuracy of 1.00 and perfect cross-validation scores. However, when evaluated on raw data, SVM outperformed MLP with a test accuracy of 0.4417 and validation accuracy of 0.59, compared to MLP's test accuracy of 0.3917 and validation accuracy of 0.54. Despite this, both models' raw data performance was below random guessing, indicating room for improvement.

## Conclusion
This project successfully demonstrated the potential of ML models in mechanical engineering diagnostics. While both models showed high accuracy on preprocessed data, SVM proved more effective on raw data, highlighting its robustness. Future work should include more comprehensive evaluations, such as training speed and memory usage, as well as hyperparameter tuning to enhance model performance.

## References
Kaggle Dataset: https://www.kaggle.com/brjapon/gearbox-fault-diagnosis?select=Healthy 
SpectraQuest Gearbox Fault Diagnostics Simulator: https://spectraquest.com/prognostics/details/gps/
scikit-learn Documentation: https://scikit-learn.org/stable/index.html




