---
layout: page
title: Domain Adaptation for engine condition monitoring
description: Sim2Real domain adaptation
img: assets/img/Domain_adaptation_engines.jpg
importance: 5
category: work
---

## Introduction

Condition monitoring of large combustion engines is critical for ensuring operational safety and prolonging engine life. Traditional methods often require extensive instrumentation to accurately detect faults such as cylinder-specific misfire or heavy knocking, complicating the data acquisition process for intelligent fault diagnosis. Simulation-based approaches are commonly used to generate data for condition monitoring thresholds or as training data for data-driven fault diagnosis models, addressing challenges in data scarcity. However, discrepancies between simulation models and real-world lead to inaccuracies in the intelligent fault diagnosis models. These inaccuracies often affect the accuracy of intelligent fault diagnosis models, if samples obtained from simulation models are utilized to train them. 

Domain adaptation is a subset of transfer learning, where a intelligent model is trained in a specific domain (source) and then tested and validated in another domain (target). However, the task remains the same. That is, the label space remains constant while the input space contains variation. This project introduces the scenario present in Sim-to-Real condition monitoring problems. The project is based on a journal article currently in writing. 

## Problem formulation

Let \( \mathcal{X} \) represent the input space and \( \mathcal{Y} \) the output space. For a multi-class classification problem, where \( \mathcal{Y} \) is a finite set of classes, \( \mathcal{H} \), the hypotheses under consideration, map from \( \mathcal{X} \) to \( \mathcal{Y} \). Therefore, \( h(x) \) represents a probability distribution over the classes in \( \mathcal{Y} \) for each \( x \in \mathcal{X} \). Let \( \ell \) be a loss function, which outputs non-negative values. For any \( h \in \mathcal{H} \), the loss on a labelled sample \( (x, y) \in \mathcal{X} \times \mathcal{Y} \) is given by \( \ell(h(x), y) \). The expected loss of a hypothesis \( h \) with respect to a distribution \( D \) over \( \mathcal{X} \times \mathcal{Y} \) is defined as:

\begin{align}
    L_D(h) &= \mathbb{E}_{(x, y) \sim D} \left[ \ell(h(x), y) \right],
\end{align}

The hypothesis \( h_D \) that minimizes this expected loss is given by:

\begin{align}
    h_D &= \arg\min_{h \in \mathcal{H}} L_D(h).
\end{align}

This formulation corresponds to the traditional supervised setting. 

Domain adaptation is a special case of transfer learning that assumes a similar feature structure and label space \( \mathcal{Y} \), while including a varying input space \( \mathcal{X} \). That is, the source and target distributions have different probability distributions. While transfer learning spans task transfer and properly labelled target datasets, domain adaptation assumes an unlabelled or a partly labelled target dataset. Therefore, we denote \( \mathcal{D}_s \) as the source domain and \( \mathcal{D}_t \) as the target domain. Domain adaptation is defined such that the model predicts labels from the target domain given labelled data from the source domain. That is, a hypothesis is established in the source domain, often regularized in some way, and then utilized in the target domain with unknown labels \cite{farahani2021brief,singhal2023domain} :



\begin{align}
    L_{D_s}(h) &= \mathbb{E}_{(x, y) \sim \mathcal{D}_s} \left[ \ell(h(x), y) \right],
\end{align}

\begin{align}
    L_{Reg}(h) &= \mathbb{E}_{x \sim \mathcal{D}_t} \left[ \ell_{reg}(h(x)) \right]
\end{align}
    
\begin{align}   
    h^* = \arg\min_{h \in \mathcal{H}} L_{D_s}(h) + \lambda L_{Reg}(h).
\end{align}

Here, $h^* $ corresponds to a trained hypothesis $h$ that minimizes the source loss $L_{D_s}(h)$ while being regularized with the regularization term $L_{Reg}(h)$. The hypothesis $h^*$ is then utilized on the target dataset. The simplest experiment is to determine a hypothesis based on the source data and directly apply it to the target data without specific regularization. This approach is known as direct transfer. Direct transfer assumes that the source and target distributions contain similar and domain general features inherently. Therefore, the optimization problem only minimizes the expected loss of the hypothesis with respect to the source domain. In this case, the minimization objective remains the same as in traditional supervised setting, or as in Equation (1). However, as expected, this rarely yields satisfactory results in Sim-to-Real transfer, unless the source and target domains align well enough.

## Domain adaptation

Domain adaptation is a well established field within machine and deep learning research. Often utilized approaches include finding a common representation space for both data domains. The common representation space approach aims to obtain a hypothesis that performs well on the entire target domain, using an intermediate representation or transformation \( \Phi \) to align the source and target distributions, which ideally allow the extraction of domain-general features:

\begin{align}
    h_{D_t} &= \arg\min_{h \in \mathcal{H}, \Phi} L_{D_t}(\Phi, h),
\end{align}

where:

\begin{align}
    L_{D_t}(\Phi, h) &= \mathbb{E}_{(x, y) \sim D_t} \left[ \ell(h(\Phi(x)), y) \right].
\end{align}

With vibration data, this could be as simple as transforming the time-series signal into frequency domain with techniques such as the fast fourier transform. Other techniques include noise injection to account for inherent noise present in real measurements. Many libraries have been developed to implement domain adaptation methods, such as the Awesome Domain Adaptation Python Toolbox (ADABT) available [here, https://github.com/adapt-python/adapt].

Domain adaptation methods can be split into three separate categories:

\begin{itemize}
    \item Feature-based methods
    \item Instance-based methods
    \item Parameter-based methods
\end{itemize}




