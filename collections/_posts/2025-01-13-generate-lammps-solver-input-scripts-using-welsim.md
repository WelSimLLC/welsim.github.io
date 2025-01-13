---
lang: en
layout: post
title:  "Generate LAMMPS solver input scripts using WelSim"
date:   2025-01-13
author: "[SimLet](https://twitter.com/getwelsim)"
---

LAMMPS (Large-scale Atomic/Molecular Massively Parallel Simulator) is an excellent general-purpose molecular dynamics open-source computational software, based on the GPL license. It is primarily used to simulate systems of atoms, molecules, and macroscopic particles and can run on both Windows and Linux operating systems. It was developed by the Sandia National Laboratories and is suitable for research in various fields, ranging from materials science to biophysics. The solver supports a rich set of force fields, many atomic types, excellent computational performance, parallel and GPU computing support, and can calculate various complex microscopic models. LAMMPS is widely used in academia and industry. The latest version is 2024August29, and the project team has made the full code open-source, while also providing compiled executables and numerous examples.
<p align="center">
  <img src="\assets\blog\20250113\welsim_logo_lammps.jpg" alt="welsim_logo_lammps" />
</p>


The LAMMPS solver input script format is simple and clear, similar to most finite element analysis solver formats, making it easy to learn. The file extension can be arbitrary, but *.in is commonly used. The input file controls various parameters, including analysis type, computing region, force fields, boundary conditions, and initial conditions. Additionally, the input script can read external files, such as a separate molecular data file. This is similar to finite element input script, where large mesh files are separated and read independently. The difference is that LAMMPS’ molecular files contain information like atomic coordinates, masses, molecular bonds, bounding boxes, etc.

To better support the open-source solver and simulation community, WELSIM has recently added support for LAMMPS pre- and post-processing. Users can quickly generate LAMMPS input files for simulations. After defining the model, users can select “Output LAMMPS Files” from the Tools menu to generate solver files in a specified directory.
<p align="center">
  <img src="\assets\blog\20250113\welsim_export_lammps.png" alt="welsim_export_lammps" />
</p>
 
After a successful export, a solver input file named lammps_welsim.in will be generated, which can directly be used for molecular dynamics simulations.
<p align="center">
  <img src="\assets\blog\20250113\welsim_exported_input_script_lammps.png" alt="welsim_exported_input_script_lammps" />
</p>

At the same time, WELSIM can directly call LAMMPS executable program to solve the generated scripts. After downloading the LAMMPS solver, users can configure the solver executable path (lmp.exe) via Preferences — Solver — LAMMPS executable file. After defining the model, users can solve the problem and obtain result files.
<p align="center">
  <img src="\assets\blog\20250113\welsim_pref_lammps.png" alt="welsim_pref_lammps" />
</p>


Since LAMMPS is the default molecular dynamics solver, there is no need to set the solver properties in the Study Settings when performing joint solving.
<p align="center">
  <img src="\assets\blog\20250113\welsim_study_settings_solver.png" alt="welsim_study_settings_solver" />
</p>


## Supported Commands
The latest version of LAMMPS includes nearly 100 general commands, and WELSIM has currently supported 36 commands, which account for 36% of the total, all of which are core commands and meet most common analysis needs. The supported commands are as follows:

atom_modify, atom_style, boundary, comm_modify, comm_style, compute, compute_modify, create_atoms, create_bonds, create_box, dimension, displace_atoms, dump, dump_modify, echo, fix, group, include, lattice, log, mass, neigh_modify, neighbor, newton, pair_coeff, pair_modify, pair_style, region, run, special_bonds, thermo, thermo_modify, thermo_style, timestep, units, velocity.

More solver commands will be added with version updates and user needs.


## Post-Processing of Molecular Dynamics Results
Currently, WELSIM supports some post-processing features related to molecular dynamics. It can read LAMMPS-generated log files (log.lammps) and result files (dump.lmps), and display the results in contour.
<p align="center">
  <img src="\assets\blog\20250113\welsim_lammps_peri_result.png" alt="welsim_lammps_peri_result" />
</p>

## Conclusion

This blog introduces how to generate LAMMPS input scripts using WELSIM and how to set up joint solving. Thanks to its excellent GUI, users can quickly generate high-quality LAMMPS input scripts.

LAMMPS is licensed under the GPL open-source protocol, and WELSIM’s installation package does not include the LAMMPS solver. Users need to download the solver separately. With simple configuration, WELSIM can work together with LAMMPS to solve particle problems.

The LAMMPS input file functionality is available in the 2025R1 development version and will continue to be maintained and enhanced in the official and future releases.



---
<small>
WELSIM and the author are not affiliated with LAMMPS, its development team or institution. LAMMPS is referenced here solely for the purpose of this technical blog post and software usage.
</small>

