---
layout: page
title: Virtual sensor for powertrains
description: Summary of a journal publication
img: assets/img/Virtual_sensor.jpg
importance: 2
category: work
---


## Introduction

Virtual sensors, also known as soft sensors, appear as a promising branch of solutions well suited for machine monitoring. Virtual sensors are computational models that estimate physical quantities from other available information about the system, for example secondary measurements or known physical quantities. A virtual sensor can be, for example, used as a backup sensor for sensor prone to breaking due to environmental factors. Virtual sensors have attracted much attention across multiple research fields, including process monitoring and process fault diagnosis. Additionally, virtual sensors have recently gained some attention in mechanical application fields, for example in machine condition monitoring. Virtual sensors are often classified either as model-based virtual sensors, or as data-driven virtual sensors. Model-based virtual sensors apply given system dynamics and domain knowledge, for example in the form of a physics model that simulates the system dynamics, to determine the wanted output quantity. Data-driven virtual sensors on the other hand apply machine learning (ML) techniques to learn patterns directly from historical data without any domain knowledge, but while requiring measured data for training. Commonly used machine learning (ML) models for these sensors include multilayer perceptrons (MLP) and support vector machines (SVM). However, a major drawback of traditional ML-based virtual sensors is the necessity for complex feature extraction and manual feature selection from the training data. Deep learning has been outperforming traditional ML methods in various applications, such as natural language processing and image classification, and has become increasingly popular in mechanical applications like rotating machinery diagnosis. As a result, many current data-driven virtual sensors now rely on more effective deep learning architectures. Despite the growing interest in data-driven virtual sensors and their proposed applications in fields such as rotating machinery, there are still relatively few implementations specifically for powertrains. Additionally, slight variations between different instances of the same powertrain design create a need for a generalized virtual sensor that can account for these differences and operate within the required accuracy range without additional training. Transfer learning offers potential techniques for achieving this generalization by applying learned patterns from one domain to another. Depending on the application, these domains can vary significantly or be nearly identical. For example, transfer learning techniques can enable a deep reinforcement learning-based autonomous robot to be trained entirely with simulated data and then function effectively in a real-world environment.

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/Virtual_Sensor.jpg" %}
  </div>
</div>




\begin{align}
    f_{t} &= \sigma(W_f \cdot [h_{t-1},x_t]+b_f)             \\
    i_{t} &= \sigma(W_i \cdot [h_{t-1},x_t]+b_i)               \\ 
    o_{t} &= \sigma(W_o \cdot [h_{t-1},x_t]+b_o)             \\
    \tilde{c}_{t} &= tanh(W_c \cdot [h_{t-1},x_t]+b_c)       \\
    c_{t} &= f_{t} \odot c_{t-1}+i_{t} \odot \tilde{c}_{t} \\
    h_{t} &= o_{t} \odot tanh(c_{t})
\end{align}

