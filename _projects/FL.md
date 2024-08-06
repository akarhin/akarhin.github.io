---
layout: page
title: Collaborative Lane Detection with Federated Learning
description: A data private approach to lane detection models utilizing federated learning.
img: assets/img/FL.jpg
importance: 2
category: work
---

## Introduction

In recent years, advancements in robotics and computer vision have led to significant progress in autonomous driving technologies. Lane detection, as a critical component of such systems, plays a crucial role for intelligent vehicles in perceiving and understanding the surrounding environment. Accurate and robust lane detection is essential for tasks such as vehicle navigation, lane keeping, and advanced driver-assistance systems (ADAS). However, traditional lane detection methods often rely on centralized data collection and processing. That is, that the party training the model needs to have access to the data in order to apply it for learning or testing. This can lead to data privacy concerns that may limit the collaboration of parties in the competing markets or exclude parties overall concerned about data leaks from participating in the development of these types of models.

Federated learning (FL) rises as a promising branch of solutions suitable for collaborative machine learning (ML) models. FL algorithms enable collaborative model training across distributed devices, or robots, without the need for data sharing. The fundamental principle behind FL lies in training the models locally while preserving the privacy of the collected data. By training models locally, sensitive data remains on the devices, minimizing the risk of data breaches or privacy violations. Only model updates or gradients are exchanged between the devices or even be seen by the global model, allowing for collaborative training of the global model without exposing the raw data to unwanted eyes.

This project focused on applying FL approaches for collaborative lane detection. The primary goal was to portray a promising solution to safeguard data privacy. This study explores and evaluates different FL algorithms suitable for collaborative lane detection on TurtleBots, which are differential drive three wheel robots based on the Robot Operating System (ROS).

First, the data acquisition framework is introduced. Second, the FL algorithms and the training scenario is introduced. Third, the results are discussed. Finally, the project concludes by discussing further improvements.

## Data gathering and processing

The datasets used in this project were collected on a TurtleBot which had a Raspberry Pi camera module 2 attached. The TurtleBot was driven around the three different tracks remotely via an SSH (Secure Shell) connection from a remote Ubuntu laptop. While driving, a rosbag was created on the remote laptop, which recorded all the published messages in the ROS environment. After the recording, the images published by the camera node were exported and fed to an OpenCV algorithm based on Canny edge detection. Each datapoint consisted of the original image resampled to the size (3x96x128) (3 corresponding to the RGB values of each image) as the feature and the same image with same size, but with highlighted lanes as the label. 

Data was taken during operation of the TurtleBot (while moving) for added realism. Due to time and project constraints, all data was gathered with the same TurtleBot, just in separate tracks, still ensuring that the local models had no access to each other's data.

## Problem formulation and the chosen FL algorithms

### GTVMin

GTVMin, or generalized total variation minimization, is a technique used in various fields such as image processing, machine learning, and signal processing. It aims to find an optimal set of parameters or weights that minimize a given objective function. The research topic of the project can be formulated as a GTVMin problem. By constructing an empirical graph based on the research problem, FL algorithms can be used to solve this special case of GTVMin by applying different iterative optimisation methods. The empirical graph is constructed with a collaborative framework in mind: each edge has the same weight. In some more detailed collaborations, e.g. highly different environment lane detection datasets, the weights could be defined differently. However, the scope of this project is limited to equal weight collaborative lane detection. Each edge corresponds to the information flow, or the flow of weights and gradients, from each local node to the global node. Likewise, the global node shares the current global model along the same edges to the local nodes. Each local node has a dataset containing data from a different environment for the task of lane detection.

