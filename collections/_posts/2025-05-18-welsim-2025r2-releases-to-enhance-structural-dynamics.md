---
lang: en
layout: post
title:  "WELSIM 2025R2 releases to enhance structural dynamics"
date:   2025-05-18
author: "[SimLet](https://twitter.com/getwelsim)"
---

The general-purpose engineering simulation software WELSIM has released the latest version 2025R2 (internal version number 3.1). Compared with the previous version, the 2025R2 version contains many new features and enhancements, which can better support various types of engineering analysis, especially structural dynamics.
<p align="center">
  <img src="\assets\blog\20250518\welsim_splash_2025r2.png" alt="welsim_splash_2025r2" />
</p>


## Enhanced support for OpenRadioss
The new version enhances the pre- and post-processing support for the OpenRadioss solver. By supporting the thermal stress commands, WelSim has the function of solving thermal stress problems. The reading and display of contact force results have been added. New functions such as remote displacement boundary conditions are supported as well.
<p align="center">
  <img src="\assets\blog\20250518\welsim_thermal_stress_openradioss.png" alt="welsim_thermal_stress_openradioss" />
</p>

In the material editing module, new material properties that can be applied to OpenRadioss have been added, such as damage plasticity (LAW23), brittle plasticity (LAW27), honeycomb structure (LAW28), Swift plasticity, Ramberg-Osgood plasticity, etc. The existing thermal expansion and specific heat material properties can output the solver command in OpenRadioss format. The independent material editing software MatEditor has also added the same function.


## Open source WelSim's documentation
All help documents of WelSim are open source now. This is another open source intelligent assets of WelSim after the official website and automated testing cases. Users can not only submit document updates about WelSim, but also use this framework to build online help documents for their own products. The documents are currently open source on GitHub at [GitHub](https://github.com/WelSimLLC/welsim-docs.github.io)
<p align="center">
  <img src="\assets\blog\20250518\welsim_docs_screen_capture.png" alt="welsim_docs_screen_capture" />
</p>


## Other enhancements and upgrades
In addition, the new version has other features and improvements. For example, it supports pre-processing of multi-layer shell structures. The application window title displays the full path name of the current project file. It supports dragging and dropping STEP geometry files. The CFD solver SU2 is upgraded to the latest version 8.2. And other enhancements and improvements.
<p align="center">
  <img src="\assets\blog\20250518\welsim_multilayer_shell_edit_layers.png" alt="welsim_multilayer_shell_edit_layers" />
</p>


---
<small>
WELSIM and the author are not affiliated with OpenRadioss, SU2. The use of OpenRadioss, SU2 is for reference in this technical blog post and software usage only.
</small>

