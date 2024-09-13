---
lang: en
layout: post
title:  "WELSIM releases the 2024R2, supporting more open-source solvers"
date:   2024-05-01
author: "[SimLet](https://twitter.com/getwelsim)"
---


The general-purpose engineering simulation software WELSIM has released its latest 2024R2 (internal version 2.9). Compared to its previous releases, the 2024R2 version contains many new features and enhancements, which can better support various types of engineering simulation analysis.
<p align="center">
  <img src="\assets\blog\20240501\welsim_splash.png" alt="welsim_splash" />
</p>


## Added support for CalculiX
The new 2024R2 version adds a pre-processing module for the CalculiX solver, allowing users to quickly generate input scripts required for CalculiX computation, or directly call CalculiX for solving through WELSIM.
<p align="center">
  <img src="\assets\blog\20240501\welsim_calculix_export.png" alt="welsim_calculix_export" />
</p>

Currently, 60 commands are supported, which accounts for 42% of all CalculiX commands. All of which are core commands, capable of common analysis needs.
<p align="center">
  <img src="\assets\blog\20240501\welsim_solver_calculix.png" alt="welsim_solver_calculix" />
</p> 


## Added support for Elmer FEM
The new version adds pre-processing support for Elmer FEM, allowing users to quickly generate input scripts required for Elmer FEM calculations. Upon successful export, a solver input script named elmer_welsim.sif will be generated, along with a mesh dataset consisting of four files named mesh.header, mesh.nodes, mesh.elements, and mesh.boundary.
<p align="center">
  <img src="\assets\blog\20240501\welsim_export_elmer_scripts.png" alt="welsim_export_elmer_scripts" />
</p>

Users can also directly call Elmer FEM for calculations through WELSIM. Currently supported Elmer equations include: Coil Solver, Fluidic Force, Free Surface Reduced, Heat Equation, MagnetoDynamics, Mesh Update, Navier-Stokes, Poisson BEM, Save Line, Save Scalars, Static Electrical Solver, Static Current Solver, Stress Analysis, Stream Solver, etc.
<p align="center">
  <img src="\assets\blog\20240501\welsim_solver_propperty_elmer.png" alt="welsim_solver_propperty_elmer" />
</p>


WELSIM introduced a new Additional Solver object to support users in adding various Elmer solver settings.

## Enhancements
To conclude, the 2024R2 version has new features and improvements, such as adding a search function to the solver output window, and supporting the import and export of csv format files for the table window. WELSIM has added a specific gas constant material property. Furthermore, the free material editing software MatEditor has added the feature to export material data in CalculiX and Elmer FEM formats.
<p align="center">
  <img src="\assets\blog\20240501\welsim_mateditor_export_elmer.png" alt="welsim_mateditor_export_elmer" />
</p>


The automatic testing system has become more user-friendly and contains more tests. WELSIM has created support for reading and saving of test group files *.wstb, and support for the deletion of selected test cases. WELSIM now also provides system-level operations, such as deleting local files and confirming specified files. In the new 2024R2 version, more than 200 test cases can be found and utilized.
<p align="center">
  <img src="\assets\blog\20240501\welsim_regression_system_playback_ui.png" alt="welsim_regression_system_playback_ui" />
</p>


---
<small>
WELSIM and the author are not affiliated with CalculiX and Elmer FEM. CalculiX and Elmer FEM is used only as a nominative reference to the open-source project and software developed and released by these teams or institutions.
</small>
