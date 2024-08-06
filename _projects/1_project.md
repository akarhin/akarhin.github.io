---
layout: page
title: Gearbox fault diagnosis
description: Short IFD project done on a publicly available dataset.
img: assets/img/gearbox.jpg
importance: 1
category: fun
related_publications: false
---



## Introduction


While traditional condition monitoring (CM) done by vibration analysis is effective, it is not very scalable, requiring more well educated data analysts for accurate diagnosis. While the calulated features such as the RMS do alleviate this problem, reducing the vibration signature into specific features does not necessarily capture the entire distribution of faulty vibration behaviour. Therefore, the field of intelligent fault diagnosis (IFD) aims to automate CM with machine learning (ML) solutions. The aim is to produce intelligent models that take the vibration signature or a multitude of calculated features as their input and produce a health class as the output. The field has gained a lot of traction and many articles are published aiming to improve their use.

This project explores the application of Machine Learning (ML) for gearbox fault diagnosis. The goal was to develop intelligent models that can accurately determine whether a gearbox is healthy or faulty based on processed vibration data from accelerometers. The comparison focuses on two traditional ML models: the Support Vector Machine (SVM) and the Multilayer Perceptron (MLP). First, traditional CM methods are introduced for comparison. Second, the beforementioned ML models are introduced. Third, the results are shown and a superior ML model is chosen based on perceived performance. Finally, the project concludes by discussing further improvements applicable.


<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/gearbox.jpg" %}
  </div>
</div>

## Traditional condition monitoring

The monitoring of rotating machines is often conducted with vibration analysis due to its non-invasive nature compared to other monitoring methods such as lubricant analysis. Additionally, vibration analysis shows instant changes in the vibration signature when faults do occurs, facilitating fast reaction times and proper maintenacne actions. 

Traditional vibration analysis is conducted with techniques such as time-domain analysis, frequency analysis and envelope analysis.

Time-domain analysis can be conducted by directly comparing exctracted vibration signatures from a healthy and a faulty machine. Other forms of time-domain analysis include calculating features, such as the Root-mean square (RMS) value from the vibration signature and doing a similar comparison. By comparing their RMS values, one can determine which signal has greater overall energy or intensity, higher energy in similar operating conditions often signaling faulty behaviour. Features like this can be useful for the automation of CM systems, since raw time-domain analysis requires more finesse compared to the comparison of singular numerical features.

Frequency-domain analysis transforms the vibration signature into frequency domain with a transformation operation such as the Fourier transform. One of the main reasons for using a frequency-domain representations is to simplify the processed signal into its frequency components, reducing the noise present in the signature. For rotating machinery, specific faults present themself in specific fault frequencies further elaborated below. Frequency representation makes finding these specific frequencies easier compared to time-domain analysis. 

Some faults are strongly present in the harmonic frequencies, or integer multiples of specific fault frequencies. Envelope analysis aims to examine the high frequency components present in the vibration signature. One form of envelope analysis involves taking a Hilbert transformation of the raw measurement, extracting the envelope by taking the absolute value from the analytical signal, transforming the resulting signal into the order domain (1 order = 1 x Rpm in Hz) and then calculating the power spectral density (PSD) in the order domain. From the PSD, known fault frequencies related to the rotating speed of the system can be examined to determine if a fault mode corresponding to specific fault frequencies is present. 

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

**Hunting thooth frequency** The hunting teeth frequency (HTF) is the rate at which a tooth in one gear engages with a specific tooth in another gear. 

**Formula:**

$$
HTF = \frac{\text{GMF} \times N_a}{T_{out} \times T_{in}}
$$
where
-GMF is the gear meshing frequency
- N_a is the common frequency
-T_in = pinion teeth
-T_out = gear teeth

