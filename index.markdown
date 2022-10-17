---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
title:  "Simplified Cylindrical Detector"
image: 
  path: /images/header_photo.png
  thumbnail: /images/scd_logo_2_small.png
  caption: "Fig. 1: An event as seen in the Phoenix event display"
categories:
---
<!-- <div align="center">
Nilotpal Kakati and Nathalie Soybelman on behalf of the [SCD-Team](#the-scd-team)
</div>
<br /> -->

Nilotpal Kakati and Nathalie Soybelman on behalf of the [SCD-Team](#the-scd-team)

# Introduction

Currently, ML research in HEP is limited by the publicly available simulation tools. Most methods are developed using very simplified simulation setups like Delphes [1] that applies a parametric smearing but does not take into account interactions between particles and detector material.
In order to fully exploit the potential of ML R&D it is necessary to have an as realistic setup as possible. Since internal detector simulations, of e.g. the ATLAS collaboration, are proprietary, a common, publicly available detector simulation is desired.
We present a fully configurable, open source, GEANT4 [2] based detector simulation for such HEP analysis. This detailed simulation infrastructure provides a reasonable foundation for the development of new experimental techniques. This calorimeter simulation mimics the granularity and response characteristics of general purpose detectors at the LHC. Two use-cases based on data from the SCD are presented: first, an ML-based global particle reconstruction which shows potential to outperform traditional approaches. Second, a fast simulation model transforming a set of truth particles into a set of reconstructed particles.

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

- Final state particles from the underlying event simulated by e.g. Pythia propagate through the ITS where a smearing is applied to the tracks of charged particles. An examplary event display of tracks is shown in Fig. 3.
- Material interactions are simulated within ECAL and HCAL. Deposited energy in each cell is recorded.
- For the jet clustering makes use of the external FastJet [3] library.
- A Topoclustering algorithm clusters cells with energy deposits in a way that separates hadronic form electromagnetic showers and suppresses noise.

<figure style="width: 300px" class="align-right">
  <img src="{{ '/images/tracks.png' | absolute_url }}" alt="">
  <figcaption>Fig.3: Tracking</figcaption>
</figure> 

# ML Applications 

## ParticleFlow 

The task is to reconstruct particles from low-level
detector response data to predict the set of final state parti-
cles in a proton-proton collision event. A novel architecture applied to this problem for the first time is based on Hypergraphs[4]. The main objective is to provide SCD data as input and obtain the reconstructed objects.
<figure style="width: 200px" class="align-right">
  <img src="{{ '/images/event_display.png' | absolute_url }}" alt="">
  <figcaption>Fig.5: Placeholder for Pflow plot</figcaption>
</figure> 

## FastSim 

We are developing a machine learning fast simulation tool that directly maps final state truth particles to the reconstructed events, skipping the computationally expensive detector simulation as well as the reconstruction step. The architecture is based on graph neural networks with slot-attention components. The training target are, ideally, events processed by the SCD with an additional ParticleFlow algorithm applied to it. At the current stage we use a simple smearing with a deterministic dropout on the final state particles to imitate detector and reconstruction effects. An examplary event display comparing our network to a baseline is shown in Fig. 5.
<figure style="width: 200px" class="align-left">
  <img src="{{ '/images/event_display.png' | absolute_url }}" alt="">
  <figcaption>Fig.5: FastSim event display</figcaption>
</figure> 

### References

<sub>[1] A. Mertens. *New features in Delphes 3.* J. Phys.281 Conf. Ser., 608(1):012045, 2015</sub>
<br />
<sub>[2] S. Agostinelli et al. *GEANT4: A simulation toolkit.* Nucl. Instrum. Meth., A506:250–303, 2003</sub>
<br />
<sub>[3] M. Cacciari, G. P. Salam, G. Soyez. *FastJet user manual.* The European Physical Journal C,72(3), mar 2012</sub>
<br />
<sub>[4] D. W. Zhang, G. J. Burghouts, C. GM Snoek. *Recurrently predicting hypergraphs.* arXiv preprint arXiv:2106.13919, 2021</sub>
<br />

# The SCD team

<sub>Francesco A. di Bello, Etienne Dreyer, Eilam Gross, Lukas Heinrich, Anna Ivina, Marumi Kado, Nilotpal Kakati, Patrick Rieck, Lorenzo Santi, Nathalie Soybelman, Matteo Tusoni</sub>


![no-alignment]({{ '/images/logos.png' | absolute_url }})
