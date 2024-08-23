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

## Instrumentation

TODO

## Time-domain analysis

Time-domain analysis can be conducted by directly comparing exctracted vibration signatures from a healthy and a faulty machine. Other forms of time-domain analysis include calculating features, such as the Root-mean square (RMS) value from the vibration signature and doing a similar comparison. By comparing their RMS values, one can determine which signal has greater overall energy or intensity, higher energy in similar operating conditions often signaling faulty behaviour. Features like this can be useful for the automation of CM systems, since raw time-domain analysis requires more finesse compared to the comparison of singular numerical features.

## Frequency domain analysis

## Envelope analysis

## Order tracking analysis

## Time-frequency domain analysis

## Cepstrum analysis

## Statistical methods

## Operational deflection shape (ODS) analysis

## Modal analysis

## Cyclostationary analysis

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/vcm_c.jpg" %}
  </div>
</div>
