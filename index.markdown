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

<video width="320" controls>
  <source src="images/detector_sim.mp4" type="video/mp4">
</video>

# Introduction

Currently, ML research in HEP is limited by the publicly available simulation tools. Most methods are developed using very simplified simulation setups like Delphes [[1]](#delphes) that applies a parametric smearing but does not take into account interactions between particles and detector material.

In order to fully exploit the potential of ML R&D it is necessary to have an as realistic setup as possible. Since internal detector simulations, of e.g. the ATLAS collaboration, are proprietary, a common, publicly available detector simulation is desired.

We present a fully configurable, open source, GEANT4 [[2]](#geant) based detector simulation for such HEP analysis. This detailed simulation infrastructure provides a reasonable foundation for the development of new experimental techniques. The calorimeter simulation mimics the granularity and response characteristics of general purpose detectors at the LHC. Two use-cases based on data from the SCD are presented: first, an ML-based global particle reconstruction which shows potential to outperform traditional approaches. Second, a fast simulation model transforming a set of truth particles into a set of reconstructed particles.

# Detector Design and Event Processing

- Final state truth particles produced by Pythia8[[3]](#pyth) from underlying specified event

<figure style="width: 200px" class="align-right">
  <img src="{{ '/images/tracks.png' | absolute_url }}" alt="">
  <figcaption>Fig.2: Tracking</figcaption>
</figure> 

- **Inner Tracking System (ITS)** Particles pass through the ITS which consists of hollow cylinders at the center and disks at the edges. A smearing to the charged particle tracks is applied and material interactions are simulated. The hits, however, are not used for tracking though a potential extension with an open data tracking detector can be considered.

- **ECAL and HCAL** The calorimeter system lies on top of an iron layer seperating it from the ITS. Both calorimeters consist of 3 layers. In each layer the cells have a constant depth and cover the same distance in terms of pseudorapidity and azimuthal angle. This ensures a uniform distribution of incoming particles and the layer fraction of deposited energy not to depend on the direction of incoming particles. The obtained $1/\cosh \eta$ shape is similar to the ATLAS and CMS design and is better suited for shower learning tasks than a rectangular calorimeter design. The granularity and material composition is configurable with the default settings corresponding to the ATLAS setup. Particles interact with the material and the deposited energy is recorded.

<figure style="width: 300px" class="align-center">
  <img src="{{ '/images/scd_yz.png' | absolute_url }}" alt="">
  <figcaption>Fig.3: Detector geometry</figcaption>
</figure> 

- A jet clustering using the external FastJet [[4]](#fastj) library is applied.

- A Topoclustering algorithm clusters cells with energy deposits to separates hadronic form electromagnetic showers and suppress noise.

# Performance

Fig.4 shows the energy deposists in the different layers for different particles which matches the expectation.

<figure style="width: 200px" class="align-right">
  <img src="{{ '/images/layerdeposit.png' | absolute_url }}" alt="">
  <figcaption>Fig.4: Energy deposit by layer</figcaption>
</figure> 

# ML Applications 

- **ParticleFlow** The task is to reconstruct particles from the detector response to predict the set of final state particles. The main objective is to provide SCD data as input and obtain the reconstructed objects.

- **FastSim** This tool is being developed to directly map final state truth particles to the reconstructed events, skipping detector simulation and reconstruction. Events processed by the SCD with an additional ParticleFlow algorithm applied are used as target for training. 

### References

<sub><a name="delphes">[1]</a> A. Mertens. *New features in Delphes 3.* J. Phys.281 Conf. Ser., 608(1):012045, 2015</sub><br/>
<sub><a name="geant">[2]</a> S. Agostinelli et al. *GEANT4: A simulation toolkit.* Nucl. Instrum. Meth., A506:250–303, 2003</sub><br/>
<sub><a name="pyth">[3]</a> C. Bierlich, et al. *A comprehensive guide to the physics and usage of pythia 8.3*, 2022</sub><br/>
<sub><a name="fastj">[4]</a> M. Cacciari, G. P. Salam, G. Soyez. *FastJet user manual.* The European Physical Journal C,72(3), mar 2012</sub><br/>

# The SCD team

<sub>Francesco A. di Bello, Etienne Dreyer, Eilam Gross, Lukas Heinrich, Anna Ivina, Marumi Kado, Nilotpal Kakati, Patrick Rieck, Lorenzo Santi, Nathalie Soybelman, Matteo Tusoni</sub>


![no-alignment]({{ '/images/logos.png' | absolute_url }})
