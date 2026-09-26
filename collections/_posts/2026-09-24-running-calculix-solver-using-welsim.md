---
lang: en
layout: post
title:  "Running CalculiX solver using WELSIM"
date:   2026-09-24
author: "[SimLet](https://twitter.com/getwelsim)"
---

CalculiX is a classic open-source, general-purpose finite element solver licensed under the GPL. It supports linear and nonlinear static, dynamic, thermal, and contact analyses, and is natively compatible with the Abaqus INP input file format. From university research to small-to-medium-sized enterprise simulations, CalculiX is widely used.


As a general-purpose CAE pre and post-processing software, WELSIM features native pre-processing support for CalculiX: users can either export CalculiX INP input scripts for offline calculation with a single click, or directly call the CalculiX solver within the WELSIM graphical user interface to complete computations, streamlining the workflow of "CAD import -> mesh -> material -> boundary conditions -> solving."

This article outlines the steps for co-solving finite element models utilizing both software applications under the Windows operating system.

## Software Preparation
Download and install the latest version of WELSIM; this blog's example uses the 2026R3 development version.
<p align="center">
  <img src="\assets\blog\20260924\welsim_calculix_github_download.png" alt="welsim_calculix_github_download" />
</p>


The CalculiX solver can be downloaded as a pre-compiled package from the official website (www.calculix.de) or GitHub. After extraction, you will find the solver executable files in the bin folder: ccx.exe (serial) and ccx_MT.exe (multi-threaded parallel version). Users do not need to modify any of the extracted CalculiX files. Please avoid placing the CalculiX folder on the system drive (such as the C drive) and refrain from having an excessively long absolute folder path.

## Path Configuration
When executing the CalculiX solver via WELSIM for the first time, you need to briefly configure the CalculiX path. The steps are as follows:
1.Open the WELSIM software, and click Preferences in the menu or toolbar.
<p align="center">
  <img src="\assets\blog\20260924\welsim_calculix_preferences.png" alt="welsim_calculix_preferences" />
</p>

2.Locate the Solvers tab in the left-hand list.

3.Find the CalculiX file field on the right, click Browse, and select the extracted ccx_MT.exe or ccx.exe. On Windows, an example path could be: D:\WelSimLLC\executable34\CalculiX-2.23.0-win-x64\bin\ccx_MT.exe.
<p align="center">
  <img src="\assets\blog\20260924\welsim_calculix_preferences_solvers.png" alt="welsim_calculix_preferences_solvers" />
</p>


4.Click OK to save the configuration.

5.During specific finite element analyses, simply set the Solver property of the Study Settings node to CalculiX in the project tree window.
<p align="center">
  <img src="\assets\blog\20260924\welsim_calculix_study_setttings_solvers.png" alt="welsim_calculix_study_setttings_solvers" />
</p>

Once configuration is complete, you can directly call the CalculiX solver.

## Conclusion
This article describes how to configure the co-solving of finite element models between CalculiX and WELSIM under the Windows operating system. In a Linux environment, the setup and operations are largely identical. The WELSIM installation package does not include the CalculiX solver, so users should download the CalculiX binary program and configure its path themselves as demonstrated in the article.

WELSIM currently does not support post-processing for CalculiX results, but reading and displaying CalculiX result files will be supported in future versions.

---

<small>WELSIM and the author are not affiliated with CalculiX or Abaqus, and have no direct relationship with the development teams or organizations of CalculiX and Abaqus. The names of the open-source software referenced here are used solely for technical blog articles and software usage reference. </small>
