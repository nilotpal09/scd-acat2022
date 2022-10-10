---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
title:  "Simplified Cylindrical Detector"
image: 
  path: /images/header_photo.png
#   thumbnail: /images/scd_yz.png
  caption: "An event as seen in the Phoenix even display"
categories:
---
# Abstract 

The feature complexity of data recorded by particle detectors combined with the availability of large simulated datasets presents a unique environment for applying state-of-the-art machine learning (ML) architectures to physics problems. We present the Simplified Cylindrical Detector (SCD): a fully configurable GEANT4 calorimeter simulation which mimics the granularity and response characteristics of general purpose detectors at the LHC. The SCD will be released as a public software to accelerate development of ML-based reconstruction and calorimeter models. Two use-cases based on data from the SCD are presented: first, an ML-based global particle reconstruction which shows potential to outperform traditional approaches. Second, a fast simulation model transforming a set of truth particles into a set of reconstructed particles.

# Introduction

# Detector Design

Describe details of the design

- Inner Tracking System (ITS)
- ECAL
- HCAL

# Topoclustering

Describe topoclustering

<img src="images/scd_yz.png" class="align-center" alt="">

# ML Applications 

## ParticleFlow 

Describe ParticleFlow here.

## FastSim 

Describe FastSim here.

# Trackz...

<figure style="width: 300px" class="align-right">
  <img src="{{ '/images/tracks.png' | absolute_url }}" alt="">
  <figcaption>trackzzzzzzz....</figcaption>
</figure> 


<!-- <img src="images/tracks.png" class="align-right" alt=""> -->
