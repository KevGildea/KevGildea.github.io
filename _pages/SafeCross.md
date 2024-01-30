---
permalink: /SafeCross/
title: "SafeCross: Open source application for predictive modelling of cyclist crossing success on tram tracks"
---

<p align="center">
  <img src="/assets/images/SafeCross/SafeCross_AUTO.gif" width="900">
</p>

## Introduction

SafeCross is an open-source framework for proactively assessing risk for single bicycle crashes at locations where cyclists interact with tram tracks. 

Cyclist detection and tracking is automatically performed using advanced computer vision and deep learning techniques. The trajectories are then automatically processed to calculate the angles at which the cyclists crossed the tracks. These are then fed into a risk model for predicting the probability of crossing success. Risk estimates are then compiled to predict the number of unsuccessful crossings that may occur over time, and to generate a risk heatmap which highlights risky sections of the tracks.

The tool is a standalone Windows application, and was designed with ease-of-use in mind. It can be run using a standard CPU, without the need for a cuda-enabled GPU, or any coding/manual data processing.


<p align="center">
  <img src="/assets/images/SafeCrossSafeCross_pipeline.png" width="900">
</p>

## Tools


| Step                  | Description                                                  | Tools                                     | Manuals                                  |
|-----------------------|--------------------------------------------------------------|-------------------------------------------|------------------------------------------|
| T-calibration               |                        | [Tools](){:target="_blank"} | TBD |
| SafeCross TA               |                        | [Tool](){:target="_blank"} | TBD |
| SafeCross AUTO             |                        | [Tool](){:target="_blank"} | TBD |



## Example application in Dublin, Ireland



## Conference presentations
- [International Cycling Safety Conference (ICSC 2022)](https://cyclingsafety.net/)

## Cite our methods papers
If you find SafeCross useful in your research, please consider citing our work:

```
@article{Gildea2023,
   author = {Kevin Gildea and Daniel Hall and Clara Mercadal-Baudart and Brian Caulfield and Ciaran Simms},
   doi = {10.1016/J.JSR.2023.09.017},
   issn = {0022-4375},
   journal = {Journal of Safety Research},
   month = {10},
   publisher = {Pergamon},
   title = {Computer vision-based assessment of cyclist-tram track interactions for predictive modeling of crossing success},
   year = {2023}
}

```
