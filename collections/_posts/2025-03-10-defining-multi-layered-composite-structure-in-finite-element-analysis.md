---
lang: en
layout: post
title:  "Defining Multi-Layered Composite Structure in Finite Element Analysis"
date:   2025-03-10
author: "[SimLet](https://twitter.com/getwelsim)"
---


In modern structural analysis, multi-layer composite materials are often encountered. These composites frequently appear as a complete shell structure, made up of multiple layers stacked on top of each other. The angles, thicknesses, and materials of the layers may all vary. For the analysis of such composite materials, simulation software needs to provide relevant features, with users inputting data based on the actual materials.
<p align="center">
  <img src="\assets\blog\20250310\welsim_multilayer_composite.png" alt="welsim_multilayer_composite" />
</p>


The WELSIM composite parameter input provides a simplified method. This article introduces the steps to define composites.

1.Create a new FEM project.
2.Add two material objects, named Glass and Plastic Film, respectively.
<p align="center">
  <img src="\assets\blog\20250310\welsim_multilayer_shell_materials.png" alt="welsim_multilayer_shell_materials" />
</p>


3.Double-click the Glass material object to enter the editing mode. Enter the initial density of 2.5e-6 kg/mm³, Young's modulus of 70 GPa, Poisson's ratio of 0.2, plastic yield stress of 80 MPa, hardening parameter of 500 MPa, and hardening exponent of 0.8. Add Orthotropic Brittle Failure properties with the default parameters set to 0.
<p align="center">
  <img src="\assets\blog\20250310\welsim_multilayer_shell_mat_glass.png" alt="welsim_multilayer_shell_mat_glass" />
</p>


4. Double-click the Plastic Film material object to enter the editing mode. Enter the initial density of 2.5e-6 kg/mm³, Young's modulus of 100 MPa, Poisson's ratio of 0.2, plastic yield stress of 10 MPa, hardening parameter of 20 MPa, and hardening exponent of 0.5. Add orthotropic brittle failure properties with strain at the beginning of tensile failure set to 0.6, maximum tensile strain set to 0.7, and the maximum tensile strain for element deletion set to 0.8.
<p align="center">
  <img src="\assets\blog\20250310\welsim_multilayer_shell_mat_plastic_film.png" alt="welsim_multilayer_shell_mat_plastic_film" />
</p>


5. Add a plane shape to represent the shell structure. Users can also import a real shell structure. In the properties window, set the Structural Type to Multi-Layer Shell structure.
<p align="center">
  <img src="\assets\blog\20250310\welsim_multilayer_shell_shape_type.png" alt="welsim_multilayer_shell_shape_type" />
</p>



6. Once the Structural Type is set to Multi-Layer Shell, the table window is activated to edit layer data. This allows users to define the number of layers, angle, thickness, Z position, and materials for each layer. Here, a total of three layers are defined, with thicknesses of 1 mm, 0.5 mm, and 1 mm, and materials of Glass, Plastic Film, and Glass, respectively.
<p align="center">
  <img src="\assets\blog\20250310\welsim_multilayer_shell_edit_layers.png" alt="welsim_multilayer_shell_edit_layers" />
</p>


7. At this point, the multi-layer shell structure is defined and ready for subsequent analysis and computation. For example, an OpenRadioss input script can be generated to view the input layer data. As shown in the picture below, the material information and multi-layer shell structure properties are fully defined for solver.
<p align="center">
  <img src="\assets\blog\20250310\welsim_multilayer_shell_radioss_script_mat.png" alt="welsim_multilayer_shell_radioss_script_mat" />
</p>
<p align="center">
  <img src="\assets\blog\20250310\welsim_multilayer_shell_radioss_script_prop.png" alt="welsim_multilayer_shell_radioss_script_prop" />
</p>


## Conclusion
This blog  demonstrates the definition of a multi-layer shell structure and the associated material properties. This is the first step in composite material analysis. WELSIM makes it easy and quick to define multi-layer structures. This feature has been implemented in the 2025R2 development version and will continue to be optimized in future versions.

---
<small>
WelSim and author are not directly related to the OpenRadioss development team and institution. The reference to OpenRadioss is only used here for technical blog and software usage references.
</small>

