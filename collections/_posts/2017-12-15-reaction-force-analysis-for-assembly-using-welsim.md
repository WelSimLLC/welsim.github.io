---
lang: en
layout: post
title:  "Reaction Force Analysis for Assembly Using WELSIM"
date:   2017-12-15
author: "[SimLet](https://twitter.com/getwelsim)"
---

In structural mechanics analysis, we are often interested in the reaction of the structure at the fixed end, in addition to the conventional displacement, stress, and strain results. Understanding the fixed-side reaction force plays a very important role in the selection of fixtures in the engineering practices. The common reaction types in the structure are reaction force and reaction moment.

Today we use the engineering simulation software WELSIM to analyze the reaction forces of the assembly. A cylindrical structure is fixed at both ends, and two positions in the middle part are subjected to concentrated forces. The problem is described as follows:

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*lLB4e4DbHGrIzVAsblsQLg.png"/>
</p>

In order to better simulate the conditions and verify the results, the following table gives a specific geometric dimensions, loads, and material properties:

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*F6Gy_83RXugZpNoyhg9YbQ.png"/>
</p>

The following opens the simulation software WELSIM, sets up the material parameters, establishes the geometrical model. Since this structure is assembled from three sub-structures, we also need to set up two face contact pairs and bond three sub-bodies together.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*iPhynSws0HRR0uuL3BI9Ww.jpeg"/>
</p>

Define the boundary conditions, which are the full fixed constraints of the top and bottom, and the two concentrated forces in the middle as shown in the figure blow.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*zqYKAFjZP1XpnZx0jEK05Q.jpeg"/>
</p>

In order to obtain a more accurate reaction force, we need to define a high mesh density. Here we set the maximum element size to 0.1. After meshing, The grid with 190,595 nodes and 128,189 tetrahedral elements are generated.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*PJjgljIPOBz5YbJyBLr63Q.jpeg"/>
</p>

Click the Solve button and the calculation will be completed in a few minutes. Next add deformation, stress, and reaction forces, respectively, to see the computational results.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*YxK4mZt2204yXFRq9PQuiQ.jpeg"/>
</p>

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*OGUgarboiJgJc0z-M-uvXA.jpeg"/>
</p>

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*OzBwet5Dafu_UG1uydnIpg.jpeg"/>
</p>

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*pSsoOusSNdHDgT2ZSmOE8Q.jpeg"/>
</p>

We can compare the results of the reaction forces with the theory, and the results are very close to the theoretical ones.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*Dsf667jQIAfvn482N4byEw.png"/>
</p>

This example is also distributed with the WELSIM software. Users can directly open the file named VM_WELSIM_001B.wsdb from the installation directory for calculation and verification.


