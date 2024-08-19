---
layout: page
title: Virtual sensor for powertrains
description: Summary of a journal publication
img: assets/img/Virtual_sensor.jpg
importance: 2
category: work
---


## Introduction

In order to conduct proper diagnosis of rotating machines, proper instrumentation is required. For vibration analysis, which is the most used form of condition monitoring for rotating machinery, this can include multiple accelerometers and/or torque transducers. With proper instrumentation, reliable and accurate diagnosis can be conducted. Machine dimensioning, the operating environment or the cost of the sensors can limit the available instrumentation. These factors are twofold when considering critical quantities, where backup sensors are placed in case of a sensor failure.

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/Virtual_sensor.jpg" %}
  </div>
</div>


Virtual sensors, also known as soft sensors, appear as a promising branch of solutions well suited for machine monitoring. Virtual sensors are computational models that estimate physical quantities from other available information about the system, for example secondary measurements or known physical quantities. A virtual sensor can be, for example, used as a backup sensor for sensor prone to breaking due to environmental factors. Virtual sensors have attracted much attention across multiple research fields, including process monitoring and process fault diagnosis. Additionally, virtual sensors have recently gained some attention in mechanical application fields, for example in machine condition monitoring. Virtual sensors are often classified either as model-based virtual sensors, or as data-driven virtual sensors. Model-based virtual sensors apply given system dynamics and domain knowledge, for example in the form of a physics model that simulates the system dynamics, to determine the wanted output quantity. Data-driven virtual sensors on the other hand apply machine learning (ML) techniques to learn patterns directly from historical data without any domain knowledge, but while requiring measured data for training. Commonly used machine learning (ML) models for these sensors include multilayer perceptrons (MLP) and support vector machines (SVM). However, a major drawback of traditional ML-based virtual sensors is the necessity for complex feature extraction and manual feature selection from the training data. Deep learning has been outperforming traditional ML methods in various applications, such as natural language processing and image classification, and has become increasingly popular in mechanical applications like rotating machinery diagnosis. As a result, many current data-driven virtual sensors now rely on more effective deep learning architectures.

