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

Currently, ML research in HEP is limited by the publicly available simulation tools. Most methods are developed using very simplified simulation setups like Delphes [[1]](#delphes) that applies a parametric smearing but does not take into account interactions between particles and detector material.

In order to fully exploit the potential of ML R&D it is necessary to have an as realistic setup as possible. Since internal detector simulations, of e.g. the ATLAS collaboration, are proprietary, a common, publicly available detector simulation is desired.

We present a fully configurable, open source, GEANT4 [[2]](#geant) based detector simulation for such HEP analysis. This detailed simulation infrastructure provides a reasonable foundation for the development of new experimental techniques. The calorimeter simulation mimics the granularity and response characteristics of general purpose detectors at the LHC. Two use-cases based on data from the SCD are presented: first, an ML-based global particle reconstruction which shows potential to outperform traditional approaches. Second, a fast simulation model transforming a set of truth particles into a set of reconstructed particles.

# Detector Design

The detector consists of the following parts:

- **Inner Tracking System (ITS)** The ITS consists of hollow cylinders at the center and disks at the edges. It applies smearing to the charged particle tracks and simulates material interactions. The hits, however, are not used for tracking though a potential extension with an open data tracking detector can be considered.

<figure style="width: 300px" class="align-right">
  <img src="{{ '/images/scd_yz.png' | absolute_url }}" alt="">
  <figcaption>Fig.2: Detector geometry</figcaption>
</figure> 

- **ECAL and HCAL** The calorimeter system lies on top of an iron layer seperating it from the ITS. Each of the calorimeters consists out of 3 layers. The calorimeter cells are designed such that in every layer each of them covers the same distance in terms of pseudorapidity and azimuthal angle, such that an approximately uniform distribution of incoming particles is obtained. Furthermore, the depth of the cells of every layer is constant in order to ensure that the layer fractions of deposited energy do not depend on the incoming particle direction. This design, leading to layer shapes of the form $1/\cosh \eta$, is similar to the ATLAS and CMS design and makes SCD better suited for shower learning tasks than a simple rectangular calorimeter design. The granularity and material composition is configurable with the default settings corresponding to the ATLAS setup.

An illustration of the geometry is given in Fig. 2.

# Event Processing

<figure style="width: 200px" class="align-right">
  <img src="{{ '/images/tracks.png' | absolute_url }}" alt="">
  <figcaption>Fig.3: Tracking</figcaption>
</figure> 

- Final state particles from the underlying event simulated by e.g. Pythia propagate through the ITS where a smearing is applied to the tracks of charged particles. An examplary event display of tracks is shown in Fig. 3.
- Material interactions are simulated within ECAL and HCAL. Deposited energy in each cell is recorded.
- Afterwards a jet clustering using the external FastJet [[3]](#fastj) library is applied.
- Finally, a Topoclustering algorithm clusters cells with energy deposits in a way that separates hadronic form electromagnetic showers and suppresses noise.

# ML Applications 

## ParticleFlow 

<figure style="width: 200px" class="align-right">
  <img src="{{ '/images/event_display.png' | absolute_url }}" alt="">
  <figcaption>Fig.4: Placeholder for Pflow plot</figcaption>
</figure> 

The task is to reconstruct particles from low-level
detector response data to predict the set of final state parti-
cles in a proton-proton collision event. A novel architecture applied to this problem for the first time is based on Hypergraphs [[4]](#hyperg). The main objective is to provide SCD data as input and obtain the reconstructed objects.

## FastSim 

<figure style="width: 200px" class="align-left">
  <img src="{{ '/images/event_display.png' | absolute_url }}" alt="">
  <figcaption>Fig.5: FastSim event display</figcaption>
</figure> 

We are developing a machine learning fast simulation tool that directly maps final state truth particles to the reconstructed events, skipping the computationally expensive detector simulation as well as the reconstruction step. The architecture is based on graph neural networks with slot-attention components. The training target are, ideally, events processed by the SCD with an additional ParticleFlow algorithm applied to it. At the current stage we use a simple smearing with a deterministic dropout on the final state particles to imitate detector and reconstruction effects. An examplary event display comparing our network to a baseline is shown in Fig. 5.

### References

<sub><a name="delphes">[1]</a> A. Mertens. *New features in Delphes 3.* J. Phys.281 Conf. Ser., 608(1):012045, 2015</sub>
<sub><a name="geant">[2]</a> S. Agostinelli et al. *GEANT4: A simulation toolkit.* Nucl. Instrum. Meth., A506:250–303, 2003</sub>
<sub><a name="fastj">[3]</a> M. Cacciari, G. P. Salam, G. Soyez. *FastJet user manual.* The European Physical Journal C,72(3), mar 2012</sub>
<sub><a name="hyperg">[4]</a> D. W. Zhang, G. J. Burghouts, C. GM Snoek. *Recurrently predicting hypergraphs.* arXiv preprint arXiv:2106.13919, 2021</sub>


# The SCD team

<sub>Francesco A. di Bello, Etienne Dreyer, Eilam Gross, Lukas Heinrich, Anna Ivina, Marumi Kado, Nilotpal Kakati, Patrick Rieck, Lorenzo Santi, Nathalie Soybelman, Matteo Tusoni</sub>


![no-alignment]({{ '/images/logos.png' | absolute_url }})