The common frequency is determined by dividing the amount of theeth from both gears in the gearpair into integer multiples. For example, 24 can be divided into 1* 24, 2*12, 3*8 and 4*6. The highest number present in both of the gears integer multiples is the common frequency. For example, 12 theeth gear and the previous gear have a common frequency of 12. This is a bad design choice, since specific theeth collide in a frequency of 12 * GMF. More importantly, if we have an even gear ratio, faults in specific theeth in the pinion affect specific theeth on the corresponding gear, accelerating the wear induced in these specific gear theeth locations.


The following section explains some common fault modes and their effect on the specific fault frequencies and the vibration signature in the frequency domain.

### Misalignment
- **Symptoms:** Amplitude increase in the axial direction of the axes. Appearance of 2X, 3X RPM, and 2X, 3X GMF.
- **Causes:** Wrong alignment procedures, loss of tolerances, thermal expansion.


### Excessive Wear
- **Symptoms:** Increased amplitude of the 1XGMF and 1X sidebands. Appearance of gear's natural frequency.
- **Causes:** Improper lubrication, contaminated or degraded lubricant. Change of wear pattern. Assembly and adjustment failures.


### Excessive Backlash
- **Symptoms:** Increased amplitude of the 1XGMF and 1X sidebands. Appearance of gear's natural frequency.
- **Causes:** Bad assembly, design or manufacturing flaws, wear.

### Overload
- **Symptoms:** Increased amplitude of 1XGMF, multiple 1X RPM sidebands.
- **Causes:** Operation outside of design conditions.

### High Friction
- **Symptoms:** Increase of the 1XGMF component, rise of the global amplitude in acceleration, and shock pulse.
- **Causes:** Lubrication failures and/or lubricant quality. Component assembly and tolerances.

### Broken Teeth
- **Symptoms:** Synchronous impact pattern in the time waveform with 1X of damaged gear.
- **Causes:** Overload, fatigue, adjustments and tolerances.

### Assembly or Manufacturing Failures
- **Symptoms:** Increased amplitude of the 1XGMF and 1X sidebands. Appearance of Hunting Tooth Frequency (HFT) or the Gear Assembly Phase Frequency (GAPF).
- **Causes:** Manufacturing defects in geometry and/or materials. Irregular teeth surface. Changes from the original wear pattern.

## The Nyquist frequency

During the data gathering process, something called the Nyquist frequency is often discussed. The nyquist frequency corresponds to the frequency thats cycle length is half of the samplers frequency. Therefore, for example, a sampling rate of 3 kHz has a Nyquist frequency of 1.5 kHz. Conversely, a frequency of 1.5 kHz has a Nyquist rate of 3 kHz. The Nyquist rate is used to mimimize the effect of aliasing during data acquisition. It is stated that to avoid aliasing, the Nyquist rate of the phenomena monitored has to be smaller or at least equal to the sampling rate. That is, if we want to monitor high frequency phenomena, the sampling frequency has to be at least double the monitored phenomenas frequency to avoid aliasing in the signal. 

## Methodology

### Dataset Description:

Sourced from Kaggle, the dataset includes vibration data from four accelerometers placed on gearboxes under different loads. It contains 20 files: 10 for healthy gearboxes and 10 for gearboxes with a broken tooth, each under different load conditions (0% - 90%). The four vibration sensors placed in four different direction, and under variation of load from '0' to '90' percent.

