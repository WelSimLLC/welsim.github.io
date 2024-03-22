---
lang: en
layout: post
title:  "Generate CalculiX solver files using WELSIM"
date:   2024-03-19
author: "[SimLet](https://twitter.com/getwelsim)"
---


CalculiX is an outstanding general-purpose open-source finite element software based on the GPL open-source license, which can run on both Windows and Linux operating systems. The solver supports a variety of element types, analysis types, and also parallel processing. It can compute static, transient, fluid, thermal, and other models. Overall, CalculiX has excellent solving performance, and it has been widely used in academia and industry. The latest version is 2.21. The code for the program is all open-sourced, while also providing compiled executable programs and numerous examples.
<p align="center">
  <img src="\assets\blog\20240319\welsim_calculix_example_gallery.png" alt="welsim_calculix_example_gallery" />
</p>

CalculiX solver input files have a concise and clear format that is easy to learn, similar to Abaqus format. The file extension can be arbitrary, but `.inp` is commonly used. The input files can be a single file or divided into multiple files. The author prefers the input method of two files, one being a mesh file defining all mesh-related data; the other being a control command file containing material, load steps, parameters, etc.


In order to better support the open-source solver and simulation community, WELSIM recently added CalculiX preprocessing abilities. Users can quickly generate input files required for CalculiX computation. After defining the model, users can select the "Export CalculiX Scripts" option in the Tools menu bar to obtain solver files in the specified directory.
<p align="center">
  <img src="\assets\blog\20240319\welsim_calculix_export.png" alt="welsim_calculix_export" />
</p>


Upon successful export, two solver files will be generated, where the solver input script, `calculix_welsim.inp`, calls the mesh file named `mesh_abaqus.inp` using the *INCLUDE command.
<p align="center">
  <img src="\assets\blog\20240319\welsim_calculix_scripts.png" alt="welsim_calculix_scripts" />
</p>


Additionally, WELSIM can directly invoke CalculiX for computation. After downloading the CalculiX solver files, users can configure the path of the solver `ccx.exe` or `ccx_MT.exe` through Preferences -> Solver -> CalculiX executable file. After defining the model, users can directly solve it and obtain the result files.
<p align="center">
  <img src="\assets\blog\20240319\welsim_pereference_calculix.png" alt="welsim_pereference_calculix" />
</p>


Since CalculiX is not the default solver for WELSIM, when performing integrated analysis, the Solver property of the Analysis Settings object need to be set to CalculiX. CalculiX's load step settings are more flexible, so WELSIM provides more setting properties in each load step.
<p align="center">
  <img src="\assets\blog\20240319\welsim_solver_calculix.png" alt="welsim_solver_calculix" />
</p>

## Supported Commands
The latest version of CalculiX has a total of 141 commands. Currently, WELSIM already supports 60 commands, accounting for 42% of all commands, all of which are core commands and meet common analysis needs. Supported commands include:

**Control commands:**
* *AMPLITUDE
* *BEAM SECTION
* *CFD
* *COMPLEX FREQUENCY
* *DYNAMIC
* *ELECTROMAGNETICS
* *EL FILE
* *EL PRINT
* *END STEP
* *FREQUENCY
* *FRICTION
* *HEADING
* *HEAT TRANSFER
* *INCLUDE
* *NODE FILE
* *NODE PRINT
* *FLUID CONSTANTS
* *PHYSICAL CONSTANTS
* *REFINE MESH
* *RIGID BODY
* *STATIC
* *STEADY STATE DYNAMICS
* *STEP

**Contact, initial, and boundary conditions:**
* *BOUNDARY
* *CFLUX
* *CLOAD
* *CONSTRAINT
* *CONTACT PAIR
* *DFLUX
* *DLOAD
* *DSLOAD
* *FILM
* *INITIAL CONDITIONS
* *MASS FLOW
* *RADIATE

**Mesh commands:**
* *ELEMENT
* *ELSET
* *EQUATION
* *FLUID SECTION
* *MASS
* *NODE
* *NSET
* *SHELL SECTION
* *SOLID SECTION
* *SURFACE

**Material commands:**
* *CONDUCTIVITY
* *CREEP
* *CYCLIC HARDENING
* *DAMPING
* *DEFORMATION PLASTICITY
* *DENSITY
* *ELASTIC
* *ELECTRICAL CONDUCTIVITY
* *EXPANSION
* *HYPERELASTIC
* *MAGNETIC PERMEABILITY
* *MATERIAL
* *PLASTIC
* *RATE DEPENDENT
* *SPECIFIC GAS CONSTANT
* *SPECIFIC HEAT


## MatEditor outputs CalculiX scripts
Apart from WELSIM, the independent material editing software MatEditor also supports the export of CalculiX material data. Since Abaqus and CalculiX material commands are consistent, the exported material data text can be used for both CalculiX and Abaqus.
<p align="center">
  <img src="\assets\blog\20240319\welsim_mateditor_export_calculix.png" alt="welsim_mateditor_export_calculix" />
</p>


## Conclusion
This article introduces how to generate CalculiX input scripts using WELSIM and the settings for integrated analysis. Thanks to its excellent GUI, users can quickly generate high-quality CalculiX scripts.

Currently, WELSIM only supports Tet4, Tet10, Tri3, Tri6 elements, and the output CalculiX elements only support C3D4, C3D10, F3D4, DC3D4, DC3D10, S3, S6, B21, B32, T2D2, T3D3.

CalculiX is under the GPL open-source license, however the WELSIM installer package does not include the CalculiX solver. Users need to download the solver themselves. With simple configuration, WELSIM can be used to solve engineering problems in conjunction with CalculiX.

The functionality of CalculiX scripts has been introduced in WELSIM's 2024R2 development version. It will be continuously maintained and enhanced in official releases and future versions.

---

<small>
WELSIM and the author are not affiliated with CalculiX, or Abaqus. CalculiX and Abaqus are used only as a nominative reference to the open-source project and software developed and released by these teams or institutions.
</small>
