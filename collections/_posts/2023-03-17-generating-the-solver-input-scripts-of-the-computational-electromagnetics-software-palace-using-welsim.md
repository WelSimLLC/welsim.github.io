---
lang: en
layout: post
title:  "Generating the solver input scripts of the computational electromagnetics software Palace using WELSIM"
date:   2023-03-17
author: "[SimLet](https://twitter.com/getwelsim)"
---

On February 22, 2023, AWS released its open-source project Palace for large-scale parallel computing electromagnetics. Palace is used at the AWS Quantum Computing Center to perform large-scale 3D simulations of complex electromagnetic models and to support the design of quantum computing hardware. Currently, the entire source code of Palace is available on GitHub, and users can run the project on a variety of systems ranging from laptops to supercomputers. The accompanying Apache-2.0 open-source license is also extremely friendly to commercial applications.
<p align="center">
  <img src="\assets\blog\20230317\palace_github.png" alt="palace_github" />
</p>

The Palace solver is based on the MFEM library. WELSIM supports the input mesh format of MFEM since version R2.4. See the article “Generate MFEM initial mesh file using WELSIM”. On the basis of MFEM, Palace has improved more features and provided a variety of electromagnetic analysis types, including electrostatic, magnetostatic, eigenmode, frequency domain and time domain driven, and electromagnetic full-wave transient analyses. Various complex boundary conditions, such as waveguide ports, etc. are supported. Thanks to the scalability of open-source software, users can also expand the simulation functionalities on the basis of Palace.
<p align="center">
  <img src="\assets\blog\20230317\electrochip.png" alt="electrochip" />
</p>

Like most great open-source solvers, Palace currently has no easy-to-use graphical user interface. In order to better contribute to engineering simulation and open-source communities, WELSIM has recently supported the automatic generation of Palace solver input scripts, which makes WELSIM the world’s first pre-processor that fully supports Palace. Users can export the mesh and JSON format control files from WELSIM, which can be directly used in the computation of Palace. This greatly reduces the learning curve of Palace, so that users with different backgrounds can quickly use Palace to implement projects related to electromagnetics simulation.

## Generating Palace solver files

1. Setting Up Electromagnetic Analysis
Create a new project and set the project’s Physics Type to Electromagnetics. Select the required analysis type, as shown in the figure, Electromagnetics provides five analysis types: Electrostatic, Magnetostatic, Eigenmode, Driven, and Full-Wave Transient.
<p align="center">
  <img src="\assets\blog\20230317\welsim_project_em.png" alt="welsim_project_em" />
</p>


2. Add materials and electromagnetic properties
WELSIM contains an advanced material editing module, users can quickly add electromagnetic material properties and define relevant parameters. Currently, the supported Palace electromagnetic material properties are relative permittivity, relative permeability, conductivity, dielectric loss tangent, etc. The following figure shows the general material editing interface for electromagnetic properties.
<p align="center">
  <img src="\assets\blog\20230317\welsim_materials_em.png" alt="welsim_materials_em" />
</p>



3. Boundary conditions
In electromagnetic analysis, the boundary condition plays an important role in the overall modeling. WELSIM currently supports most boundary conditions of the Palace, including PEC, PMC, absorbing, conductivity, impedance, lumped port, waveguide port, surface current, ground, zero charges, etc.
<p align="center">
  <img src="\assets\blog\20230317\welsim_em_bcs.png" alt="welsim_em_bcs" />
</p>


4. Meshing
WELSIM provides fast automated meshing and supports Tet4/10 and Tri3/6 elements. After simply setting the size of the element, execute the mesh generation command to obtain the finite element mesh.
<p align="center">
  <img src="\assets\blog\20230317\welsim_mesh.png" alt="welsim_mesh" />
</p>



5. Export the solver files
After completing the above settings, in the Tools option of the menu bar, select Export Palace Scripts, then the output files can be obtained in the specified directory.
<p align="center">
  <img src="\assets\blog\20230317\welsim_palace_export.png" alt="welsim_palace_export" />
</p>


The generated Palace solver control file (JSON format) and mesh file are shown in the figure below.
<p align="center">
  <img src="\assets\blog\20230317\welsim_palace_exported_files.png" alt="welsim_palace_exported_files" />
</p>


At generating the Palace solver files, the program uses the corresponding mesh format according to the preference settings. The default mesh format is MFEM, and the user can modify it to the desired format in the preferences. Currently, supported mesh formats are Gmsh, MFEM, Nastran, VTK, and VTU formats.
<p align="center">
  <img src="\assets\blog\20230317\welsim_palace_mesh_format.png" alt="welsim_palace_mesh_format" />
</p>


Generating complex models for the Palace solver becomes quick and easy thanks to the ease of use of WELSIM. At present, the development version of WELSIM 2023R2 (v2.6) already contains these features, and it will be continuously maintained and enhanced in future versions.

---

<small>
WelSim and the author are not affiliated with Palace, AWS, or MFEM. Palace, AWS, and MFEM are used only as a nominative reference to the open-source project and software developed and released by these teams or institutions.
</small>

<small>
WelSim is an independent engineering simulation software provider, located in Greater Pittsburgh, PA. Its flagship product WESLIM is a general-purpose engineering simulation software with an all-in-one graphical user interface and self-integrated features.
</small>

