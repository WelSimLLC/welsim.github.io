---
lang: en
layout: post
title:  "Implicit transient analysis using OpenRadioss"
date:   2026-10-17
author: "[SimLet](https://twitter.com/getwelsim)"
---

The first impression OpenRadioss gives users is that of an excellent explicit dynamics solver designed for short-duration, highly nonlinear problems such as impacts, explosions, and shocks. However, it also includes a fully integrated implicit solver module that supports linear static, nonlinear static, buckling, springback, and quasi-static implicit dynamics analyses. This makes OpenRadioss suitable for scenarios requiring large time steps and unconditional stability, such as stamping springback, assembly pre-tightening, and structural static strength.
<p align="center">
  <img src="\assets\blog\20261017\welsim_implicit_vs_explicit.jpeg" alt="welsim_implicit_vs_explicit" />
</p>

Although the official OpenRadioss project has been discontinued, open-source community projects and teams continue to maintain it. For instance, OpenCourant provides both source code and precompiled executables. The official default precompiled version does not include the implicit solver, so if users want to use implicit calculation capabilities or the arc-length method, they need to compile the entire OpenRadioss project themselves in tandem with the open-source linear algebra solver MUMPS. Some precompiled versions with implicit functionality are also available in the open-source community.

WELSIM already supports the implicit solver of OpenRadioss. It can not only generate OpenRadioss input scripts but also through simple configuration seamlessly connect to OpenRadioss solver to perform calculations and display result contour. The steps are as follows:

1.Configure the solver path: In Preferences, set the folder location to the OpenRadioss solver. Note that this OpenRadioss build must already support implicit solving.
<p align="center">
  <img src="\assets\blog\20261017\welsim_radioss_preferences.png" alt="welsim_radioss_preferences" />
</p>

2.Set up the project: Create a new FEA project and set it to implicit transient structural analysis. Import the model, assign materials, and generate the mesh.
<p align="center">
  <img src="\assets\blog\20261017\welsim_radioss_project_property.png" alt="welsim_radioss_project_property" />
</p>

3.Configure solver settings: In the Study object properties, configure the solver options. Select the OpenRadioss solver and set the direct method MUMPS as the linear algebra solver, which generates the corresponding /IMPL/SOLVER/2 command. Select the BFGS Quasi-Newton solver as the nonlinear solver, which corresponds to the /IMPL/NONLIN/2 command. Enable the Arc-Length method, which corresponds to the /IMPL/DT2 or /IMPL/DT3 commands. It is worth noting that for an analysis without contact or nonlinear materials, the Large Deflection option must be turned on to generate the /IMPL/NONLIN command; otherwise, the /IMPL/LINEAR command will be generated.
<p align="center">
  <img src="\assets\blog\20261017\welsim_radioss_study.png" alt="welsim_radioss_study" />
</p>

4.Set load steps and substeps: Since this is a transient analysis, configure the load steps and substeps in the Study object properties as well. For a simple single load step analysis, only substeps need to be configured: enable automatic time stepping, set the initial time step to 0.1, the minimum time step to 0.01, and the maximum time step to 0.5. The corresponding commands are /IMPL/DTINI and /IMPL/DT/STOP.
<p align="center">
  <img src="\assets\blog\20261017\welsim_radioss_study2.png" alt="welsim_radioss_study2" />
</p>

5.Solve and view results: After setting all initial and boundary conditions, click Solve to directly obtain the transient results. The time distribution of the results for each substep is shown below.
<p align="center">
  <img src="\assets\blog\20261017\welsim_radioss_result_stress.png" alt="welsim_radioss_result_stress" />
</p>

6.Access input and result files: If you want to check the generated input *.rad file and result files, right-click the Answer object and select "Open Containing Folder" from the context menu to open the corresponding folder.
<p align="center">
  <img src="\assets\blog\20261017\welsim_radioss_open_folder.png" alt="welsim_radioss_open_folder" />
</p>


## Conclusion
OpenRadioss's implicit solving capability is just as robust as its explicit counterpart, delivering reliable results at high computational speed. Through testing, the author found that for simple problems, the implicit solver is highly efficient and takes less solving time. WELSIM is one of the most comprehensive pre- and post-processors in the simulation industry supporting the OpenRadioss solver.

---

<small>WELSIM and the author are not affiliated with OpenRadioss or OpenCourant, nor do they have a direct relationship with the OpenRadioss or OpenCourant development teams or institutions. Names and images of these open-source tools cited here are used solely for technical blogging and software reference purposes.</small>
