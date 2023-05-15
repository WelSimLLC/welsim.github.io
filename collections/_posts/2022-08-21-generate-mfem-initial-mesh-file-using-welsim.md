---
lang: en
layout: post
title:  "Generate MFEM initial mesh file using WELSIM"
date:   2022-08-21
author: "[SimLet](https://twitter.com/getwelsim)"
---


MFEM (mfem.org) is one of the most active open-source partial differential equation (PDE) solver projects in recent years. Although this open source package is promoted as a lightweight and scalable C++ library, it provides higher-order finite element spaces. Additionally supporting mixed elements, discontinuous Galerkin elements, isogeometric analysis methods, and more. MFEM is a great advantage particularly in high-performance computing, not only supporting message passing interface (MPI) parallelism and shared memory parallelism (OpenMP), but also being beneficial in GPU parallel computing. The built-in post-processing program GLVis can easily read and display the result files. The BSD-3 license is also extremely friendly to developers. Recently, MFEM started supporting Python programming, which makes this library even more convenient for various researchers.

<p align="center">
  <img src="\assets\blog\mfem_electromangetics_results.png" alt="welsim_electrostatic_voltage" />
</p>


MFEM has been brought to Welsim's attention more than 10 years ago, and at the time, only some electromagnetic field problems could be solved. Eventually, however, the functionality became more stable, and MFEM now supports a collection linear solvers, such as hypre and PETSc, eigenvalue solver SLEPc, and parallel iterative solver Ginkgo. Moreover, different types of elements and adaptive mesh are available. MFEM also provides a large number of examples, which can help users quickly understand and use the library.


Like other PDE solvers, MFEM requires a necessary mesh input file. One advantage of MFEM is that users can choose to apply a simple and rough initial mesh at the beginning of the modeling. After that, a more optimized mesh can be generated through the adaptive mesh feature, during the calculation. The mesh format of MFEM is concise and clear. It contains information blocks including the dimension, elements, nodes, and boundary. The program's official website provides more details about the mesh file format.

<p align="center">
  <img src="\assets\blog\mfem_mesh_file.png" alt="welsim_mfem_mesh1" />
</p>


Although MFEM has many excellent features and the mesh file format is easy to understand, for complex geometric models, it is difficult to manually generate the mesh. Currently, the community does not have a user-friendly initial mesh generation tool, which limits its application to complex geometric models to a certain extent. WELSIM not only has a simple and easy-to-use graphical user interface, but also supports geometry-to-mesh generation and export of mesh files in multiple formats. Users can quickly obtain meshes of complex models by selecting the output mesh file in MFEM format.

<p align="center">
  <img src="\assets\blog\export_mesh.png" alt="welsim_export_mesh" />
</p>


In many cases of scientific computing and PDEs solving, it is insufficient for mesh files to contain only node and element information. The boundary mesh that is selected in the boundary conditions is also needed. WELSIM provides a practical solution for this scenario, users only need to set the analysis type to Electromagnetics in the GUI, add some boundary conditions such as voltage, etc., and select the corresponding geometric model boundary. Then, select Export Input Scripts from the Toolbar.

<p align="center">
  <img src="\assets\blog\export_input_script.png" alt="welsim_export_input_script" />
</p>

At this point, multiple solver-related files are generated. The mesh file contains not only node and element information, but boundary elements are also defined.

<p align="center">
  <img src="\assets\blog\mfem_mesh_with_bounary.png" alt="welsim_mfem_mesh_boundary" />
</p>


This way, users can quickly generate complex mesh files for the MFEM solver, which is more practical for real-world engineering applications.

<p align="center">
  <img src="\assets\blog\mfem_electromangetics_results_e_field.png" alt="welsim_electrostatic_e_field" />
</p>


WelSim currently supports automated mesh generation of Tet4/10 and Tri3/6.

<br>

<small>
WelSim is not affiliated with the MFEM team. MFEM is used only as a nominative reference to the open-source project and software developed and released by the MFEM team.
</small>


******

<small>
[WelSimulation LLC](https://welsim.com) is an independent engineering simulation technology provider, located in Greater Pittsburgh, PA. Its flagship product WESLIM is a general-purpose engineering simulation software with an all-in-one graphical user interface and self-integrated features.
</small>
