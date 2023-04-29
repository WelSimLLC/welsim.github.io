---
lang: en
layout: post
title:  "Multi-step and time-varying settings in dynamics simulation"
date:   2023-04-28
author: "[SimLet](https://twitter.com/getwelsim)"
---

Nowadays, it is often necessary to set multi-step conditions and time-varying boundary conditions in modeling real engineering problems. These requirements bring challenges to the simulation software. Not only the solver needs to support multiple steps, but also the graphical user interface should provide convenient and easy input methods. WELSIM supports the multi-step analysis as early as 2019. For details, please refer to the article “[Multi-step quasi-static structural finite element analysis](https://welsim.com/2019/07/17/multi-step-quasi-static-structural-finite-element-analysis.html)”. Recently, with the support of the explicit dynamic analysis software OpenRadioss, the multi-step related features have also gained more attention. This article discusses the multi-step and time-varying boundary condition features in WELSIM with a true engineering example.
<p align="center">
  <img src="\assets\blog\20230428\engineers_with_computer.jpg" alt="engineers_with_computer" />
</p>


Among the multi-step models, metal sheet forming has both die-casting and separation steps, which is a typical and common multi-step working case. The model is shown in the figure below. When the punch is pressed down, the sheet metal is bent under force, resulting in plastic deformation. Then the punch and holder spring back and separate from the deformed sheet. In this example, molds and fixtures are rigid bodies, and the sheet metal part is an elastic-plastic body. All shapes are meshed as shell elements.
<p align="center">
  <img src="\assets\blog\20230428\welsim_spring_back_exploded_view.png" alt="welsim_spring_back_exploded_view" />
</p>


## Multi-steps and time settings
When meshing is completed and the contact pairs are defined, it is necessary to perform multi-step settings for the analysis. Increase the number of steps as needed, set the time for each step, and define the number of substeps for iterations. Here we set the model to a total of 5 steps. The total number of sub-steps is 1000, then 1000 result files will be generated.
<p align="center">
  <img src="\assets\blog\20230428\welsim_multistep_study_settings.png" alt="welsim_multistep_study_settings" />
</p>

After setting the time, the user can double-click the Study Settings object to display a list of quantities at each step, as shown in the figure below. The time of each step here is 0.3, 0.5, 0.9, 1, and 1.2 seconds respectively. Users can check whether the time is set properly. When the checking is complete, you can click the red delete button on the tab to close the view.
<p align="center">
  <img src="\assets\blog\20230428\welsim_multistep_study_settings_spreadsheet.png" alt="welsim_multistep_study_settings_spreadsheet" />
</p>



## Add time-varying boundary conditions
In this model, the boundary conditions that vary with load steps (time) are forces and velocities. Users need to first set the properties of these boundary conditions as Tabular, and then assign table data. As shown in the figure below, change the property data type in the lower left area. The table on the right lists the velocity values for each step, and the user can edit the specific values. The Chart window at the bottom shows velocity over time for better visualization.
<p align="center">
  <img src="\assets\blog\20230428\welsim_multistep_bc_tabular_notes.png" alt="welsim_multistep_bc_tabular_notes" />
</p>


The time of each step is uniform and fixed, and cannot be changed in the current boundary conditions. When changing the time is needed, you can modify it in the properties of Study Settings.

So far, the setting of the multi-step analysis is completed.

If you generate the OpenRadioss solver scripts for this model, it can be seen that the setting of multi-steps and velocity values are accurately expressed in the input scripts, as shown in the picture below.
<p align="center">
  <img src="\assets\blog\20230428\welsim_multistep_bc_openradioss.png" alt="welsim_multistep_bc_openradioss" />
</p>


Obviously, it is very easy to define multi-steps and time-varying boundary conditions in WELSIM, and generate relevant OpenRadioss solver scripts.

The result animation of the given analysis is shown below.
[![metal_sheet_forming](https://img.youtube.com/vi/MyIbjrKB6is/0.jpg)](https://youtu.be/MyIbjrKB6is)

WELSIM has supported multi-step features since 2019. The multi-step OpenRadioss solver script has been added in the 2023R3 development release. The features related to multi-steps will be continuously enhanced in future versions.

---

<small>
WelSim and the author are not affiliated with OpenRadioss. OpenRadioss is used only as a nominative reference to the open-source project and software developed and released by these teams or institutions.
</small>

<small>
WelSim is an independent engineering simulation software provider, located in Greater Pittsburgh, PA. Its flagship product WESLIM is a general-purpose engineering simulation software with an all-in-one graphical user interface and self-integrated features.
</small>

