---
layout: page
title: fault injection with GANs
description: Thesis summary
img: assets/img/gan_image.jpg
importance: 1
category: work
---

## Introduction

Automation of condition monitoring (CM) systems has been gaining wide research interest. Specifically, data-driven intelligent fault diagnosis (IFD) solutions have gained popularity in the field. However, solutions based on machine learning (ML) and recently deep learning (DL) suffer from three significant problems which limit their use in industry:

- Data scarcity: IFD models require large quantities of examples in the form of vibration data from different operating conditions, machines and fault modes in order to function in the proper accuracy range.
- Generalization: IFD models struggle to generalize outside the given training set. This leads to the training of a multitude of models for fleets of machines, or required constant retraining of prior models, which can lead to catastrophic forgetting of prior knowledge.
- Explainability: ML and DL solutions are often perceived as black boxes. This leads to decreased trust, or worse, unwarranted trust building towards these types of solutions.

This works aims to answer one of these problems, Data scarcity, by leveraging a limited amount of fault samples in order to train a GAN generator to learn to "inject" fault modes into healthy vibration samples. This work has been completed as a Master's thesis, available at Aaltodoc or with personal request. The following is a discussion on the results and its significance scientifically.

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/gan_image.jpg" %}
  </div>
</div>

## Data description

The data for this study originated from a compact maritime thruster testing platform. The primary feature of this test bench was to ensure that its fundamental frequencies closely matched those of the full-scale thruster. In order to create artificial faults into the test bench measurement data, thin metal sheets (shims) were glued into the pinion gear of the thrusters gearbox. It is to note that this fault is highly artificial and does not imitate any reasonable fault possible in a bevel gear: it is purely to create separate vibration profiles for multiclass fault diagnosis.
Below image showcases the test bench and all the properties that created the dataset. The utilized measurement was torsional vibration measured by a strain gage-based torque transducer. 
<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/thesis_data.jpg" %}
  </div>
</div>

## GAN and IFD architectures


## General setting

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/General_setting.jpg" %}
  </div>
</div>

## Results

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/Qualitative_res.jpg" %}
  </div>
</div>
<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/Quantitative_res.jpg" %}
  </div>
</div>

## Discussion

The thesis explores the use of Generative Adversarial Networks (GANs) for fault diagnosis in rotating machines, specifically focusing on the generation of synthetic fault data to supplement limited measured data. This approach addresses a significant challenge in the domain of machine fault diagnosis: the scarcity of labeled fault data required for training deep learning models effectively. The discussion section of the thesis evaluates the scientific and practical impacts, highlights the uncertainties, and suggests directions for further research.

### Scientific Impact

The thesis presents several novel contributions to the field of GAN-based fault diagnosis for rotating machines:

1. **Novel GAN Implementation**: Unlike previous research, which often employs multimodular GAN implementations (a separate GAN for each fault class), this thesis uses a single modular GAN to generate multiple fault states. This approach simplifies the model architecture and potentially reduces computational overhead.

2. **Varied Operating Conditions**: The GAN model was trained and tested under various operating speeds, ranging from 250 RPM to 1500 RPM. This variation in operating conditions is relatively novel and crucial for developing robust fault diagnosis systems that can perform accurately under different conditions.

3. **Time-Domain Data Generation**: The thesis demonstrates positive results for generating fault data in the time-domain. This is significant because most existing GAN implementations for rotating machine fault diagnosis operate in the frequency or time-frequency domain to minimize noise and preserve signal information.

4. **Low Training Data**: The research shows that GANs can effectively generate synthetic fault data even with limited available training data. This is particularly valuable for industrial applications where obtaining extensive fault data is challenging and costly.

### Practical Impact

The practical implications of this thesis are the following:

1. **Enhanced Data Availability**: By generating synthetic fault samples, GANs can supplement real measured data, balancing datasets and improving the training of deep learning models for fault diagnosis. This is especially beneficial for faults that are difficult to measure or rare in occurrence.

2. **Improved Model Generalization**: The inclusion of synthetic data exposes fault diagnosis models to a broader range of fault distributions during training. This exposure helps in improving the generalization capability of the models, leading to more accurate and reliable fault detection in real-world applications.

3. **Reduced Overfitting**: The combined use of measured and synthetic data reduces the risk of overfitting, a common issue when training models with limited data. This results in more robust models that perform better on unseen data.

### Uncertainty Analysis

The thesis acknowledges several sources of uncertainty:

1. **Stochastic Nature of Training**: The performance of neural networks, including GANs, can vary due to their stochastic training nature. Different runs can converge to different local minima, leading to variability in model performance.

2. **Experimental Setup**: Uncertainties in the test rig, such as gear clearances and heating effects, could affect the results. The absence of documentation on these factors in the utilized dataset adds to the uncertainty.

3. **Public Code Packages**: Reliance on publicly available code packages introduces potential inaccuracies and variabilities in the results.

### Further Research

The thesis suggests several avenues for further research:

1. **Enhanced GAN Techniques**: Future work could explore new GAN architectures and training techniques to improve the accuracy of synthetic fault data generation.

2. **2D Architectures**: Instead of using 1D architectures, transforming time-series data into the time-frequency domain and using 2D GAN architectures could leverage the strengths of GANs in image synthesis.

3. **Simulation-to-Reality Applications**: Investigating the use of GANs for transforming simulation-generated samples into realistic measurements could enhance the practical integration of fault diagnosis systems.

4. **Transfer Learning**: Exploring GAN-based transfer learning theories could further promote practical research and real-life integration of intelligent fault diagnosis systems in rotating machines.

## Conclusion

The discussion section of the thesis highlights the significant scientific and practical contributions of using GANs for fault diagnosis in rotating machines. Despite some uncertainties, the research presents a promising approach to addressing the data scarcity issue in fault diagnosis, paving the way for more robust and reliable industrial applications. Further research in enhancing GAN techniques, exploring new architectures, and investigating practical applications is essential for advancing this field.
