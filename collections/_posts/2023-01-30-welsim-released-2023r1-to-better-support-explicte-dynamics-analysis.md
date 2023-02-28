---
lang: en
layout: post
title:  "WELSIM releases 2023R1 to better support finite element analysis of complex structures"
date:   2023-01-30
author: "[SimLet](https://twitter.com/getwelsim)"
---


The general engineering simulation software WELSIM has released the latest version 2023R1 (internally v2.5). Compared with the previous version, the 2023R1 contains many new features and enhancements, which can better support the finite element analysis of complex structures, especially the analysis of explicit dynamics.

<p align="center">
  <img src="\assets\blog\20230130\welsim_splash.png" alt="welsim_release_25" />
</p>

## Exploded views of assemblies
For complex assemblies, 2023R1 adds the Exploded View feature. By enabling this option, users can quickly understand the internal structure of components in complex assemblies.
<p align="center">
  <img src="\assets\blog\20230130\welsim_exploded_view_icon.png" alt="welsim_exploded_view_icon" />
</p>

For complex assemblies with multiple structures inside, as shown in the figure below, now you can quickly understand the internal layout of the imported model.
<p align="center">
  <img src="\assets\blog\20230130\welsim_exploded_view2.png" alt="welsim_exploded_view2" />
</p>

In the preferences, there are also parameter settings for the exploded view, which are used to adjust the direction and scale of the explosion.
<p align="center">
  <img src="\assets\blog\20230130\welsim_exploded_view_preference.png" alt="welsim_exploded_view_preference" />
</p>

## Automatic contact search
The 2023R1 adds the automatic contact search function for the assemblies. Users no longer need to spend a lot of time and effort manually defining contact pairs, and the program can quickly detect potential contact pairs for complex models. This function can eliminate the cumbersome operations in contact surface selection.
<p align="center">
  <img src="\assets\blog\20230130\contact_search_menu.png" alt="contact_search_menu" />
</p>

## Supports for explicit dynamics and OpenRadioss
2023R1 sets the default solver for explicit dynamics to OpenRadioss. Users only need a simple configuration to directly call OpenRadioss to solve. For the configuration method, please refer to the article “[Run OpenRadioss solver for explicit dynamics analysis using WELSIM](/2023/01/04/run-openradioss-solver-for-explicit-dynamics-analysis-using-welsim.html)”. At present, OpenRadioss has been generally supported from the pre/post-processing aspects, and WELSIM will continue to enhance the OpenRadioss-related workflow in the next version 2023R2.

In addition, users can use WELSIM as an input script generator for the OpenRadioss solver. As shown in the figure below, using WELSIM to quickly generate solver input scripts greatly reduces the learning curve for OpenRadioss.
<p align="center">
  <img src="\assets\blog\20230130\welsim_export_openradioss.png" alt="welsim_export_openradioss" />
</p>

## Data persistence of mesh and results
This upgrade supports the data persistence of mesh and computation results. When the user opens the previously saved project files, if the saved project has successfully meshed or solved, and all project files are integrated, the user can quickly get the previous mesh and results without re-meshing or resolving. For large models, it effectively saves the user time and improves user experience.

## Enhancements and optimization
The software as a whole continues to be maintained and rapidly iterated. The overall optimized and improved software becomes more stable, accurate, and easier to use. In terms of third-party libraries, we upgrade NetGen to the latest version 6.2.2301, upgrade the front-end framework Qt to version 5.15.2, upgrade OpenCascade to version 7.5.3, upgrade the Windows C++ compiler to Visual Studio 2022 (v14.3), and upgrade Boost to version 1.80.


<small>
WelSim and the author are not affiliated with the OpenRadioss, NetGen, Opencascade, etc teams. OpenRadioss and others are used only as nominative references to the open-source project and software developed and released by their teams.
</small>

<small>
WelSimulation LLC is an independent engineering simulation technology provider, located in Greater Pittsburgh, PA. Its flagship product WESLIM is a general-purpose engineering simulation software with an all-in-one graphical user interface and self-integrated features.
</small>

