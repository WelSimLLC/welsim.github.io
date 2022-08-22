---
lang: en
layout: post
title:  "Generate MFEM initial mesh file using WELSIM"
date:   2022-08-21
author: "[SimLet](https://twitter.com/getwelsim)"
---


MFEM (mfem.org) is one of the most active open-source partial differential equation (PDE) solver projects in recent years. Although this open source package is positioned as a lightweight and scalable C++ library, it provides higher-order finite element spaces, supports mixed elements, discontinuous Galerkin elements, isogeometric analysis methods, and more. In particular, it has great advantages in high-performance computing, not only supports message passing interface (MPI) parallelism and shared memory parallelism (OpenMP), but also has good strength in GPU parallel computing. The built-in post-processing program GLVis can easily read and display the result files. The BSD-3 license is also extremely friendly to developers. Recently, MFEM supports Python programming, which makes the library more convenient for various types of researchers.

<p align="center">
  <img src="\assets\blog\mfem_electromangetics_results.png" alt="welsim_electrostatic_voltage" />
</p>


The author began to pay attention to the MFEM more than 10 years ago, and at that time, only some electromagnetic field problems could be solved. Over time, the functionality has become more stable, and the supported linear solvers have become more and more abundant, such as hypre and PETSc, eigenvalue solver SLEPc, and various parallel iterative solvers Ginkgo. Many different types of elements and adaptive mesh are supported. The program also provides a large number of examples, which can help users quickly understand and use the library.


Like other PDE solvers, MFEM requires a mesh input file, which is indispensable. The advantage of MFEM is that users can choose to apply a simple and rough initial mesh at the beginning of the modeling, a more optimized mesh can be generated during the calculation through the adaptive mesh feature. The mesh format of MFEM is concise and clear. It contains information blocks including dimension, elements, nodes, and boundary. Its official website provides details about the mesh file format.

<p align="center">
  <img src="\assets\blog\mfem_mesh_file.png" alt="welsim_mfem_mesh1" />
</p>


Although MFEM has many excellent features and the mesh file format is easy to understand. For complex geometric models, it is difficult to generate the mesh manually. Currently, the community has no easy-to-use initial mesh generation tool, which limits its application to complex geometric models to a certain extent. WELSIM not only has a simple and easy-to-use graphical user interface but also supports geometry-to-mesh generation and export of mesh files in various formats. Users can quickly obtain meshes of complex models by selecting the output mesh file in MFEM format.

<p align="center">
  <img src="\assets\blog\export_mesh.png" alt="welsim_export_mesh" />
</p>


In many cases of scientific computing and PDEs solving, it is insufficient for mesh files to contain only node and element information. We also need the boundary mesh that is selected in the boundary conditions. WELSIM provides a good solution also for this scenario, users only need to set the analysis type to Electromagnetics in the GUI, add some boundary conditions such as voltage, etc., and select the corresponding geometric model boundary. Then select Export Input Scripts from the Toolbar.

<p align="center">
  <img src="\assets\blog\export_input_script.png" alt="welsim_export_input_script" />
</p>

At this point, multiple solver-related files are generated. The mesh file contains not only node and element information, but also boundary elements are defined.

<p align="center">
  <img src="\assets\blog\mfem_mesh_with_bounary.png" alt="welsim_mfem_mesh_boundary" />
</p>


In this way, users can quickly generate complex mesh files for the MFEM solver in terms of more complex simulation studies, and more practical engineering applications.

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
