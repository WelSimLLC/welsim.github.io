---
lang: en
layout: post
title:  "WELSIM releases 2023R2, supporting open-source electromagnetic simulation solver"
date:   2023-04-05
author: "[SimLet](https://twitter.com/getwelsim)"
---


The general-purpose engineering simulation software WELSIM has released the latest version 2023R2 (internal version 2.6). Compared with the previous version, the 2023R2 version contains many new functions and enhancements, particularly supporting large-scale electromagnetic simulation and explicit dynamic analysis.
<p align="center">
  <img src="\assets\blog\20230405\welsim_splash.png" alt="welsim_splash_26" />
</p>

## Support Palace solver
The new version supports the automatic generation of the Palace solver input scripts, and is also the world’s first software that supports Palace pre-processing. Supported analysis types are: electrostatic, magnetostatic, eigenmode, driven, and full-wave transient analyses. The supported electromagnetic material properties are: relative permittivity, relative permeability, conductivity constant, dielectric loss tangent, etc.
<p align="center">
  <img src="\assets\blog\20230317\welsim_palace_export.png" alt="welsim_palace_export" />
</p>


Meanwhile, the supported boundary conditions are: perfect conductance surface, perfect magnetic conductance surface, absorbing boundary, conductance, impedance, lumped port, wave port, surface current, ground, zero charges, etc.
<p align="center">
  <img src="\assets\blog\20230317\welsim_em_bcs.png" alt="welsim_em_bcs" />
</p>


The generated grid file and JSON control file can be directly used for the Palace solver. For details, see the article "[Generating the solver input scripts of the computational electromagnetics software Palace using WELSIM](https://welsim.com/2023/03/17/generating-the-solver-input-scripts-of-the-computational-electromagnetics-software-palace-using-welsim.html)".

## Export mesh in Gmsh and Nastran formats
WELSIM supports the export of various types of meshes. This new version adds support for Gmsh and Nastran formats, both of which are widely used in the community. Users can choose to use these two formats when exporting the Palace solver scripts, or choose to use these two formats when exporting mesh data separately.
<p align="center">
  <img src="\assets\blog\20230405\welsim_mesh_export.png" alt="welsim_mesh_export" />
</p>


## Support rigid body settings for dynamic analysis
The new version supports the definition of rigid bodies in the GUI, especially in dynamic analysis, making it easy to define rigid bodies. The user only needs to set the geometry as a rigid body in the property window. Since rigid bodies are widely used in dynamic simulation and OpenRadioss, this function provides a convenient method for users to use WELSIM for explicit dynamic analysis. See "[Rigid body and dynamics in structural finite element analysis](https://welsim.com/2023/04/03/rigid-body-and-dynamics-in-structural-finite-element-analysis.html)" for details.
<p align="center">
  <img src="\assets\blog\20230403\welsim_define_rigid_body.png" alt="welsim_define_rigid_body" />
</p>


## Other enhancements and upgrades
The overall software continues to strengthen features and maintain rapid iteration. The new version optimizes many functions, making WELSIM more stable, accurate, and easier to use. For example, new functions such as opening recent files and spring boundary conditions have been added. In terms of the third-party library, the new version uses nlohmann/json as an additional JSON library, upgrades MFEM to version 4.5, upgrades Hypre to version 2.25, and upgrades FrontISTR to version 5.5.

---

<small>
WelSim and the author are not affiliated with Palace, OpenRadioss, Gmsh, or Nastran. These project names are used only as a nominative reference to the open-source project and software developed and released by these teams or institutions.
</small>
<small>
WelSim is an independent engineering simulation software provider, located in Greater Pittsburgh, PA. Its flagship product WESLIM is a general-purpose engineering simulation software with an all-in-one graphical user interface and self-integrated features.
</small>









