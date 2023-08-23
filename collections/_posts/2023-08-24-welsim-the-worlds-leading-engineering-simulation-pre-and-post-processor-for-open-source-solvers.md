---
lang: en
layout: post
title:  "WELSIM - The World's Leading Engineering Simulation Pre- and Post-Processor for Open-Source Solvers"
date:   2023-08-24
author: "[SimLet](https://twitter.com/getwelsim)"
---


With the rapid development of engineering simulation CAE software over the past few decades, it has become a highly complex and intricate product. Users' expectations for simulation CAE software have also risen accordingly. Modern simulation software not only requires rich computational capabilities and accurate results but also demands a graphical interactive interface (GUI) that is user-friendly, easy to learn, and intuitive. This presents significant challenges for small and medium-sized development teams. Many outstanding simulation CAE projects, due to a lack of ongoing development resources, end up failing or attracting little attention. Similarly, some well-established and capable solvers, lacking a user-friendly GUI and an automated maintenance system for sustainable development, struggle to expand their user base and community influence. The lack of attention to excellent solvers undoubtedly results in the waste of computing resources.
<p align="center">
  <img src="\assets\blog\20230824\welsim_processors_demo.png" alt="welsim_processors_demo" />
</p>


Through years of dedicated research and development, the engineering simulation software WELSIM has acquired the capability to address these industry issues. Developers of exceptional solvers, particularly those working on open-source solvers, can focus on advancing their solver's core features while entrusting the pre- and post-processing tasks to WELSIM. Additionally, WELSIM enables the establishment of an automated regression testing system, ensuring the precision of solvers. This approach significantly conserves development resources and time.



## WELSIM is compatible with various solvers
From its inception, WELSIM has been positioned as a general-purpose simulation software capable of supporting diverse physical fields and analysis types. It currently seamlessly integrates with several third-party open-source solvers and, with ongoing development, will extend support to even more exceptional open-source solvers.

A user-friendly graphical interactive interface is an essential aspect of excellent pre- and post-processors. WELSIM already contains a comprehensive set of pre-and post-processing features.

(1) It possesses a variety of user interaction windows, such as project tree, properties, 3D graphics, output, table, chart, and more. For more details, refer to the article "Window design and development for general-purpose simulation software."
<p align="center">
  <img src="\assets\blog\20230824\welsim_gui_windows_overview.png" alt="welsim_gui_windows_overview" />
</p>


(2) It features a range of user interaction commands and menus. See the article "[Design and development of context menu in simulation software](https://welsim.com/2023/05/28/window-design-and-development-for-general-purpose-simulation-software.html)" for more information.
<p align="center">
  <img src="\assets\blog\20230824\welsim_rmb_tree.png" alt="welsim_rmb_tree" />
</p>


(3) It includes a flexible material editing module. Material definitions are extensively used in engineering analysis, and WELSIM's material module is user-friendly while covering almost all material properties used in engineering analyses. The material module also incorporates curve-fitting capabilities to derive material parameters from test data.
<p align="center">
  <img src="\assets\blog\20230824\welsim_rmb_mat_curvefit.png" alt="welsim_rmb_mat_curvefit" />
</p>


(4) The unit module supports over 50 quantities and 16 unit systems. All unit properties are handled in the front end, eliminating the need for the solver to consider any unit conversions. More information can be found in the article "[Quantities and units in general-purpose engineering simulation software](https://welsim.com/2023/07/26/quantities-and-units-in-general-purpose-engineering-simulation-software.html)."
<p align="center">
  <img src="\assets\blog\20230824\welsim_units.png" alt="welsim_units" />
</p>


(5) It offers geometric model import functionality. It can swiftly read STEP format geometry files and display them in the 3D graphics window. The assembly model is supported. The built-in contact search feature can automatically identify contact pairs for assembly, users do not need to manually define contact pairs.
<p align="center">
  <img src="\assets\blog\20230824\welsim_data_cad.png" alt="welsim_data_cad" />
</p>


(6) It features a fully automatic meshing module that quickly generates finite element mesh for successive analysis.
<p align="center">
  <img src="\assets\blog\20230824\welsim_data_mesh.png" alt="welsim_data_mesh" />
</p>

(7) It provides various analysis setting capabilities. Supported conditions include but are not limited to multi-step settings, linear algebra solver parameters, nonlinear solver coefficients, boundary conditions, field conditions, initial conditions, and more.
<p align="center">
  <img src="\assets\blog\20230824\welsim_solver_settings.png" alt="welsim_solver_settings" />
</p>


(8) It enables direct solver invocation for computation while allowing users to configure the solver's directory and path.
<p align="center">
  <img src="\assets\blog\20230824\welsim_solver_path.png" alt="welsim_solver_path" />
</p>


(9) It offers extensive post-processing capabilities. Result files can be rapidly and efficiently read. Table and chart windows display maximum and minimum result values at each step. Moreover, it provides the functionality to record dynamic results into MP4 files and export result data to common formats like VTK files.
<p align="center">
  <img src="\assets\blog\20230824\welsim_rmb_colorbar.png" alt="welsim_rmb_colorbar" />
</p>


(10) An automated regression testing system is provided to ensure the accuracy and stability of the solvers. Additionally, all test cases are open-sourced. Users can also easily create their own test cases.
<p align="center">
  <img src="\assets\blog\20230824\welsim_regression_play.png" alt="welsim_regression_play" />
</p>


## Benefits of Using WELSIM as a Pre- and Post-Processor

There are numerous benefits to using WELSIM as the pre-and post-processor for solvers.

1. It significantly reduces development time by focusing development resources on the core solver. While simulation CAE software includes modules such as pre-and post-processing, solvers, and mesh generators, these modules have vastly different development approaches and mindsets, often falling into entirely separate technology domains. Utilizing the WELSIM frontend eliminates the burdensome task of GUI development, allowing concentration on improving and enhancing the core solver, thereby enhancing the product.

2. WELSIM comes with an automated regression testing system, solver developers do not need to spend efforts on creating another regression system. Regardless of the numerical methods employed, such as finite element, finite volume, or other scientific computing approaches, CAE software requires extensive automated testing to ensure solver accuracy. Establishing such a testing system can be resource-intensive. Leveraging WELSIM's testing framework can save considerable development resources and time. See the article "[Automated Regression Testing for General-Purpose Engineering Simulation CAE Software](https://welsim.com/2023/08/22/automated-regression-testing-for-general-purpose-engineering-simulation-cae-software.html)".


3. Collaborating with WELSIM in the simulation and computation ecosystem leads to mutual development. After years of development, WELSIM has gained international recognition within ecosystems and communities. Using the WELSIM frontend enhances the brand image of the core solver, attracting more attention from the community.

4. WELSIM is user and collaborator-friendly. The development needs of users and collaborators are prioritized, aiming for prompt fulfillment. 


5. WELSIM has been long-term supported. Solver developers do not need to concern about the discontinuity of the WELSIM development and maintenance. 


6. WELSIM already encompasses a wide range of frontend features for general-purpose CAE software, applicable to nearly any type of simulation analysis. It can quickly adapt to various new solvers.

## Conclusion
WELSIM offers a world-leading engineering simulation CAE pre- and post-processing modules. It contributes continually to the simulation community through its exceptional products and friendly approach to users and collaborators. Talented solver developers are encouraged to use WELSIM as a pre- and post-processor.


---

<small>
WELSIM is the #1 engineering simulation software for the open-source community.
</small>
