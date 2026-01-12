---
lang: en
layout: post
title:  "WELSIM 2026R1 Releases to Support Particle Generation and Enhance Electromagnetic Simulation"
date:   2026-01-05
author: "[SimLet](https://twitter.com/getwelsim)"
---

WELSIM, the general-purpose engineering simulation and analysis software, has released its latest version 2026R1 (Internal Version: 3.2). Compared to the previous version, 2026R1 comes with a host of new features and enhancements, enabling WELSIM to better support various types of engineering simulation CAE analyses, with notable improvements in particle and electromagnetic simulation capabilities.
<p align="center">
  <img src="\assets\blog\20260105\welsim_release_2026r1.png" alt="welsim_release_2026r1" />
</p>

## Support for Particle Generation
The new version introduces particle generation from geometric models, along with the ability to adjust particle generation methods and particle density. This feature simplifies the setup of smoothed particle and molecular dynamics simulations in WELSIM.
<p align="center">
  <img src="\assets\blog\20260105\welsim_sph_generate_particles_mesh_denser.png" alt="welsim_sph_generate_particles_mesh_denser" />
</p>

WELSIM is committed to supporting open data exchange, so users can also export particle data to VTK-format files for visualization or further analysis in other software tools.

## Enhanced Support for the OpenRadioss Solver
The latest version improves compatibility with the OpenRadioss solver, allowing WELSIM to generate more types of OpenRadioss input files. The newly added input cards include: Fabric Geometric Property /PROP/TYPE16, Self-contact /INTER/TYPE24, and the SPH Cell Command SPHCEL. Meanwhile, a wide range of new material properties have been incorporated, such as LAW6 (HYD_VISC), LAW24 (CONC), LAW25 (COMPSH), LAW58 (FABR_A), LAW73, and LAW74. MatEditor, the standalone material editing software, has been updated with the same features accordingly.
<p align="center">
  <img src="\assets\blog\20260105\mateditor_hill_orthotropic.png" alt="mateditor_hill_orthotropic" />
</p>

## Enhanced Support for Palace
The new version strengthens compatibility with Palace, the open-source electromagnetic solver. WELSIM now supports more Palace solver types and fully upgrades Palace and its dependent libraries to their latest versions. On the post-processing model, the Poynting Vector result type has been added.
<p align="center">
  <img src="\assets\blog\20260105\welsim_em_poynting_vector.png" alt="welsim_em_poynting_vector" />
</p>


## Other Enhancements and Upgrades
With this release, WELSIM is more stable and user-friendly through optimizations to existing features.

---

*Disclaimer: WELSIM and its authors are not affiliated with OpenRadioss or Palace, nor do they have any connection with the respective development teams and organizations. The references to OpenRadioss and Palace herein are solely for informational purposes in technical blog posts and software usage guidance.*
