---
lang: en
layout: post
title:  "Multi-step transient analysis of hyperelastic bushing"
date:   2025-02-25
author: "[SimLet](https://twitter.com/getwelsim)"
---


In transient analysis, the multi-step setting is often required. This article will demonstrate how to use WELSIM for multi-step transient finite element analysis of hyper-elastic materials.

1.Start the WELSIM software, click on Preferences, and set the current unit system to kg-mm-s.
<p align="center">
  <img src="\assets\blog\20250225\welsim_bushing_units.png" alt="welsim_bushing_units" />
</p>

2.Create a new finite element analysis (FEA) project.

3.Add a new material object and name it Rubber42. Double-click this material object to enter editing mode. Add density and 2nd-order Odgen hyperelastic material properties. Set the density to 6e-6 kg/mm3. Set the Odgen2 material parameters as follows: Mu1 = 600,000 kPa, A1 = 2, Mu2 = 0, A2 = -2. The corresponding stress-strain curve will be displayed in the Chart window.
<p align="center">
  <img src="\assets\blog\20250225\welsim_bushing_materials.png" alt="welsim_bushing_materials" />
</p>

4.After editing the material, close the material edit window. Click on the FEM Project object and set the properties to Explicit Transient Structural Analysis.
<p align="center">
  <img src="\assets\blog\20250225\welsim_bushing_project_properties.png" alt="welsim_bushing_project_properties" />
</p>


5.Import the pre-prepared bushing geometry model (bushing3d.step) and assign the newly created hyperelastic material Rubber42 to it.
<p align="center">
  <img src="\assets\blog\20250225\welsim_bushing_shapes.png" alt="welsim_bushing_shapes" />
</p>


6.Click on the mesh settings object, set the Maximum Size to 10mm, and click the mesh generation button. Quickly, the mesh will be automatically generated.
<p align="center">
  <img src="\assets\blog\20250225\welsim_bushing_solution.png" alt="welsim_bushing_solution" />
</p>



7.Click on the Study Settings object. In the properties window, set the load steps to 3. Set the time for each load step to 0.0005s, 0.001s, and 0.0015s respectively. Set the time step to 1e-5s.
<p align="center">
  <img src="\assets\blog\20250225\welsim_bushing_study_settings.png" alt="welsim_bushing_study_settings" />
</p>

Double-click the Study Settings object to see the time settings for each load step in the new window.
<p align="center">
  <img src="\assets\blog\20250225\welsim_bushing_study_settings_spreadsheet.png" alt="welsim_bushing_study_settings_spreadsheet" />
</p>


8.After defining the Study Settings, start adding boundary conditions. First, add a fixed boundary condition, and choose the outer boundary of the bushing as the fixed boundary.
<p align="center">
  <img src="\assets\blog\20250225\welsim_bushing_bc_fixed.png" alt="welsim_bushing_bc_fixed" />
</p>


9.Then, add a Remote Displacement boundary condition, and choose the inner boundary of the bushing to apply the boundary. Since this is a multi-step analysis, displacement values for each step need to be defined in a table. In this example, the displacement in the Y and Z directions and the rotation about the Z-axis are set in the table. The displacement values in the Y direction are 10, 10, and 10. The displacement values in the Z direction are 0, 5, and 5. The rotation about the Z-axis is 0, 0, and 20 degrees.
<p align="center">
  <img src="\assets\blog\20250225\welsim_bushing_bc_remote_displacement.png" alt="welsim_bushing_bc_remote_displacement" />
</p>



10.After defining these analysis settings, simply click the Solve button to call the solver for computation. (Users need to connect to the external solver OpenRadioss in Preferences). When the calculation is completed, click on the Answers object, where you can view various time-dependent variables, such as energy, mass, momentum, etc., in the Table and Chart windows.
<p align="center">
  <img src="\assets\blog\20250225\welsim_bushing_solution.png" alt="welsim_bushing_solution" />
</p>



11.Add the stress results and evaluate them.
<p align="center">
  <img src="\assets\blog\20250225\welsim_bushing_result_stress.png" alt="welsim_bushing_result_stress" />
</p>


12.Add the displacement results and evaluate them.
<p align="center">
  <img src="\assets\blog\20250225\welsim_bushing_result_displacement.png" alt="welsim_bushing_result_displacement" />
</p>


13.Users can also add other results, such as strain, velocity, acceleration, etc.

14.If you need to generate an animation video file, you can click on the camera icon in the Chart window to create an animation video of the current result object.
<p align="center">
  <img src="\assets\blog\20250225\welsim_bushing_save_video.png" alt="welsim_bushing_save_video" />
</p>


This example demonstrates how to perform multi-step transient analysis using WELSIM. The model has been saved in the automated test example (file name: 12010_or_bushing_multistep.xml). Note that users need to configure the OpenRadioss path in Preferences for the first time running.


---
<small>
WelSim and author are not directly related to the OpenRadioss development team and institution. The reference to OpenRadioss is only used here for technical blog and software usage references.
</small>

