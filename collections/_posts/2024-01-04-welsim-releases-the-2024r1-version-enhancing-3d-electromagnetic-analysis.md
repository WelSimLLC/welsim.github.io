---
lang: en
layout: post
title:  "WELSIM releases the 2024R1 version, enhancing 3D electromagnetic analysis"
date:   2024-01-04
author: "[SimLet](https://twitter.com/getwelsim)"
---

The general engineering simulation analysis software WELSIM has released its latest 2024R1 version (internal version number 2.8). Compared to the previous version, the 2024R1 version has new added features to better support various types of engineering CAE analysis, especially calculations related to electromagnetics.
<p align="center">
  <img src="\assets\blog\20240104\welsim_splash.png" alt="welsim_splash" />
</p>


## Large-scale electromagnetic computation
On the basis of existing electrostatic and magnetostatic field analysis functions, 3D Eigenmode, Transient, and Driven analysis types have been added. At the same time, the electromagnetic field supports high-performance parallel computing. This widens WelSim's application scope and increases computational speed.

<p align="center">
  <img src="\assets\blog\20240104\welsim_em_analysis_type.png" alt="welsim_em_analysis_type" />
</p> 

A free compiled Windows-version of the open-source electromagnetic solver Palace is provided. Now, Palace users do not need to compile it themselves, and they can utilize Palace for large-scale electromagnetic field computation on Windows. This product can be obtained in the palace.exe executable file from the WELSIM installation package, or be downloaded it from the WelSim GitHub page.


## Support for importing GDSII geometric models
The geometric preprocessing module now supports the widely used GDSII format in the integrated circuit and chip industry. Users can apply WelSim to read GDS files, generate 2D solid models, and perform subsequent operations such as meshing and analysis calculations. Users can also directly export solid models to the well-established STEP format in the CAD industry.
<p align="center">
  <img src="\assets\blog\20240104\welsim_imported_gds_shapes.png" alt="welsim_imported_gds_shapes" />
</p>

## 3D layer selector
Additionally, the new version introduces a layer selector. When the mouse selects a position with multiple entity surfaces, a layer selector will appear at the bottom left corner of the 3D graphics window, allowing users to easily choose the inner surface of the geometric body or the obstructed surface. This feature enhances the preprocessing capability for three-dimensional fluid, electromagnetic, and complex assembly bodies.
<p align="center">
  <img src="\assets\blog\20240104\welsim_selection_layer_interior.png" alt="welsim_selection_layer_interior" />
</p>

## Linux version upgrade
The Linux version has been comprehensively upgraded to Ubuntu 22.04 LTS, with the compiler upgraded to GCC 11. All dependent libraries have been compiled and upgraded as well. This makes running WELSIM in the Linux environment much faster and more stable.
<p align="center">
  <img src="\assets\blog\20240104\welsim_v28_ubuntu2204.png" alt="welsim_v28_ubuntu2204" />
</p>

## Other enhancements
In addition, the WELSIM's new version includes other enhancements and optimizations, such as improved scale rulers for measuring microscale geometric bodies, the addition of the Metric unit system (kg, mm, ns, A, N, V) for high-frequency electromagnetic transient analysis, and other minor features.

WELSIM will continue to maintain rapid development and stable maintenance, contributing to the simulation community.


---

<small>
_WelSim is not affiliated with Palace, and the author has no direct relationship with the Palace development team and institution. The reference to Palace here is solely for technical blog articles and software usage._
</small>
