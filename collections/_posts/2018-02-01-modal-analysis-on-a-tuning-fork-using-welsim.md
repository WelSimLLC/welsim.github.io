---
lang: en
layout: post
title:  "Modal Analysis on a Tuning Fork using WELSIM"
date:   2018-02-01
author: "[SimLet](https://twitter.com/getwelsim)"
---

Modal analysis plays an important role in the structural analysis. Many essential components or entire machine designs need to avoid the natural frequencies to achieve the purpose of the safety operation. Some structures such as musical instruments require natural frequencies near a specific value. The general-purpose finite element software WELSIM also supports the modal analysis features. Today we use an intuitive example of a tuning fork to understand how to calculate the natural frequencies quickly and easily through WELSIM.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*gVVM3gW9oMGqTnrYM7xtYQ.jpeg"/>
</p>


First, import a tuning fork CAD model, as shown below.


<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*DLTu6bRZ4WSSuzj_H9LKTg.png"/>
</p>

Because it is a modal analysis, you need to change the default structure static analysis to modal analysis in the project properties. The GUI for property modification is shown in the figure:

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*CWtGQT-ZlLeeh9v3fYLc2g.png"/>
</p>

Set the grid parameters and click on the mesh to get the mesh with 19376 nodes and 9760 elements.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*e0gfKXnH7Kupe7YJNZvprw.png"/>
</p>

Add a fixed boundary condition to hold the bottom end of the tuning fork.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*5VI9sf4rlY5POlGsWoAWnQ.png"/>
</p>

Then you can click the Solve button, and you’ll be finished solving it soon. On a small simulation computer, it takes about 2 seconds. In the chart and tables windows, you can read the natural frequencies of the tuning fork under these conditions are 250.53, 251.55, 451.66, 1766.1, 2083.5, and 13011 Hz. According to the lowest frequency, we can estimate the pitch of this tuning fork close to note C. The figure below shows the deformation distribution of the structure at the first frequency.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*RGBj_LtAuPt1ggpOHA5WQA.png"/>
</p>

Is it very straightforward to conduct modal analysis in WELSIM? This example is saved in the WELSIM installation directory. Users can directly open the file named “structural_modal_v16_fork.wsdb” for calculation and verification.