This project summarizes the implementation done to the publication: Data-driven virtual sensor for powertrains based on transfer learning, available [here](https://research.aalto.fi/en/publications/data-driven-virtual-sensor-for-powertrains-based-on-transfer-lear). The implementation includes the description of the dataset, the model architecture and the results of the implementation. 

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/VS.jpg" %}
  </div>
</div>

## Data

The data used to train the presented virtual sensor was created with a lumped-mass model of a miniatyre sized azimuth thruster. The following image and table describe the utilized model.

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/lumped_page-0001.jpg" %}
  </div>
</div>

| **Component**                                 | **Index** | **\(I_i\) (kgm\(^2\))** | **\(c_i\) (Nm/(rad/s))** | **\(k_i\) (Nm/rad)**   | **\(d_i\) (Nm/(rad/s))** |
|-----------------------------------------------|-----------|-------------------------|--------------------------|------------------------|-------------------------|
| Driving motor, coupling                       | 1         | \(7.94 \times 10^{-4}\) | 8.08                     | \(1.90 \times 10^{5}\) | 0.0030                  |
| Shaft                                         | 2         | \(3.79 \times 10^{-6}\) | 0.29                     | \(6.95 \times 10^{3}\) | 0                       |
| Elastomer coupling hub                        | 3         | \(3.00 \times 10^{-6}\) | 0.24                     | 90.0                   | 0                       |
| Elastomer coupling middle piece               | 4         | \(2.00 \times 10^{-6}\) | 0.24                     | 90.0                   | 0                       |
| Elastomer coupling hubs & shaft               | 5         | \(7.81 \times 10^{-3}\) | 0.24                     | 90.0                   | 0                       |
| Elastomer coupling middle piece               | 6         | \(2.00 \times 10^{-6}\) | 0.24                     | 90.0                   | 0                       |
| Elastomer, coupling hub, encoder & shaft      | 7         | \(3.17 \times 10^{-6}\) | 0.00                     | 30.13                  | 0                       |
| Shaft, encoder & coupling                     | 8         | \(5.01 \times 10^{-5}\) | 1.78                     | \(4.19 \times 10^{4}\) | 0                       |
| Torque transducer                             | 9         | \(6.50 \times 10^{-6}\) | 0.23                     | \(5.40 \times 10^{3}\) | 0                       |
| Torque transducer & coupling                  | 10        | \(5.65 \times 10^{-5}\) | 1.78                     | \(4.19 \times 10^{4}\) | 0                       |
| Shaft                                         | 11        | \(4.27 \times 10^{-6}\) | 0.52                     | \(1.22 \times 10^{3}\) | 0                       |
| Shaft & gear                                  | 12        | \(3.25 \times 10^{-4}\) | 1.84                     | \(4.33 \times 10^{4}\) | 0.0031                  |
| Coupling                                      | 13        | \(1.20 \times 10^{-4}\) | 1.32                     | \(3.10 \times 10^{4}\) | 0                       |
| Shaft                                         | 14        | \(1.15 \times 10^{-5}\) | 0.05                     | \(1.14 \times 10^{3}\) | 0                       |
| Shaft & coupling                              | 15        | \(1.32 \times 10^{-4}\) | 1.32                     | \(3.10 \times 10^{4}\) | 0                       |
| Shaft                                         | 16        | \(4.27 \times 10^{-6}\) | 0.52                     | \(1.22 \times 10^{4}\) | 0                       |
| Shaft & gear                                  | 17        | \(2.69 \times 10^{-4}\) | 1.88                     | \(4.43 \times 10^{4}\) | 0.0031                  |
| Coupling                                      | 18        | \(1.80 \times 10^{-4}\) | 5.86                     | \(1.38 \times 10^{5}\) | 0                       |
| Torque transducer                             | 19        | \(2.00 \times 10^{-5}\) | 0.85                     | \(2.00 \times 10^{4}\) | 0                       |
| Torque transducer & coupling                  | 20        | \(2.00 \times 10^{-4}\) | 5.86                     | \(1.38 \times 10^{5}\) | 0                       |
| Shaft                                         | 21        | \(4.27 \times 10^{-6}\) | 0.52                     | \(1.22 \times 10^{4}\) | 0                       |
| Shaft, mass & loading motor                   | 22        | \(4.95 \times 10^{-2}\) | -                        | -                      | 0.2400                  |

*Table 1: Nominal powertrain parameters used in the simulated powertrain instances. Parameters belonging to the mass moment of inertia (\(I_i\)), damping (\(c_i\)) and stiffness (\(k_i\)) for each powertrain instance were drawn from a uniform distribution between 0.5 and 1.5 times each nominal value separately.*

### Lumped-mass modelling



### The LSTM
The long-short term memory (LSTM) is a recurrent neural network architecture known to work well with temporal patterns present in time-series data, such as vibration measurements. The LSTM operates by a sophisticated gating mechanism modifying information flow to hidden and cell states, essentially functioning as a temporary memory when producing the output to the next layer of the network. This gating mechanism is updated by the following equations:
f_t = σ(W_f · [h_(t-1), x_t] + b_f)

i_t = σ(W_i · [h_(t-1), x_t] + b_i)

o_t = σ(W_o · [h_(t-1), x_t] + b_o)

\tilde{c}_t = tanh(W_c · [h_(t-1), x_t] + b_c)

c_t = f_t ⊙ c_(t-1) + i_t ⊙ \tilde{c}_t

h_t = o_t ⊙ tanh(c_t)

where the variables correspond to the following quantities
- \( f_t \): Forget gate activation vector
- \( \sigma \): Sigmoid activation function
- \( W_f \): Weight matrix for the forget gate
- \( h_{(t-1)} \): Previous hidden state
- \( x_t \): Current input
- \( b_f \): Bias vector for the forget gate
- \( i_t \): Input gate activation vector
- \( W_i \): Weight matrix for the input gate
- \( b_i \): Bias vector for the input gate
- \( o_t \): Output gate activation vector
- \( W_o \): Weight matrix for the output gate
- \( b_o \): Bias vector for the output gate
- \( \tilde{c}_t \): Candidate cell state
- \( \text{tanh} \): Hyperbolic tangent activation function
- \( W_c \): Weight matrix for the candidate cell state
- \( b_c \): Bias vector for the candidate cell state
- \( c_t \): Cell state
- \( \odot \): Hadamard product (element-wise multiplication)
- \( h_t \): Hidden state

The following image visualizes the flow of this computation throughout a singular time-step.

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/cell_page-0001.jpg" %}
  </div>
</div>

| **Parameter**             | **Value**       |
|---------------------------|-----------------|
| Window length             | 5000            |
| Training stride           | 250             |
| Test stride               | 5000            |
| Model input dimension     | 5000 × 3        |
| Model output dimension    | 5000 × 4        |
| Batch size                | 2               |
| Cell size                 | 81              |
| Number of layers          | 4               |
| Dropout                   | 0               |
| Learning rate             | 0.0001          |
| Epochs                    | 15              |

*Table 2: Model and training parameters used in training and testing. Window length corresponds to the time sample size, stride corresponds to the amount of samples between the start of a data point and the start of the next data point, dimensions correspond to the used array dimensions as input and output of the virtual sensor, batch size to the amount of data points given to the model at a time, layers to the amount of LSTM layers in the model, learning rate to a parameter used in the back propagation algorithm and epochs to the amount of iterations of training through the training set.*

A virtual sensor architecture was employed, consisting of four LSTM layers followed by a fully-connected layer. The suggested virtual sensor takes generated data points as input. Model parameters are listed in Table 2. The training procedure for the data-driven virtual sensor was conducted using traditional supervised learning scenario. During training, rotating speeds and torque near the propeller end of the powertrain were estimated from rotating speeds and torque near the motor end of the powertrain. An error term was established using a loss function. The loss was calculated using mean squared error (MSE):

The Mean Squared Error (MSE) is calculated as:

\[ \text{MSE} = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2 \]

where:
- \( n \) is the number of data points,
- \( y_i \) is the actual value,
- \( \hat{y}_i \) is the predicted value.

The loss terms shown in the Results section have been expressed in MSE. The loss was applied via Stochastic Gradient Descent (SGD) to improve the weights of the model after every training epoch. More precisely, the model was optimized using Adam, a widely used optimizer for neural networks trained with SGD. Adam has been introduced further in *Collaborative Lane Detection with Federated Learning* and in [here](https://www.geeksforgeeks.org/adam-optimizer/).






