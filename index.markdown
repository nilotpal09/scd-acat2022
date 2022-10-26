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

__Nilotpal Kakati and Nathalie Soybelman on behalf of the [SCD-Team](#the-scd-team)__


<!-- # Introduction

Currently, ML research in HEP is limited by the publicly available simulation tools. Most methods are developed using very simplified simulation setups like Delphes [[1]](#delphes) that applies a parametric smearing but does not take into account interactions between particles and detector material.

In order to fully exploit the potential of ML R&D it is necessary to have an as realistic setup as possible. Since internal detector simulations, of e.g. the ATLAS collaboration, are proprietary, a common, publicly available detector simulation is desired.

We present a fully configurable, open source, GEANT4 [[2]](#geant) based detector simulation for such HEP analysis. This detailed simulation infrastructure provides a reasonable foundation for the development of new experimental techniques. The calorimeter simulation mimics the granularity and response characteristics of general purpose detectors at the LHC. [Two use-cases](#ml-applications) based on data from the SCD are presented: first, an ML-based global particle reconstruction which shows potential to outperform traditional approaches. Second, a fast simulation model transforming a set of truth particles into a set of reconstructed particles. -->

<p style="margin-bottom:15mm;"></p>

# [Intorduction](#intorduction)

ML research in High Energy Physics (HEP) requires to have a realistic detector simulation, but the available tools are either - 
- Very detailed and accurate, but __internal and proprietory__ to experiments like ATLAS and CMS.
- Open sourced, but __very simplified, parameteric setup__ like Delphes [[1]](#delphes) that do not take into account interactions between particles and detector material.

We present -
- __Simplified Cylindircal Detetector (SCD)__, a fully configurable, open source, GEANT4 [[2]](#geant) based detector simulation
- SCD mimics the granularity and response characteristics of general purpose detectors at the LHC like ATLAS and CMS

We also show two [ML use-cases](#scd-in-action) -
- an ML-based global particle reconstruction which shows potential to outperform traditional approaches
- a fast simulation model transforming a set of truth particles into a set of reconstructed particles

<p style="margin-bottom:10mm;"></p>

# [Detector Design and Event Processing](#detector-design-and-event-processing)

- Final state truth particles produced by Pythia8 [[3]](#pyth) from underlying specified event

<figure style="width: 80%" class="align-center">
  <img src="{{ '/images/scd_yz.png' | absolute_url }}" alt="">
  <figcaption>Fig.3: Detector geometry</figcaption>
</figure> 

<!-- - **Inner Tracking System (ITS)** Particles pass through the ITS which consists of hollow cylinders at the center and disks at the edges. A smearing to the charged particle tracks is applied and material interactions are simulated. The hits, however, are not used for tracking though a potential extension with an open data tracking detector can be considered. -->

<figure style="width: 80%" class="align-center">
  <img src="{{ '/images/tracks.png' | absolute_url }}" alt="">
  <figcaption>Fig.2: Tracking</figcaption>
</figure> 

- **Inner Tracking System (ITS)** 
  - The ITS consists of hollow cylinders at the center and disks at the edges
  - Required to simulate material interactions for accurate shower simulation
  - Parameterized tracks with smearing
  - _Potential extension with an open data tracking detector_ (in future).

<!-- - **ECAL and HCAL** The calorimeter system lies on top of an iron layer seperating it from the ITS. Both calorimeters consist of 3 layers. In each layer the cells have a constant depth and cover the same distance in terms of pseudorapidity and azimuthal angle. This ensures a uniform distribution of incoming particles and the layer fraction of deposited energy not to depend on the direction of incoming particles. The obtained cosine hyperbolic shape is similar to the ATLAS and CMS design and is better suited for shower learning tasks than a rectangular calorimeter design. The granularity and material composition is configurable with the default settings corresponding to the ATLAS setup. Particles interact with the material and the deposited energy is recorded. -->

- **ECAL and HCAL** 
  - An iron layer seperates ECAL from the ITS. 
  - Both calorimeters consist of 3 layers. 
  - In each layer the cells have a constant depth and cover the same distance in terms of pseudorapidity and azimuthal angle. 
  - This ensures a uniform distribution of incoming particles and the layer fraction of deposited energy not to depend on the direction of incoming particles. 
  - The obtained cosine hyperbolic shape is similar to the ATLAS and CMS design and is better suited for shower learning tasks than a rectangular calorimeter design. 
  - **The granularity and material composition is configurable** with the default settings corresponding to the ATLAS setup. Particles interact with the material and the deposited energy is recorded.

<p style="margin-bottom:5mm;"></p>

- Supports __jet clustering__ using the external FastJet [[4]](#fastj) library

- Has an __inbuilt Topoclustering algorithm__ to cluster cells with energy deposits to separate hadronic form electromagnetic showers and suppress noise.

<p style="margin-bottom:10mm;"></p>

# [Performance](#performance)

For the following plots individual particles were sent through the detector and the response was recorded.

- The energy deposits in the different layers for charged pions, electrons and photons.

<figure style="width: 80%" class="align-center">
  <img src="{{ '/images/layerdeposit.png' | absolute_url }}" alt="">
  <figcaption>Fig.4: Energy deposit by layer</figcaption>
</figure>

- The total cell energy of the topoclusters for different initial energies for photons. 

<figure style="width: 80%" class="align-center">
  <img src="{{ '/images/energy_cell_sum.png' | absolute_url }}" alt="">
  <figcaption>Fig.5: Deposited energy for photons</figcaption>
</figure> 

<p style="margin-bottom:10mm;"></p>

# [Phoenix Event Display](#phoenix-event-display)

A Phoenix support for the detector simulation was implemented. It shows - 
  - the detector geometry
  - the physical objects in an event - tracks, jets and cells. 

A demo with a ttbar event -

<video width="100%" controls>
  <source src="images/detector_sim.mp4" type="video/mp4">
</video>

<p style="margin-bottom:10mm;"></p>

# [SCD in Action](#scd-in-action)

<figure style="width: 100%" class="align-center">
  <img src="{{ '/images/EHEP_pipeline.png' | absolute_url }}" alt="">
  <figcaption>Fig.5: Deposited energy for photons</figcaption>
</figure> 

<!-- - **ParticleFlow** The task is to reconstruct particles from the detector response to predict the set of final state particles. The main objective is to provide SCD data as input and obtain the reconstructed objects. -->

#### [ParticleFlow](#particleflow)

We try to reconstruct the final state particles from the detector readout using multiple graph-based approaches (object condensation, TSPN + slot attention (SA), Recurrently learning hypergraphs (HG)). The novel approach with HG seems to outperform the traditional baseline, and the other ML approaches

An example event. __Thanks to SCD, we can also investigate what's happening at the cell level!__ 

Lorenzo's ED for an event (will add it later)

+

ECAL1 for the same  (will add it later)

 _(paper coming soon!)_

#### [FastSim](#fastsim)

This tool is being developed to directly map final state truth particles to the reconstructed events, skipping detector simulation and reconstruction. Events processed by the SCD with an additional ParticleFlow algorithm applied are used as target for training. 

<figure style="width: 100%" class="align-center">
  <img src="{{ '/images/FS_results.png' | absolute_url }}" alt="">
  <figcaption>Fig.6: Deposited energy for photons</figcaption>
</figure> 

 _(paper coming soon!)_

### References

<sub><a name="delphes">[1]</a> A. Mertens. *New features in Delphes 3.* J. Phys.281 Conf. Ser., 608(1):012045, 2015</sub><br/>
<sub><a name="geant">[2]</a> S. Agostinelli et al. *GEANT4: A simulation toolkit.* Nucl. Instrum. Meth., A506:250–303, 2003</sub><br/>
<sub><a name="pyth">[3]</a> C. Bierlich, et al. *A comprehensive guide to the physics and usage of pythia 8.3*, 2022</sub><br/>
<sub><a name="fastj">[4]</a> M. Cacciari, G. P. Salam, G. Soyez. *FastJet user manual.* The European Physical Journal C,72(3), mar 2012</sub><br/>

# [The SCD team](#the-scd-team)

<!-- <sub>Francesco A. di Bello, Etienne Dreyer, Sanmay Ganguly, Eilam Gross, Lukas Heinrich, Anna Ivina, Marumi Kado, Nilotpal Kakati, Patrick Rieck, Lorenzo Santi, Nathalie Soybelman, Matteo Tusoni</sub> -->

<style>
  .avatar {
    vertical-align: middle;
    width: 100%;
    height: 100%;
    border-radius: 50%;
    /* -webkit-filter: grayscale(100%);
    filter: grayscale(100%); */
  }

  .avatar_figure {
    vertical-align: top;
    display: inline-block;
    /* border: 1px dotted gray; */
    margin: 10px; 
    width: 80px;
  }

  .avatar_caption {
    /* border: 1px dotted blue; */
    text-align: middle;
  }
}</style>


<!-- <div class="container">
  <img src="images/Nilotpal_BW.png" alt="Nilotpal Kakati" class="avatar">
  <img src="images/Nilotpal_BW.png" alt="Nilotpal Kakati" class="avatar">
</div> -->

<!-- <div class="container"> -->
<div>

  <figure class="avatar_figure">
    <img src='images/team/francesco.png' alt='missing' class="avatar">
    <figcaption class="avatar_caption">
      Francesco A. Di Bello
    </figcaption>
  </figure>

  <figure class="avatar_figure">
    <img src='images/team/etienne.png' alt='missing' class="avatar">
    <figcaption class="avatar_caption">
      Etienne Dreyer
    </figcaption>
  </figure>

  <figure class="avatar_figure">
    <img src='images/team/sanmay.jpg' alt='missing' class="avatar">
    <figcaption class="avatar_caption">
      Sanmay Ganguly
    </figcaption>
  </figure>

  <figure class="avatar_figure">
    <img src='images/team/eilam.png' alt='missing' class="avatar">
    <figcaption class="avatar_caption">
      Eilam Gross
    </figcaption>
  </figure>

  <figure class="avatar_figure">
    <img src='images/team/lukas.png' alt='missing' class="avatar">
    <figcaption class="avatar_caption">
      Lukas Heinrich
    </figcaption>
  </figure>

  <figure class="avatar_figure">
    <img src='images/team/anna.png' alt='missing' class="avatar">
    <figcaption class="avatar_caption">
      Anna Ivina
    </figcaption>
  </figure>

  <figure class="avatar_figure">
    <img src='images/team/marumi.png' alt='missing' class="avatar">
    <figcaption class="avatar_caption">
      Marumi Kado
    </figcaption>
  </figure>

  <figure class="avatar_figure">
    <img src='images/team/Nilotpal.png' alt='missing' class="avatar">
    <figcaption class="avatar_caption">
      Nilotpal kakati
    </figcaption>
  </figure>

  <figure class="avatar_figure">
    <img src='images/team/patrick.jpg' alt='missing' class="avatar">
    <figcaption class="avatar_caption">
      Patrick Reick
    </figcaption>
  </figure>

  <figure class="avatar_figure">
    <img src='images/team/lorenzo.jpeg' alt='missing' class="avatar">
    <figcaption class="avatar_caption">
      Lorenzo Santi
    </figcaption>
  </figure>

  <figure class="avatar_figure">
    <img src='images/team/nathalie.png' alt='missing' class="avatar">
    <figcaption class="avatar_caption">
      nathalie Soybelman
    </figcaption>
  </figure>

  <figure class="avatar_figure">
    <img src='images/team/matteo.png' alt='missing' class="avatar">
    <figcaption class="avatar_caption">
      MAtteo Tusoni
    </figcaption>
  </figure>

</div>


<!-- <div class="container">
  <img src="images/Nilotpal_BW.png" alt="Avatar" style="border-radius:50%;width:20%" figcaption="Nilotpal kakati">
  <img src="images/Nilotpal_BW.png" alt="Avatar">
</div> -->

<p style="margin-bottom:0.5cm;"></p>

![no-alignment]({{ '/images/logos.png' | absolute_url }})
