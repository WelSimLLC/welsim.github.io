---
lang: en
layout: post
title:  "Stress Analysis and Verification of Rectangular Plate with Circular Hole Using WELSIM"
date:   2018-01-01
author: "[SimLet](https://twitter.com/getwelsim)"
---

Plate structure with holes is widely applied in engineering practices. The reason making holes on the plate could vary, some for installing bolts and other connectors, and others for reducing weight without mainly affecting mechanical properties. Today we use finite element based simulation software WELSIM to analyze the plate subjected to tensile loading and verify the accuracy of the numerical solutions.

The geometric properties and loads of the plate are shown below. A rectangular plate structure with a fixed left side and a tensile pressure on the right side. There is a circular hole in the center of the plate.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*UAJHyqQBeminwTJWtC9d-w.png"/>
</p>

To better simulate the conditions and verify the correctness of the values, the following gives a specific structure size, force size, and material properties:

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*g1pCmbSWhxAoVeIggAtz6g.png"/>
</p>

Here the Poisson’s ratio is set to zero so that the force in one direction will not affect the deformation and stress in other directions. The purpose of doing this is to compare the numerical results with the theoretical results.

Open the software WELSIM below and set the material parameters. Create a new material node and add two properties of elastic modulus and Poisson’s ratio as shown in the figure:

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*_m2nuH22c8XwRlXwTqIXxg.png"/>
</p>

Since it is a plate structure, we can build the plate with holes by creating a plate and a cylinder and then using Boolean operations:

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*RPi7mw6WusgNg5hWNCYu0A.png"/>
</p>

And give the newly created plate the material we just defined, as shown:

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*3xYqTAV4f-YsDPMxs8Ah4A.png"/>
</p>

The next step is defining the mesh parameter and generating the grids. Since the stress around the hole is relatively concentrated, we set a relatively dense mesh around the hole. The meshed elements and nodes are given as follows. A total of 36796 nodes and 22927 tetrahedral elements are generated.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*OaovqPUkmXScfIE8mce6bw.png"/>
</p>

Next, add two boundary conditions, one displacement constraint is applied on the left surface, and one tensile pressure with the magnitude of 1e4 is imposed on the right surface.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*S00xZU0ou-MiQV-eRB-l-Q.png"/>
</p>

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*Ig7BxSvp3q27v3MLqKJrsA.png"/>
</p>

Now all analysis settings are defined. Click the Solve button, and the results will be available soon. After the calculation, add total displacement, and X normal stress result objects. Evaluate the result objects. The resulting contour looks like this:

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*UoQpzpaFbiPPI-5UqyyKIA.png"/>
</p>
<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*rJjCEdlOCWbiiXTOVwS2Ew.png"/>
</p>
<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*q0qHEdPfoCjkrSN787hIdA.png"/>
</p>

Next, we verify the results of X normal stress. The numerical results are very close to the theoretical values.
<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*BVpios3EZd-yianSbwmksw.png"/>
</p>

This simulation example is saved in the WELSIM software installation directory. Users can directly open the file named VM_WELSIM_002B.wsdb for calculation and verification.
