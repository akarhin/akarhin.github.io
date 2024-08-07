---
layout: page
title: fault injection with GANs
description: 
img: assets/img/gan_image.jpg
importance: 1
category: work
---
## Introduction

Automation of condition monitoring (CM) systems has been gaining wide research interest. Specifically, data-driven intelligent fault diagnosis (IFD) solutions have gained popularity in the field. However, solutions based on machine learning (ML) and recently deep learning (DL) suffer from three significant problems which limit their use in industry:

- Data scarcity: IFD models require large quantities of examples in the form of vibration data from different operating conditions, machines and fault modes in order to function in the proper accuracy range.
- Generalization: IFD models struggle to generalize outside the given training set. This leads to the training of a multitude of models for fleets of machines, or required constant retraining of prior models, which can lead to catastrophic forgetting of prior knowledge.
- Explainability: ML and DL solutions are often perceived as black boxes. This leads to decreased trust, or worse, unwarranted trust building towards these types of solutions.

This works aims to answer one of these problems, Data scarcity, by leveraging a limited amount of fault samples in order to train a GAN generator to learn to "inject" fault modes into healthy vibration samples.
