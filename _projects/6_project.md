---
layout: page
title: Traditional vibration analysis
description: Commonly utilized techniques
img: assets/img/vcm_c.jpg
importance: 4
category: work
---

This page gives general insight into vibration based condition monitoring techniques. The term "traditional" refers to non-data-driven techniques (ML,DL...) utilized prior intelligent fault diagnosis (IFD) techniques (Most of these techniques are still in use in industry due to major problems present in IFD models, more information about these problems [here] (//). Traditional vibration based CM can be categorized into several approaches some of which are introduced in this page, along with their shortcomings.

## Introduction

While operating correctly, rotating machines still produce a distinct vibration signature, changing with the operating conditions such as the rotating speed and load of the machine. With rotating machines, this distinct vibrational pattern is a combination of relatively random background noise and cyclically occuring vibration phenomena, such as the gears meshing together in a bevel gear. Additionally, the foundation stiffness, damping and the specific component behaviour have a major effect in the inherent vibrations produced by the machine when it experiences an excitation. The frequencies of this inherent vibration are deemed as the natural frequencies of the machine. Changes in component specific frequencies, such as the gear mesh frequency (GMF), can often indicate a fault in that specific component. Frequencies corresponding to these common falt modes are often distinguished as the common fault frequencies of those specific components.  

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/vcm_c.jpg" %}
  </div>
</div>

## Instrumentation

TODO

## Time-domain analysis

Time-domain analysis can be conducted by directly comparing exctracted vibration signatures from a healthy and a faulty machine. Other forms of time-domain analysis include calculating features, such as the Root-mean square (RMS) value from the vibration signature and doing a similar comparison. By comparing their RMS values, one can determine which signal has greater overall energy or intensity, higher energy in similar operating conditions often signaling faulty behaviour. Features like this can be useful for the automation of CM systems, since raw time-domain analysis requires more finesse compared to the comparison of singular numerical features.

One of the main drawbacks of time-domain analysis is its limited ability to detect specific faults, especially in complex systems where multiple sources of vibration are present. Since time-domain analysis focuses on the overall signal characteristics, it may not effectively isolate or identify faults that manifest as subtle changes in vibration patterns. For instance, bearing defects or gear faults often produce small, high-frequency vibrations that may not significantly alter time-domain metrics such as RMS (Root Mean Square) or peak values. As a result, these faults can go undetected until they progress to more severe stages, leading to unexpected machine failures.

Time-domain analysis is inherently sensitive to noise, which can obscure the true characteristics of the vibration signal. In industrial environments, vibration signals are often contaminated with noise from various sources, including electrical interference, structural vibrations, and environmental factors. This noise can mask the presence of faults, making it difficult to differentiate between normal operational vibrations and those caused by defects. For example, in a scenario where a machine is operating in a noisy factory environment, the time-domain signal may appear erratic and show high RMS values due to noise, even if there are no significant faults in the machine. This sensitivity to noise reduces the reliability and accuracy of time-domain analysis.

Another significant limitation of time-domain analysis is its inability to provide frequency-specific information. Many mechanical faults, such as imbalance, misalignment, or gear mesh issues, produce characteristic frequencies that are essential for fault diagnosis. Time-domain analysis, however, does not reveal the frequency content of the signal, making it challenging to pinpoint the specific fault and its location. This lack of frequency resolution means that time-domain analysis alone is often insufficient for a comprehensive assessment of machine health. Analysts may need to supplement time-domain data with frequency-domain techniques to gain a complete understanding of the fault's nature and severity.

Operational conditions such as load changes, speed variations, and environmental factors can significantly influence time-domain vibration signals. These variations can lead to changes in time-domain metrics, potentially causing false alarms or missed fault detections. For example, a machine operating under varying load conditions may exhibit fluctuating RMS values, making it difficult to establish a consistent baseline for comparison. This variability complicates the task of distinguishing between normal operational changes and genuine fault conditions.

## Frequency domain analysis

One of the fundamental assumptions of frequency-domain analysis is that the signal is stationary, meaning its statistical properties do not change over time. In real-world scenarios, however, many vibration signals are non-stationary due to varying operational conditions, load changes, or transient events. When a non-stationary signal is analyzed using FFT, the resulting spectrum may not accurately represent the signal's true frequency content. This can lead to misinterpretation of the data, as transient faults or changes in the signal may be overlooked or incorrectly characterized.

Frequency-domain analysis is less effective in capturing transient events or non-periodic changes in the vibration signal. Transient events, such as impacts or sudden changes in machine operation, may contain valuable information about the onset of faults. However, FFT tends to smear these events across the frequency spectrum, making them difficult to detect and analyze. For instance, a sudden impact due to a bearing defect might produce a transient spike in the vibration signal, but this spike may not be easily identifiable in the frequency domain.

In complex machinery, multiple faults or vibration sources can produce overlapping frequency components. Frequency-domain analysis may struggle to distinguish between these components, leading to ambiguity in fault diagnosis. For example, both unbalance and misalignment can produce vibrations at the rotational frequency of the machine, making it challenging to determine the exact cause of the vibration based solely on frequency-domain data. This limitation necessitates the use of additional diagnostic techniques to resolve overlapping frequency components.

Frequency-domain analysis often involves identifying harmonics and sidebands associated with specific faults. However, interpreting these patterns can be complex, especially when multiple faults are present. Harmonics and sidebands can overlap or interact, creating complex spectral patterns that require expert knowledge to interpret accurately. Misinterpretation of these patterns can lead to incorrect fault diagnosis, resulting in unnecessary maintenance actions or missed fault detections.

## Envelope analysis

The success of envelope analysis heavily depends on selecting appropriate bandpass filters to isolate the frequency range of interest. Incorrect filter settings can either remove essential signal components or allow excessive noise into the analysis. Choosing the right filter parameters requires expert knowledge and experience, making envelope analysis less straightforward to implement effectively. In cases where the optimal filter parameters are not known, the analysis may produce unreliable or inconclusive results.

Envelope analysis is particularly suited for detecting bearing faults and other faults that generate high-frequency, repetitive impacts. However, it may not be effective for other types of faults, such as unbalance, misalignment, or structural resonance, which do not produce the characteristic high-frequency impacts detectable by envelope analysis. This specialization limits the scope of envelope analysis, requiring other techniques to be used in conjunction to achieve comprehensive fault detection.

## Order tracking analysis

Order tracking analysis is a technique used to analyze vibration signals in machinery with variable speeds. It converts the vibration signal into the order domain, where orders are harmonics of the rotational frequency, making it effective for diagnosing faults in variable-speed machines.

Order tracking analysis requires accurate information about the rotational speed of the machine, which can be challenging to obtain in some cases. Speed measurement sensors, such as tachometers, must be accurately synchronized with the vibration data acquisition system to ensure reliable order tracking. Any discrepancies in speed measurement can lead to inaccuracies in the analysis. The need for precise speed measurement and synchronization adds complexity to the implementation of order tracking analysis.

The effective use of order tracking analysis requires specialized knowledge and expertise in both the technique and the specific machinery being monitored. Understanding the relationship between orders and machine faults, as well as interpreting the results, requires experience and expertise. This reliance on expert knowledge can be a limitation in environments where such expertise is not readily available, making order tracking analysis less accessible to non-specialist users.

## Time-frequency domain analysis

Time-frequency domain analysis techniques, such as wavelet transforms, provide a powerful tool for analyzing non-stationary and transient signals. By offering time-frequency localization, these techniques are effective in capturing transient events and changes in the signal over time.

## Cepstrum analysis

Cepstrum analysis is used to detect periodicities in the frequency spectrum, revealing harmonics and sidebands that indicate faults such as gear mesh issues or bearing defects. 

## Statistical methods

Statistical methods, including kurtosis, skewness, and other statistical measures, are used to detect subtle changes in vibration signals that may indicate early-stage faults.

## Operational deflection shape (ODS) analysis

## Modal analysis

## Cyclostationary analysis


