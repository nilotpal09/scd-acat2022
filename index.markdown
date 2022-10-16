---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
title:  "Simplified Cylindrical Detector"
image: 
  path: /images/header_photo.png
#   thumbnail: /images/scd_yz.png
  caption: "Fig. 1: An event as seen in the Phoenix even display"
categories:
---
### Francesco A. di Bello, Etienne Dreyer, Eilam Gross, Lukas Heinrich, Anna Ivina, Marumi Kado, Nilotpal Kakati, Patrick Rieck, Lorenzo Santi, Nathalie Soybelman 

# Introduction

We present a fully configurable, open source, GEANT4 based detector simulation for HEP analysis. This detailed simulation infrastructure provides a reasonable foundation for the development of new experimental techniques. This calorimeter simulation mimics the granularity and response characteristics of general purpose detectors at the LHC. Two use-cases based on data from the SCD are presented: first, an ML-based global particle reconstruction which shows potential to outperform traditional approaches. Second, a fast simulation model transforming a set of truth particles into a set of reconstructed particles.

# Detector Design

The detector consists of the following 3 parts:
- Inner Tracking System (ITS)
- ECAL
- HCAL
The geometry is depicted in Fig. 2. The default setting correspond to a detector similar to ATLAS. 

<figure style="width: 300px" class="align-right">
  <img src="{{ '/images/scd_yz.png' | absolute_url }}" alt="">
  <figcaption>Fig.2: Detector geometry</figcaption>
</figure> 


# Event Processing

- Truth particles from the underlying event simulated by e.g. Pythia propagate through the ITS where a smearing is applied to the tracks of charged particles. An examplary event display of tracks is shown in Fig. 3.
- Material interactions are simulated within ECAL and HCAL. Deposited energy in each cell is recorded.
- For the jet clustering makes use of the external FastJet library.
- A Topoclustering algorithm clusters cells with energy deposits in a way that separates hadronic form electromagnetic showers and suppresses noise.

<figure style="width: 300px" class="align-right">
  <img src="{{ '/images/tracks.png' | absolute_url }}" alt="">
  <figcaption>Fig.3: Tracking</figcaption>
</figure> 

# ML Applications 

## ParticleFlow 

Describe ParticleFlow here.

## FastSim 

Describe FastSim here.

# Trackz...




<!-- <img src="images/tracks.png" class="align-right" alt=""> -->