$$
\widehat{\mathbf{w}} \in \underset{\mathbf{w} \in \mathcal{W}}{\arg \min} \sum_{i \in \mathcal{V}} L_{i}(\mathbf{w}^{(i)}) + \lambda \sum_{{i, i'} \in \mathcal{E}} A_{i, i'} |\mathbf{w}^{(i)} - \mathbf{w}^{(i')}|_{2}^{2}
$$

By formulating the research topic as a GTVMin problem, the aim is to produce a general model that can be taught with all local datasets while preserving privacy and improving the overall performance of the lane detection system.

Each local dataset was gathered by previously explained methods from different environments and had 150 datapoints per local dataset. The data was split into training sets (100 datapoints for each local dataset distributed into the corresponding local nodes), the validation dataset (the combinations of 25 datapoints from each local dataset = 75 datapoints used for validation scores in the global node) and the testing dataset (the combinations of 25 datapoints from each local dataset = 75 datapoints used for testing). The validation data is shared into the global node only to see how well the models generalise between local dataset, thus not being necessary for actual collaborative lane detection (or open source data could be used instead here). The data split was conducted with random.Random.shuffle(): shuffling a list of datapoints and taking first 100 to the training set, next 25 to the validation set and final 25 into the test set. 

The feature selection was self-explanatory, an image of a road segment where the lanes need to be highlighted. The dataset was notably downsampled for faster computations and ease of result repeatability. Because the model uses convolutional layers, the more detailed features from the images used are hard to pinpoint. The model used for the global and local models was a Convolutional Neural Network (CNN), which is a traditional neural network architecture used in lane detection algorithms. An identical neural network architecture between local nodes and the global model was used. The models of each node were identical in architecture, since the lane detection models take in and output a same sized image. Since the edge weights were also the same, the only difference between the local nodes were the datasets they could apply during training of the current global model. Each local model and the global model used Mean-Squared Error (MSE) as the loss function:

$$

\operatorname{MSE} = {\frac {1}{n}}\sum _{i=1}^{n}(Y_{i}-{\hat {Y_{i}}})^{2}

$$

where:
- \( n \) is the number of observations.
- \( Y_{i} \) is the actual value.
- \( \hat{Y_{i}} \) is the predicted value.



MSE is a traditional loss function that can be used to compare images when they are in array format. The FedAvg local models were optimised using Adam optimiser, which is an advanced version of traditional SGD optimizer. The FedSGD global model was optimised with traditional SGD: aggregating the gradients and modifying the weights by the product of the gradients and the learning rate. 


## Results


After 50 epochs, the average test set MSE for the FedAvg global node was found to be 816.65. It is important to note that this value represents the overall error across the entire empirical graph, since the test set is a combination of data from all local datasets. That is, local nodes did not train own models, but collaborated to train a general global model. For the FedSGD, the MSE was found to be around 1051.63. Similar to the FedAvg results, this value represents the overall error across the empirical graph. Comparing the test set errors of the two methods, we observe the following: FedAvg achieved a lower average test set error, while FedSGD resulted in a slightly higher average. This indicates that FedAvg performed better in terms of generalization and accuracy on the test set. This can as well be observed from the validation scores that have been visualised in Figures \ref{fig:Avg_val}, \ref{fig:avg_global_val} \ref{fig:SGD_val} and \ref{fig:SGD_global_val}. Due to the nature of the problem, the loss and validation errors achieved relatively high values. That is, the method compares each pixel value independently, more likely resulting in more variation between the output and the goal. Nevertheless, the validation losses achieved during the training of FedSGD indicate it not generalising at all, but still being able to find a decently low convergence point. Due to this reason, the FedSGD global model requires more refined techniques for accurate function in all environments. It is important to mention that the test set errors were obtained using global models trained with a fixed number of epochs: the convergence to the validation set was not taken into account during training. The results may vary with different hyperparameters, dataset characteristics, and training settings. The training loss for both FedSGD and FedAvg global models with validation data from each dataset has been visualised in Figures \ref{fig:Avg_train} \ref{fig:SGD_train}. It can be observed that the FedSGD converged relatively quickly after few epochs compared to the more slow descent of the FedAvg. The performance of both global models has been visualised for all three datasets in Figure \ref{fig:Results}. The FedAvg seems to generalise more, as stated before. However, the FedSGD seems to produce clearer pictures for some datasets while producing uncertain noise for others. Based on these results, the FedAvg FL method was chosen for the presented scenario as the superior FL algorithm with more potential.


## Conclusion

In this study, the problem of data privacy in collaborative lane detection was addressed by investigating the application of FL approaches on TurtleBots. An experimental evaluation of the proposed FL framework was conducted using real-world lane detection datasets captured by TurtleBots. This evaluation provided practical evidence of the feasibility and effectiveness of the FL approach in collaborative lane detection tasks: the global model learned the given training sets with relatively good accuracy. The empirical results highlighted the potential of FL in improving data privacy while maintaining satisfactory detection accuracy. Based on the results, a superior FL method was chosen: FedAvg showcased better generalisation, thus more potential. The introduced FL methods were successful in ensuring data privacy by not requiring nodes to exchange any data directly: only gradients or weights were exchanged during training.

## Further improvements

Further studies should further emphasise on data privacy preservation through the adoption of encryption, differential privacy and/or secure communication protocols to the suggested framework when exchanging gradients/weights. In addition, the overall performance of the global models should be improved with more advanced architectures and training algorithms. More complex empirical graphs could also be explored when applying FL techniques for lane detection algorithms. For example, when detecting lanes from different environments, different weights could be placed to rarer/common environments when updating the global model.


