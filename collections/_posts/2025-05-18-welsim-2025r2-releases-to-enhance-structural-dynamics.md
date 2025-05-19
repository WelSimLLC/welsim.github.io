---
lang: en
layout: post
title:  "WELSIM 2025R2 releases to enhance structural dynamics"
date:   2025-05-18
author: "[SimLet](https://twitter.com/getwelsim)"
---

The general-purpose engineering simulation software WELSIM has released its latest version 2025R2 (internal version number 3.1). Compared with the previous one, version 2025R2 contains many new features and enhancements, which can better support various types of engineering analysis, especially structural dynamics.
<p align="center">
  <img src="\assets\blog\20250518\welsim_splash_2025r2.png" alt="welsim_splash_2025r2" />
</p>


## Enhanced support for OpenRadioss
The new version improves the pre- and post-processing support for the OpenRadioss solver. Through support of thermal stress commands, WelSim now has the ability to solving thermal stress problems. The reading and display of contact force results have also been added. More functions such as remote displacement boundary conditions have been implemented, too.
<p align="center">
  <img src="\assets\blog\20250518\welsim_thermal_stress_openradioss.png" alt="welsim_thermal_stress_openradioss" />
</p>

In the material editing module, new material properties applicable to OpenRadioss have been added, such as damage plasticity (LAW23), brittle plasticity (LAW27), honeycomb structure (LAW28), Swift plasticity, Ramberg-Osgood plasticity, etc. The existing thermal expansion and specific heat material properties can output the solver command in OpenRadioss format. The independent material editing software MatEditor has also added the same function.


## Open source WelSim's documentation
All help documents of WelSim are open source now. This is another open source intelligent asset of WelSim, after the official website and automated testing cases. Not only can users can submit document updates about WelSim, but they can also use this framework to build online help documents for their own products. The documents are currently open source on GitHub at [GitHub](https://github.com/WelSimLLC/welsim-docs.github.io)
<p align="center">
  <img src="\assets\blog\20250518\welsim_docs_screen_capture.png" alt="welsim_docs_screen_capture" />
</p>


## Other enhancements and upgrades
The new version has even more features and improvements. For one, WelSim now supports pre-processing of multi-layer shell structures. There have also been advancements to improve user experience: the application window title displays the full path name of the current project file, and users can now drag and drop STEP geometry files. Additionally, the CFD solver SU2 has been upgraded to the latest version 8.2. And other enhancements and upgrades.
<p align="center">
  <img src="\assets\blog\20250518\welsim_multilayer_shell_edit_layers.png" alt="welsim_multilayer_shell_edit_layers" />
</p>


---
<small>
WELSIM and the author are not affiliated with OpenRadioss, SU2. The use of OpenRadioss, SU2 is for reference in this technical blog post and software usage only.
</small>

