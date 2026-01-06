---
lang: en
layout: post
title:  "WELSIM 2026R1 Releases to Support Particle Generation and Enhance Electromagnetic Simulation"
date:   2026-01-05
author: "[SimLet](https://twitter.com/getwelsim)"
---

WELSIM, the general-purpose engineering simulation and analysis software, has released its latest version 2026R1 (Internal Version: 3.2). Compared with the previous version, 2026R1 comes with a host of new features and enhancements, enabling it to better support various types of engineering simulation CAE analyses, with particular improvements in particle and electromagnetic simulation capabilities.
<p align="center">
  <img src="\assets\blog\20260105\welsim_release_2026r1.png" alt="welsim_release_2026r1" />
</p>

## Support for Particle Generation
The new version adds the functionality to generate particles from geometric models, along with the ability to adjust particle generation methods and particle density. This feature simplifies the setup of smoothed particle and molecular dynamics simulations in WELSIM.
<p align="center">
  <img src="\assets\blog\20260105\welsim_sph_generate_particles_mesh_denser.png" alt="welsim_sph_generate_particles_mesh_denser" />
</p>

WELSIM has always been committed to supporting open data exchange. Users can also export particle data to VTK-format files for visualization or further analysis in other software tools.

## Enhanced Support for the OpenRadioss Solver
The new version expands its support for the OpenRadioss solver, allowing WELSIM to generate more types of OpenRadioss input files. The newly added input cards include: Fabric Geometric Property /PROP/TYPE16, Self-contact /INTER/TYPE24, and the SPH Cell Command SPHCEL. Meanwhile, a wide range of new material properties have been incorporated, such as LAW6 (HYD_VISC), LAW24 (CONC), LAW25 (COMPSH), LAW58 (FABR_A), LAW73, and LAW74. MatEditor, the standalone material editing software, has been updated with the same new features accordingly.
<p align="center">
  <img src="\assets\blog\20260105\mateditor_hill_orthotropic.png" alt="mateditor_hill_orthotropic" />
</p>

## Enhanced Support for Palace
The new version strengthens its support for Palace, the open-source electromagnetic solver. It now supports more Palace solver types, and fully upgrades Palace and its dependent libraries to their latest versions. On the post-processing model, the Poynting Vector result type has been added.
<p align="center">
  <img src="\assets\blog\20260105\welsim_em_poynting_vector.png" alt="welsim_em_poynting_vector" />
</p>


## Other Enhancements and Upgrades
In addition, the new version has optimized and upgraded existing features, making WELSIM more stable and user-friendly.

---

*Disclaimer: WELSIM and its authors are not affiliated with OpenRadioss or Palace, nor do they have any connection with the respective development teams and organizations. The references to OpenRadioss and Palace herein are solely for informational purposes in technical blog posts and software usage guidance.*





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
All help documents of WelSim are open source now. This is another open source intelligent asset of WelSim, after the official website and automated testing cases. Not only can users can submit document updates about WelSim, but they can also use this framework to build online help documents for their own products. The documents are currently open source on GitHub at [https://github.com/WelSimLLC/welsim-docs.github.io](https://github.com/WelSimLLC/welsim-docs.github.io)
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

