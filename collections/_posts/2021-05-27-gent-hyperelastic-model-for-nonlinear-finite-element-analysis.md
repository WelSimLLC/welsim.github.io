---
lang: en
layout: post
title:  "Gent hyperelastic model for nonlinear finite element analysis"
date:   2021-05-28
author: "[SimLet](https://twitter.com/getwelsim)"
---


In previous articles, we introduced Arruda-Boyce, neo-Hookean, Mooney-Rivlin, and Yeoh hyperelastic models. Today, let’s discuss another well-known hyperelastic model: Gent. A phenomenological model of rubber elasticity that is based on the concept of limiting chain extensibility. In this model, a simple mathematical form is used to describe the nonlinear constitutive model of rubber. Like most hyperelastic models, Gent is a model named after a person’s surname. Thanks to Dr. Gent for his contribution to this hyperelastic model.


<p align="center">
  <img src="https://miro.medium.com/max/652/1*MLGjGYTqUY1bxdbgc1N_fg.png"/>
</p>

In 1996, Gent published a short paper called “A new constitutive relation for rubber” in the journal “Rubber Chemistry and Technology” that proposed the use of a simple two-parameter phenomenological constitutive model for hyperelastic isotropic incompressible materials. The model is empirical but has the advantages of mathematical simplicity, reflects the severe strain-stiffening at large strains observed experimentally. The Gent model has widespread applications that not only in rubber elasticity but also in the area of the biomechanics of soft biomaterials. This model connects the macroscopic scale behavior to the mesoscopic structure of polymeric networks. Gent model lays a certain foundation for the future research of multiscale research. WELSIM already supports the Gent hyperelastic model.

<p align="center">
  <img src="https://miro.medium.com/max/1070/1*uKL5LDPAhhigzSw_hu9aeQ.png"/>
</p>

Dr. Alan Neville Gent (1927–2012) was born in the UK. Gent was educated at the University of London, where he earned degrees in physics and math before receiving his Ph.D. in 1955 on the mechanics of rubber and plastics. Before he relocated to the USA, Dr. Gent worked at the John Bull Rubber Co., British Army, and British Rubber Producer’s Research Association. This is similar to Rivlin’s experience, except that Rivlin is 10+ years older than Gent. In 1961, Dr. Gent joined the faculty at The University of Akron. He directed to completion more than 40 Ph.D. dissertations and 35 M.S. theses. He also served as a consultant and scientific adviser to the Research Division of The Goodyear Tire & Rubber Company from 1964 to 2002. Dr. Gent has published more than 200 articles and book chapters. He is also the chairman of several related societies. In 1991 he was elected to the National Academy of Engineering. Gent has devoted his life to the research of polymer materials and its mechanics and has won numerous awards.

<p align="center">
  <img src="https://miro.medium.com/max/861/1*AKVt_JxZBCG1FbvDf08Srg.png"/>
</p>

Although there are different versions of the Gent strain energy potentials, this article describes the strain energy function most commonly used in finite element method:

<p align="center">
  <img src="https://miro.medium.com/max/479/1*AGjzinUGrUM9M-rQjQAqtQ.png"/>
</p>

Where J is the volume ratio after and before deformation. For incompressible materials, J = 1. I1 is the first invariant of Cauchy strain tensor. u is the initial shear modulus, Jm is the limiting value of term I1–3, also known as the maximum average contour length, and D1 is the incompressible parameter that reflects the volume change. It can be seen from the strain energy function:

* The initial bulk modulus is K = 2 / D1.
* When the parameter Jm tends to infinity, the Gent model is equivalent to the neo-Hookean model. When the parameter Jm is not close to infinity, Gent can describe a more complex constitutive model curve in the stretched state than neo-Hookean.
* Under certain conditions, it is identical to the Arruda-Boyce model.

#### Advantages of the Gent model

* Simple and clear, with only three parameters. Two material parameters are the shear modulus for infinitesimal deformations and a parameter that measures a maximum allowable value of strain. Correspondingly, less experimental data is required.
* The parameters can be interpreted to the molecular properties of the polymer. This model features a locking stretch that reflects limiting chain extensibility at the molecular level.
* It can exhibit severe strain-stiffening in the stress response.


#### Limitations of the Gent model

* For small and medium deformations, especially moderate deformations (200–300% strain), the deviation is large.
* Like all other two-parameter models, it is unable to predict the whole range of strain.
* Can not predict the biaxial response of rubber if their parameters are determined with uniaxial data.


### Finite Element Analysis with Gent Material Model

Define materials

Select Gent hyperelastic material and input parameters u = 0.01 MPa, Jm = 10, D1 = 0.01 MPa^-1.

<p align="center">
  <img src="https://miro.medium.com/max/1273/1*cOppqhahOnbhu65xcBmFZA.png"/>
</p>

Import the rubber geometry, mesh it, and apply a downward displacement of -2 mm.

<p align="center">
  <img src="https://miro.medium.com/max/1274/1*uYyXrK8kHkbKHjeh-xortA.png"/>
</p>

Solve and add stress result objects to show the stress contour. As shown in the figure, the maximum stress value is non-linear with regards to time.

<p align="center">
  <img src="https://miro.medium.com/max/1274/1*x8k7xS-jYmGIXKHMTHixdQ.png"/>
</p>


