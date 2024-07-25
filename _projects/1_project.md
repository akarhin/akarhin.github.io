---
layout: page
title: Gearbox fault diagnosis
description: Short IFD project done on a publicly available dataset.
img: assets/img/gearbox.jpg
importance: 1
category: work
related_publications: false
---

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/gearbox.jpg" %}
  </div>
</div>

## Introduction

This project explores the application of Machine Learning (ML) for gearbox fault diagnosis. The goal was to develop intelligent models that can accurately determine whether a gearbox is healthy or faulty based on vibration data from accelerometers. The comparison focuses on two traditional ML models: the Support Vector Machine (SVM) and the Multilayer Perceptron (MLP). The primary focus was to conduct a quick experiment on a public dataset in the field of fault diagnosis.

In many industrial processes, halting machinery for inspection can lead to significant losses. Thus, a reliable ML model capable of diagnosing gearbox faults using vibration data prevents unnecessary downtimes. The dataset comprises accelerometer readings from gearboxes under various loads, labeled as 'Healthy' or 'Broken'.

## Traditional condition monitoring

The monitoring of rotating machines is often conducted with vibration analysis due to its non-invasive nature compared to other monitoring methods such as lubricant analysis. Additionally, vibration analysis shows instant changes in the vibration signature when faults do occurs, facilitating fast reaction times and proper maintenacne actions. 

Traditional vibration analysis is conducted with techniques such as envelope analysis. One form of envelope analysis involves taking a Hilbert transformation of the raw measurement, extracting the envelope by taking the absolute value from the analytical signal, transforming the resulting signal into the order domain (1 order = 1 x Rpm in Hz) and then calculating the power spectral density (PSD) in the order domain. From the PSD, known fault frequencies related to the rotating speed of the system can be examined to determine if a fault mode corresponding to specific fault frequencies is present. Discovering these fault frequencies forms the basis of vibration analysis techniques. Therefore, introducing common gearfault frequencies is necessary.

The main characteristic fault frequencies in gears include the Gear mesh frequency (GMF), sidebands, and harmonics.

**GMF** is the frequency at which gear teeth mesh together. It is a fundamental frequency in the vibration signal of a gearbox and is used to detect gear faults. It is calculated with the following equation:

$$
 \text{GMF} = N \times f_s 
$$

where:
- \( N \) is the number of teeth on the gear
- \( f_s \) is the shaft rotational frequency (in Hz)

**Sidebands** are frequencies that appear around the gear mesh frequency and its harmonics. They are indicative of modulation effects due to gear faults such as wear, misalignment, or eccentricity.

**Formula:**
$$
\text{Sidebands} = \text{GMF} \pm k \times f_s
$$

where:
- \( k \) is an integer (1, 2, 3, ...)
- \( f_s \) is the shaft rotational frequency (in Hz)


**Harmonics** of the GMF are integer multiples of the GMF. The presence of harmonics and their relative amplitudes can provide information about the severity and type of gear faults.

**Formula:**
$$
\text{Harmonics} = m \times \text{GMF} 
$$

where:
- \( m \) is an integer (1, 2, 3, ...)

### Summary Table

| Fault Frequency | Formula                                         | Description                                  |
|-----------------|-------------------------------------------------|----------------------------------------------|
| GMF             | $$ N \times f_s $$                              | Frequency of gear teeth meshing              |
| Sidebands       | $$ \text{GMF} \pm k \times f_s $$               | Frequencies around GMF due to modulation effects |
| Harmonics       | $$ m \times \text{GMF} $$                       | Integer multiples of the GMF                 |


While traditional CM is effective, it is not very scalable, requiring more well educated data analysts for accurate diagnostics. Therefore, the field of intelligent fault diagnosis (IFD) aims to automate CM with ML and DL solutions. The field has gained a lot of traction and many articles are published aiming to improve their use.

## Methodology

### Dataset Description:

Sourced from Kaggle, the dataset includes vibration data from four accelerometers placed on gearboxes under different loads. It contains 20 files: 10 for healthy gearboxes and 10 for gearboxes with a broken tooth, each under different load conditions (0% - 90%).

Data points were segmented into windows and labeled. Fast Fourier Transform (FFT) was applied to reduce noise and enhance signal features. Data was split into training (70%) and test (30%) sets.

## Model implementations

### MLP:

Utilized scikit-learn's MLPClassifier with logistic loss and hyperbolic tan activation functions. MLP was chosen for its capability to handle nonlinear relationships in time-series data. The utilized activation function was the Tanh.

$$\text{Tanh}(x) = \frac{e^x - e^{-x}}{e^x + e^{-x}}$$

Naturally, the hypothesis space for an MLP is:

$$h : \mathbb{R} \rightarrow \mathbb{R}$$.

The chosen loss function was the logistic loss:

$$
\text{Logistic Loss}(y, \hat{y}) = - \left[ y \log(\hat{y}) + (1 - y) \log(1 - \hat{y}) \right]
$$

### SVM:

Implemented using scikit-learn's SVC with a sigmoid kernel function. Kernel SVM was selected for its ability to construct high-dimensional features and separate data points non-linearly.

## Results
Both models performed perfectly on preprocessed data, achieving a test accuracy of 1.00 and perfect cross-validation scores. However, when evaluated on raw data, SVM outperformed MLP with a test accuracy of 0.4417 and validation accuracy of 0.59, compared to MLP's test accuracy of 0.3917 and validation accuracy of 0.54. Despite this, both models' raw data performance was below random guessing, indicating room for improvement.

## Conclusion
This project successfully demonstrated the potential of ML models in mechanical engineering diagnostics. While both models showed high accuracy on preprocessed data, SVM proved more effective on raw data, highlighting its robustness. Future work should include more comprehensive evaluations, such as training speed and memory usage, as well as hyperparameter tuning to enhance model performance.

## References
Kaggle Dataset: https://www.kaggle.com/brjapon/gearbox-fault-diagnosis?select=Healthy 
SpectraQuest Gearbox Fault Diagnostics Simulator: https://spectraquest.com/prognostics/details/gps/
scikit-learn Documentation: https://scikit-learn.org/stable/index.html