Data points were segmented into windows and labeled. Fast Fourier Transform (FFT) was applied to reduce noise and enhance signal features. Data was split into training (70%) and test (30%) sets. The dataset is publicly available (you need a Kaggle account) [here]( https://www.kaggle.com/datasets/brjapon/gearbox-fault-diagnosis). The SpectraQuest Gearbox Prognostic Simulator test setup has been introduced [here](https://spectraquest.com/prognostics/details/gps/).

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/spectraquest_2.jpg" %}
  </div>
</div>

## ML models
A short introduction to the utilized ML models and how they were implemented.

### MLP:
A Multilayer Perceptron (MLP) is a type of artificial neural network used primarily for supervised learning tasks like classification and regression. The structure of an MLP consists of an input layer, one or more hidden layers, and an output layer. Each layer is composed of neurons, where each neuron in one layer is connected to every neuron in the next layer, forming a fully connected network.

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    <iframe src="assets/img/mlp.pdf" width="100%" height="500px"></iframe>
    <figcaption style="text-align: center; margin-top: 10px;">A simple MLP structure.</figcaption>
  </div>
</div>

In an MLP, the input layer receives the raw data, which is then processed through the hidden layers. These hidden layers are responsible for learning and extracting features from the data through weighted connections and activation functions, which introduce non-linearity into the model, enabling it to learn complex patterns.

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    <iframe src="assets/img/Neuron.pdf" width="100%" height="500px"></iframe>
    <figcaption style="text-align: center; margin-top: 10px;">A simple MLP structure.</figcaption>
  </div>
</div>

The output layer produces the final prediction, which can be a single value in the case of regression tasks or a probability distribution over different classes for classification tasks. The learning process involves adjusting the weights of the connections through a method called backpropagation, which uses the gradient of a loss function to minimize the error between the predicted and actual outputs.

This project utilized scikit-learn's MLPClassifier with logistic loss and hyperbolic tan activation functions. MLP was chosen for its capability to handle nonlinear relationships in time-series data. The utilized activation function was the Tanh.

$$\text{Tanh}(x) = \frac{e^x - e^{-x}}{e^x + e^{-x}}$$

Naturally, the hypothesis space for an MLP is:

$$h : \mathbb{R} \rightarrow \mathbb{R}$$.

The chosen loss function was the logistic loss:

$$
\text{Logistic Loss}(y, \hat{y}) = - \left[ y \log(\hat{y}) + (1 - y) \log(1 - \hat{y}) \right]
$$

### SVM:
A Support Vector Machine (SVM) is a supervised learning algorithm used primarily for classification and regression tasks. The main goal of an SVM is to find the optimal hyperplane that best separates the data points of different classes in a high-dimensional space.

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/linear_svm.jpg" %}
  </div>
</div>

In the case of classification, an SVM constructs a hyperplane or set of hyperplanes in a high-dimensional space. These hyperplanes are chosen to maximize the margin between different classes, which is the distance between the hyperplane and the nearest data points from any class, known as support vectors. By maximizing this margin, the SVM aims to improve the model's ability to generalize to unseen data.

For linearly separable data, a linear hyperplane is sufficient. However, for non-linearly separable data, SVMs use a technique called the kernel trick. The kernel trick involves transforming the original data into a higher-dimensional space where a linear separator can be found. Common kernels include the polynomial kernel, radial basis function (RBF) kernel, and sigmoid kernel.

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/nonlinear_svm.jpg" %}
  </div>
</div>

This project implemented the SVM using scikit-learn's SVC with a sigmoid kernel function. Kernel SVM was selected for its ability to construct high-dimensional features and separate data points non-linearly. Sigmoid can be represented as:

$$ S(x) = \frac{e^x}{e^x + 1} $$

The used loss function for the SVM was the Hinge loss:


$$
\text{Loss}((x, y), h) := \max\left(0, 1 - y \cdot h(x)\right) + \lambda \|w\|
$$



## Results
Both models performed perfectly on preprocessed data, achieving a test accuracy of 1.00 and perfect cross-validation scores. However, when evaluated on raw data, SVM outperformed MLP with a test accuracy of 0.4417 and validation accuracy of 0.59, compared to MLP's test accuracy of 0.3917 and validation accuracy of 0.54. Despite this, both models' raw data performance was below random guessing, highlighting the importance of data preprocessing when implementing traditional ML models for IFD. 

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/Confusion_matrix_mlp.jpg" %}
  </div>
</div>

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/confusion_matrix_svm.jpg" %}
  </div>
</div>


## Conclusion
This project successfully demonstrated the potential of ML models in mechanical engineering diagnostics. It functions as a good starting point for any mechanical engineering student who is interested in 

The project code is available to download as a .pdf file: [PDF file](../assets/pdf/gearbox_fault_diagnosis.pdf).


## Things to improve



