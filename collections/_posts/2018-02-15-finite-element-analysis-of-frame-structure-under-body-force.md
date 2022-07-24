---
lang: en
layout: post
title:  "Finite Element Analysis of Frame Structure Under Body Force"
date:   2018-02-15
author: "[SimLet](https://twitter.com/getwelsim)"
---

The frame structure is widely used in engineering and often seen in large and medium-sized buildings such as stations, ports, and industrial and mining areas. This structure has the characteristics of large span and small load. In this article, we simulate this type of structure to reveal the deformation and stress under its body force using WELSIM.


### Physical model

The applications of frame structure can be seen on various occasions. The design of the frame, especially the stability of the structure are critical.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*ddgxB9mHnX006tOc92Vz0A.jpeg"/>
</p>

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*gk3F-Viyfy70dkn72nG-qw.jpeg"/>
</p>

The types are frame structure are also varied, and each design has its advantages. A schematic view of the frame structure designs is shown as follows:

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*Ku05B4uTjtwUUvDfDFeNPQ.jpeg"/>
</p>


### Finite Element Analysis Model
Now, we import the designed frame structure model from CAD software into WELSIM software and conduct the subsequent analysis.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*cc570v5rsCrONAKad57LhQ.png"/>
</p>

It can be seen that the imported geometry is a multi-body structure, as it is assumed here that welding or riveting make this structure, and the material is generally the same for bodies. We combine all bodies to eliminate the need for contact setup steps and save computing time. WELSIM provides the Boolean operation features. You can press the “Union” button from the toolbar or menu bar.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*HkCtaihB_QxSuelvdCzEXQ.png"/>
</p>

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*m2QVzUOBXl8GgscPHmpcZA.png"/>
</p>

As the structure is merged, you get a combined body as shown in the picture below. Here we assign the default structural steel material to the structure.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*zqp83Wb01dnvHD1wjqlg-A.png"/>
</p>

### Mesh
WELSIM provides an automatic meshing function. With a simple setting, you can quickly get the generated elements and nodes. Here we set to mesh the domain with the Tet10 element type. The results of meshing are as follows. There are 147,811 nodes and 78,081 tetrahedral elements.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*tVIUSvM6uYTCZdQkNstwYw.png"/>
</p>

### Boundary conditions and loads
In this analysis, we impose two fixed supports on the bottom.
<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*0oC6X23twysEZ_klOIx3Bg.png"/>
</p>
<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*ZQh02CSBygvG98D4CgBgeQ.png"/>
</p>

Next, we enter the body force that represents the weight of the frames. The body force is a force that acts on the entire structure. Such forces can be caused by the gravity, electric fields, and magnetic fields. The body force is not the same as the contact force or surface force exerted on the surface of an object. Some virtual forces, such as centrifugal force, Euler force and Coriolis effect, also belong to body force.

Like surface forces, the body force is also a directional vector force. It can be regarded as the product of the force density and mass. The formula is as follows:
<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*cNGubPxbhhHmUWpy0pLUaw.png"/>
</p>

WELSIM supports the body force input. Users can find the related buttons from the toolbar or menu bar as shown in the figure.
<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*bMYgVAD8Ltn3DpNmgo4X3g.png"/>
</p>
<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*3q9t0r0ByQmfRMbnc8A1qg.png"/>
</p>

In the graphic selection window, users can activate different selection modes including volume, surface, edge, and vertex selection.
<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*UVBfbWy6nTvmG4X2e2p5Bg.png"/>
</p>

Since the body force acts on the entire body, we activate the selection of the volume and select the geometries from the graphics window. Here we set the magnitude of the body force to 1e6 with the direction of -X.
<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*5V1W9XUBBX5x7bZtfJTi9A.png"/>
</p>

### Solution and Results
Click the Solve button, and you’ll be able to solve the model quickly. The maximum total deformation is 2.793e-3, and the maximum Von-Mises stress is 1.669e8.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*mKGT_jZTbiHkM2LaYYQsHw.png"/>
</p>
<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*d4sdko2APyd82cIfAaGH0w.png"/>
</p>

The result contours show the total deformation and the von-Mises stress of the given frame structure. Now user can clearly understand the deformation and stress status of the designs under the body force effects. You also can evaluate other analysis results such as strain, reaction force at the support positions.

Note: Body force feature is newly introduced to the version 1.7 of WELSIM.

