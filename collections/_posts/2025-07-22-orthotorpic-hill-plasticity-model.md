---
lang: en
layout: post
title:  "Orthotropic Hill Plasticity Model"
date:   2025-07-22
author: "[SimLet](https://twitter.com/getwelsim)"
---

In the field of structural mechanics, the plastic deformation processes of many materials are anisotropic in nature. Examples include composite materials, titanium alloys, additively manufactured structures, and multiscale materials. In these cases, traditional isotropic yield criteria are no longer sufficient to accurately describe the behavior, and appropriate models are required to characterize anisotropic plastic yielding. Commonly used anisotropic yield functions include the Hill, Barlat, Banabic, and Cazacu models. Among them, the Hill model was proposed relatively early and has a wide range of applications. It performs particularly well in describing orthotropic materials and is extensively used in structural finite element analysis.
<p align="center">
  <img src="\assets\blog\20250722\hill_augmented_manufacturing2.png" alt="hill_augmented_manufacturing" />
</p>


The Hill model is named after Professor R. Hill, who was appointed Professor of Applied Mathematics at the University of Nottingham in 1953. His 1950 work “The Mathematical Theory of Plasticity” laid the foundation for modern plasticity theory. He is widely regarded as one of the most significant contributors to solid mechanics in the second half of the 20th century.

It’s important to note that the Hill model is not the only yield criterion for orthotropic anisotropic materials. Alternatives include Barlat models with 3 or 6 parameters, or modified versions of the Hill yield criterion. This article focuses only on the classical Hill model, but similar approaches can be used to determine parameters for other yield models. The Hill model is applicable for analyzing plastic deformation in anisotropic materials and can be viewed as a generalized form of the von Mises yield criterion tailored for anisotropic behavior. It is particularly useful for orthotropic plastic materials in structural engineering applications.

The Hill yield criterion is given by:
<p align="center">
  <img src="\assets\blog\20250722\hill_yield_equation.png" alt="hill_yield_equation" />
</p>

For shell elements, the yield function is given by:
<p align="center">
  <img src="\assets\blog\20250722\hill_yield_equation4.png" alt="hill_yield_equation2" />
</p>

Where σ represents the stress components. For 3D models, F to H are six anisotropy calibration coefficients, also known as Hill parameters, which can be determined through material experiments. For shell elements, only four parameters F to N are required.

In computational mechanics, solid elements typically use yield stress ratios (or yield stresses) R11, R22, R33, R12, R13, R23 to calculate Hill parameters. To determine the yield stress ratios, the material’s yield stresses under different loading conditions must be measured:

* σ11, σ22, σ33 are obtained from tensile tests.
* σ12, σ13, σ23 are obtained from shear tests.

For shell elements, Lankford parameters are used to determine the Hill parameters. A Lankford parameter rₐ is defined as the ratio of plastic strain in the plane to that in the thickness direction. For orthotropic anisotropy, rₐ can be obtained from simple tensile tests:

* r₀₀: tensile direction aligned with the orthotropic axis 1.
* r₉₀: tensile direction perpendicular to the orthotropic axis 1.

Once r₀₀, r₄₅, r₉₀ are measured, the Hill parameters can be calculated. Higher Lankford values indicate better formability.

Most finite element analysis software requires the user to input either R values or Lankford parameters for the Hill model. Once these are specified, the Hill yield criterion equation can be fully determined.

## Support for the orthotropic Hill model in WelSim
The complexity of the Hill model lies in parameter input and solving the orthotropic nonlinear behavior. The general-purpose simulation software WESLIM supports transient analysis involving the Hill model. The free material editing software MatEditor supports Hill material model input. Currently, MatEditor supports three types of orthotropic Hill plastic material models and can generate OpenRadioss material input scripts: Law32, Law73/74, and Law93.
<p align="center">
  <img src="\assets\blog\20250722\mateditor_hill_orthotropic.png" alt="mateditor_hill_orthotropic" />
</p>


## Conclusion
The Hill model effectively describes orthotropic yield behavior, especially in tension-compression directions and in scenarios with minimal shear deformation. It can also be used to model the mechanical behavior of metallic lattice structures in additive manufacturing.

Hill parameters can be determined via R or Lankford parameters. When these parameters are unavailable from experiments, they can be approximated using curve fitting methods.

WelSim already provides support for the Hill model and can be integrated with OpenRadioss for transient simulations involving orthotorpic plastic deformation.


---
<small>
WelSim and authors have no direct affiliation with developers of OpenRadioss. References to OpenRadioss here are solely for technical blogging and software usage discussion.
</small>

