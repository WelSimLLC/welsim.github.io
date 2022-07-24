---
lang: en
layout: post
title:  "A Free Material Editing Tool - MatEditor"
date:   2019-06-25
author: "[SimLet](https://twitter.com/getwelsim)"
---

In engineering practices, we often deal with various materials. It is always important for engineers to accurately and quickly define materials and material properties. For example, as in the common finite element analysis, defining materials is one of the first steps. Due to the wide variety of materials, the material properties are also complex. However, there was no independent, easy-to-use material editing software. To resolve this situation, WELSIM releases a free material editing tool that can be used independently. This tool can help users quickly generate material data for engineering analysis.

<p align="center">
  <img src="https://miro.medium.com/max/1210/1*IFTjvHuEF2o6zH3gjnrcfg.png"/>
</p>

### Material Properties

Currently, the material editor supports 62 material properties, including:

Density
Isotropic Thermal Expansion
Isotropic Instantaneous Thermal Expansion
Orthotropic Thermal Expansion
Orthotropic Instantaneous Thermal Expansion
Constant Damping Coefficient
Isotropic Elasticity
Orthotropic Elasticity
Viscoelastic
Uniaxial Test Data
Biaxial Test Data
Shear Test Data
Volumetric Test Data
SimpleShear Test Data
Uniaxial Tension Test Data
Uniaxial Compression Test Data
Arruda-Boyce
Blatz-Ko
Gent
Mooney-Rivlin 2
Mooney-Rivlin 3
Mooney-Rivlin 5
Mooney-Rivlin 9
Neo-Hookean
Ogden 1stOrder
Ogden 2ndOrder
Ogden 3rdOrder
Polynomial 1st Order
Polynomial 2nd Order
Polynomial 3rd Order
Yeoh 1st Order
Yeoh 2nd Order
Yeoh 3rd Order
Bilinear Isotropic Hardening
Multilinear Isotropic Hardening
Bilinear Kinematic Hardening
Multilinear Kinematic Hardening
Anand Viscoplasticity
Strain Hardening
Time Hardening
Generalized Exponential
Generalized Graham
Generalized Blackburn
Modified Time Hardening
Modified Strain Hardening
Generalized Garofalo
Exponential Form
Norton
Combined Time Hardening
Rational Polynomial
Generalized Time Hardening
Strain Life Parameters
Compressive Ultimate Strength
Compressive Yield Strength
LaRc0304 Constants
Orthotropic Strain Limits
Orthotropic Stress Limits
Puck Constants
Tensile Ultimate Strength
Tensile Yield Strength
Tsai-Wu Constants
Prony Shear Relaxation
Prony Volumetric Relaxation
Shape Memory Effect
Drucker-Prager Strength Piecewise
Drucker-Prager Strength Linear
Ideal Gas EOS
Crushable Foam
Nonlinear Elastic Model Damage
Plakin Special Hardening
Tensile Pressure Failure
Crack Softening Failure
Enthalpy
Isotropic Thermal Conductivity
Orthotropic Thermal Conductivity
Specific Heat
B-H Curve
Isotropic Relative Permeability
Orthotropic Relative Permeability
Isotropic Resistivity
Orthotropic Resistivity

For ease of use, these 62 material properties are grouped into 9 categories: Basic, Linear Elastic, Hyperelastic Test Data, Hyperelastic, Plasticity, Creep, Visco-elastic, Thermal, and Electromagnetics.

<p align="center">
  <img src="https://miro.medium.com/max/264/1*YHYEvjqot0AfzHHrq4N0Sw.png"/>
</p>

### System Material Library

The software also comes with a default material library, containing 33 different materials at the latest version, users can directly select materials from the library. These materials include:

Structural Steel
Stainless Steel
Aluminum Alloy
Concrete
Copper Alloy
Gray Cast Iron
Titanium Alloy
Aluminum Alloy NL
Concrete NL
Copper Alloy NL
Stainless Steel NL
Structural Steel NL
Titanium Alloy NL
Elastomer Mooney-Rivlin
Elastomer Neo-Hookean
Elastomer Ogden
Elastomer Yeoh
Neoprene Rubber
Brass
Bronze
Copper
Diamond
Ferrite
Nodular Cast Iron
Solder
Teflon
Tungsten
Wood
SS416
Supermendure
Water Liquid
Argon
Ash

These materials are grouped into six groups: General Materials, Nonlinear Materials, Hyperelastic Materials, Thermal Materials, Electromagnetic Materials, and Other Materials.

<p align="center">
  <img src="https://miro.medium.com/max/271/1*zYTPJul58clYyxd0YHsuAw.png"/>
</p>

### Material Tree Window

The MatEditor supports editing multiple materials at the same time. When a material is created, a new object is generated in the tree window. A material object with bold font represents that the material is currently edited. The material object can be renamed by the user.

<p align="center">
  <img src="https://miro.medium.com/max/225/1*cRBIgfIosoYOH78ZuK32lQ.png"/>
</p>

Right-click on a material object to display a context menu, the available options include edit, duplicate, delete, and rename.

<p align="center">
  <img src="https://miro.medium.com/max/248/1*4fD_nz-MmN8mP7PQ0STA_Q.png"/>
</p>

### Material Property Window

The material properties window is the main window for editing materials. This window shows all the properties that have been added to the material. Users can add or modify property values, set units, suppress properties, or delete properties.

<p align="center">
  <img src="https://miro.medium.com/max/657/1*Nhe-1aLpZS-Ef6oAH1zFhw.png"/>
</p>

<p align="center">
  <img src="https://miro.medium.com/max/657/1*YnuxtyRwqTUEtYrL4x9QqQ.png"/>
</p>


### Table and Graph Windows

For many materials, you need to use the table to enter material property data. Such as the material properties based on temperature changes, it is necessary to give values for each critical temperature; For the hyperelastic and nonlinear material properties, it is necessary to display the stress-strain curve in order to verify whether the input parameters are reasonable. The graph window displays the corresponding curves based on the values entered in the table or properties window.

<p align="center">
  <img src="https://miro.medium.com/max/381/1*sqrruIse0Le2Fs7T0k6BGg.png"/>
</p>

<p align="center">
  <img src="https://miro.medium.com/max/1077/1*KCU6Vy7VXM0jRQfKHB5OZA.png"/>
</p>

At the same time, the table window supports other auxiliary functions. For example, the user can change the unit of quantity data, add, or delete rows of data.

<p align="center">
  <img src="https://miro.medium.com/max/501/1*cJG6xGL45RL46NN1tOcsbQ.png"/>
</p>

The graph window supports various drag, pan, and zoom operations.

<p align="center">
  <img src="https://miro.medium.com/max/530/1*Xbqs-VGdM7r7cUFe8uy8-g.png"/>
</p>

### Save and Export

The finished material data can be saved or exported by the user. These saved database files can be used in the future or consumed by other software. Currently, the supported file formats are WELSIM’s own material format and the generic MatML 3.1 format.

<p align="center">
  <img src="https://miro.medium.com/max/673/1*8JYak9izanb-Ft2QHNg9bQ.png"/>
</p>


### About

MatEditor’s information interface can display the software versions and local hardware information.

<p align="center">
  <img src="https://miro.medium.com/max/605/1*DgI8pdblcgf7pJa4Ilx9Nw.png"/>
</p>

Finally, MatEditor is a free lifetime material editing tool, you are welcome to use, and comment. The software can be downloaded directly from [https://welsim.com/mateditor](https://welsim.com/mateditor).





