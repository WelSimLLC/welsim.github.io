---
lang: en
layout: post
title:  "Generate FrontISTR mesh and input scripts using WelSim"
date:   2022-09-08
author: "[SimLet](https://twitter.com/getwelsim)"
---


FrontISTR is a well-known free and open-source finite element analysis software. Since 2005, when the Japanese Ministry of Education funded this project, it has been 17 years of development and maintenance history.

FrontISTR has versatile structural and thermal analysis features. These features such as structural contact problems, shell and beam engineering elements, and nonlinear material constitutive relations such as hyperelasticity, plasticity, viscoelasticity, etc. have been well supported. Nonlinear solver for thermal analysis is also supported. Compared with other open-source structural finite element software, FrontISTR's biggest advantage is that it supports large-scale cluster computing. While providing the source code, the FrontISTR team also shows the compiled Linux and Windows binary versions for the convenience of users. The software is open-source with the MIT license and thus is friendly to commercial developers and users.

<p align="center">
  <img src="\assets\blog\welsim_finite_element_thermal_exhaust_manifold.png" alt="welsim_frontistr_gui" />
</p>

The author began to pay attention to FrontISTR many years ago at the recommendation of a friend and found that its functions are powerful and the solving results are reliable. Friendly to engineering personnel, no software development work or experience is required. Although the development has been relatively slow in recent years, the maintenance of the program has not stopped. It is a set of structural finite element programs worth using and learning.

Although FrontISTR has great utility, for complex geometric models, like many other open source solvers, a preprocessor is required to generate meshes and input scripts. Due to FrontISTR's unique mesh and command format, input scripts for complex models require specialized software. FrontISTR officially provides its own free preprocessing tool REVOCAP PrePost, and the well-known open source CAD software FreeCAD also provides plug-in support for FrontISTR. In addition, WELSIM has excellent support for FrontISTR. Using WELSIM's efficient preprocessing GUI, users can quickly generate complex input scripts required for FrontISTR calculations.

In the actual use of WELSIM, only after the mesh is generated, the material and the boundary conditions are applied. Select the command **Export FrontISTR Input Script** from the menu to genereated the required mesh and input scripts.

<p align="center">
  <img src="\assets\blog\export_frontistr_script.png" alt="export_frontistr_script" />
</p>


At this point, in the specified folder, three ASCII files are generated. This is consistent with the regular input format of FrontISTR, and can be directly used in the FrontISTR program. At the same time, users can also make modifications based on this set of files to perform other analyses.

<p align="center">
  <img src="\assets\blog\frontistr_scripts.png" alt="frontistr_scripts" />
</p>


The control script and mesh file names are given by the hecmw_ctrl.dat file.

<p align="center">
  <img src="\assets\blog\demo_hecmw_ctrl_dat.png" alt="demo_hecmw_ctrl_dat" />
</p>



Alternatively, you can only use the generated mesh files, together with user-defined control scripts, to perform a highly customized simulation. The mesh file not only has node and element blocks but also defines element groups, which is convenient for users to assign different material properties to the geometry. The node and surface groups are supported as well for users to apply boundary conditions and contact pairs.

<p align="center">
  <img src="\assets\blog\demo_frontistr_mesh.png" alt="demo_frontistr_mesh" />
</p>


Due to the ease of use of WELSIM, generating complex models for the FrontISTR solver is quick and easy.

<small>
WelSim is not affiliated with the FrontISTR, REVOCAP, or FreeCAD team. FrontISTR, REVOCAP, and FreeCAD are used only as nominative references to the open-source project and software developed and released by the FrontISTR, REVOCAP, or FreeCAD team.
</small>

******

<small>
[WelSimulation LLC](https://welsim.com) is an independent engineering simulation technology provider, located in Greater Pittsburgh, PA. Its flagship product WESLIM is a general-purpose engineering simulation software with an all-in-one graphical user interface and self-integrated features.
</small>
