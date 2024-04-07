---
lang: en
layout: post
title:  "Generate Elmer FEM solver scripts using WELSIM"
date:   2024-04-06
author: "[SimLet](https://twitter.com/getwelsim)"
---


Elmer FEM is an excellent open-source finite element software for general-purpose multi-physics simulations. It is developed through collaboration between CSC, Finnish universities, research laboratories, and the industry. The Elmer solver is based on the GPL open-source license and is capable of computing various physical models including fluid dynamics, structural mechanics, electromagnetics, heat transfer, and acoustics. It can run on both Windows and Linux operating systems and has been widely used in academic and industrial settings. The latest version is 9.0, and the official release includes all the source code along with extensive examples and documentation. Installation packages are also provided for easy setup.
<p align="center">
  <img src="\assets\blog\20240405\welsim_elmer_logo.png" alt="welsim_elmer_logo" />
</p>


Elmer FEM solver files have a relatively independent format, which is concise and easy to learn. These files typically consist of a single file with the extension *.sif. Mesh data is composed of four additional mesh files.

To better support the open-source and simulation community, WELSIM recently added support for pre-processing Elmer FEM, allowing users to quickly generate input scripts required for Elmer FEM computation. After defining the model, users can select the option to output Elmer FEM files from the Tools menu, resulting in solver files in the specified directory.
<p align="center">
  <img src="\assets\blog\20240405\welsim_export_elmer_scripts.png" alt="welsim_export_elmer_scripts" />
</p>


Upon successful export, a solver input script named elmer_welsim.sif is generated along with four mesh files named mesh.header, mesh.nodes, mesh.elements, and mesh.boundary.
<p align="center">
  <img src="\assets\blog\20240405\welsim_elmer_generated_scripts.png" alt="welsim_elmer_generated_scripts" />
</p>


Additionally, WELSIM can directly invoke Elmer FEM for computation. After downloading Elmer FEM solver files, users can configure the path to the solver directory through Preferences -> Solver -> Elmer FEM executable file. This enables direct invocation of Elmer FEM to solve the model and obtain result files.
<p align="center">
  <img src="\assets\blog\20240405\welsim_preferences_elmer.png" alt="welsim_preferences_elmer" />
</p>


Since Elmer FEM is not the default solver, when performing the connected computing, the solver property of the Study Settings object needs to be set to Elmer FEM. Considering the various equation types within Elmer FEM, additional Elmer Equation property is provided to specify specific computational formulas. Currently, Elmer Equation options support common formulas such as Coil Solver, Fluidic Force, Free Surface Reduced, Heat Equation, MagnetoDynamics, Mesh Update, Navier-Stokes, Poisson BEM, Save Line, Save Scalars, Static Electrical Solver, Static Current Solver, Stress Analysis, Stream Solver, etc.
<p align="center">
  <img src="\assets\blog\20240405\welsim_solver_propperty_elmer.png" alt="welsim_solver_propperty_elmer" />
</p>


Elmer FEM supports multiple different types of solvers within a single analysis. To support this feature, a new Additional Solver object is introduced, allowing users to add an unlimited number of solver settings. The properties of the Additional Solver node are similar to the solver settings in Study Settings.


## MatEditor outputs Elmer scripts
In addition to WELSIM, the standalone material editing software MatEditor also supports the export of Elmer FEM material data. The generated material data can be directly used in Elmer solver input files.
<p align="center">
  <img src="\assets\blog\20240405\welsim_mateditor_export_elmer.png" alt="welsim_mateditor_export_elmer" />
</p>



## Conclusion
This article introduces the generation of Elmer FEM solver scripts using WELSIM and the setup for combined simulations. Thanks to its excellent GUI, users can quickly generate high-quality Elmer FEM files.

Currently, WELSIM only supports Tet4, Tet10, Tri3, and Tri6 elements and does not support multi-domain mesh with shared boundaries.

Elmer FEM is distributed under the GPL open-source license, and the installer of WELSIM does not include the Elmer FEM solver. Users need to download and install the solver themselves. With simple configuration, WELSIM can be used for calling Elmer FEM to run the generated scripts.

The functionality of Elmer FEM input files has been developed in the 2024R2 beta version and will be continuously maintained and enhanced in subsequent versions. For support of other open-source solvers, references can be made to articles such as "Generating CalculiX Solver Files with WELSIM", "Generating SU2 Solver Files with WELSIM", "Using WELSIM to Invoke OpenRadioss for Explicit Dynamics Analysis", "Generating FrontISTR Mesh and Input Files with WELSIM", "Generating Initial Mesh Files for MFEM with WELSIM", and "Generating Solver Files for Electromagnetic Calculation Software Palace with WELSIM".


---

<small>
WELSIM and the author are not affiliated with Elmer FEM. Elmer FEM is used only as a nominative reference to the open-source project and software developed and released by these teams or institutions.
</small>
