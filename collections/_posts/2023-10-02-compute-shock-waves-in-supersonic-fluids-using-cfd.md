---
lang: en
layout: post
title:  "Compute shock waves in supersonic fluids using CFD"
date:   2023-10-02
author: "[SimLet](https://twitter.com/getwelsim)"
---

Shockwaves are a complex physical phenomenon. When an object's velocity exceeds the speed of sound of medium, shockwaves are generated at the points where the object's surface changes. Shockwaves can occur in gases as well as in liquids, although they are less common in liquids due to their higher speed of sound. One of the most common instances of shockwaves is generated when aircraft break the sound barrier (at approximately 340 meters per second) while flying within the Earth's atmosphere. Additionally, shockwaves can be generated in various situations such as within supersonic aircraft engines and nozzles, explosives, and more.
<p align="center">
  <img src="\assets\blog\20231002\welsim_warjet_shockwave.png" alt="welsim_warjet_shockwave" />
</p>


When an aircraft is flying at supersonic speeds, the air in front of the aircraft experiences a sudden compression, forming a concentrated compression interface known as a shockwave. Shockwaves exhibit strong nonlinearity. When passing through a shockwave, the properties of the medium (typically gas) such as pressure, density, and temperature, undergo a sudden increase while the velocity abruptly decreases. Essentially, this is a process where kinetic energy is converted into pressure energy. Additionally, the rapid increase in pressure results in a loud sonic boom as some of the energy is transformed into acoustic wave energy. Due to the abrupt change in gas density at the shockwave location, we can capture images of shockwaves, and in modern designs of almost all supersonic wind tunnels, observation ports or recording positions are included.


The thickness of a shockwave depends on the type of gas and the velocity of the moving object. In the case of an ideal gas, shockwaves have no thickness and are considered as physical discontinuities. However, real gases have viscosity and thermal conductivity, which makes shockwaves continuous but still very thin. In engineering, shockwaves are often approximated as discontinuities. Moreover, as the Mach number increases, the shockwave thickness decreases.
<p align="center">
  <img src="\assets\blog\20231002\welsim_warjet_shockwave2.png" alt="welsim_warjet_shockwave2" />
</p>


In engineering, we often need to consider the changes in pressure and velocity of the fluid before and after a shockwave. The traditional approach involves using the method of characteristics, along with consulting manuals and charts to find the pressure and velocity transformations for a specific gas. Nowadays, with the maturity of CFD (Computational Fluid Dynamics) technology, we can obtain preliminary numerical solutions on a computer within minutes. Furthermore, we can obtain more complex results involving multiple interacting shockwaves.

Numerically, due to the distinct discontinuities associated with shockwaves, traditional finite element methods may not be the most suitable. Finite volume methods (FVM) with Riemann solvers as core algorithms have shown great adaptability in the CFD field, especially in the realm of compressible fluid dynamics. Therefore, in the CFD field, particularly in compressible fluid CFD, FVM has excelled.

## Performing Supersonic CFD Simulations with SU2 and WELSIM

Below, we'll demonstrate how to conduct transient CFD analysis for supersonic flow using examples.

(1) Taking a two-dimensional model as an example, after opening WELSIM, create a new project and set the model as a 2D transient fluid model.
<p align="center">
  <img src="\assets\blog\20231002\welsim_cfd2d_shockwave_analysis_type.png" alt="welsim_cfd2d_shockwave_analysis_type" />
</p>


(2) Import the geometric model.
<p align="center">
  <img src="\assets\blog\20231002\welsim_cfd2d_shockwave_geomtry.png" alt="welsim_cfd2d_shockwave_geomtry" />
</p>


(3) Mesh the geometry with a maximum element size set to 0.001 m.
<p align="center">
  <img src="\assets\blog\20231002\welsim_cfd2d_shockwave_mesh.png" alt="welsim_cfd2d_shockwave_mesh" />
</p>


(4) Set the time step for the solver to 5e-7 seconds, with a total simulation time of 0.002 seconds.
<p align="center">
  <img src="\assets\blog\20231002\welsim_cfd2d_shockwave_study1.png" alt="welsim_cfd2d_shockwave_study1" />
</p>


(5) Utilize the SU2 solver.
<p align="center">
  <img src="\assets\blog\20231002\welsim_cfd2d_shockwave_study2.png" alt="welsim_cfd2d_shockwave_study2" />
</p>


(6) Employ the RANS equations for compressible fluid as the governing equations with the Spalart-Allmaras turbulence model.
<p align="center">
  <img src="\assets\blog\20231002\welsim_cfd2d_shockwave_study3.png" alt="welsim_cfd2d_shockwave_study3" />
</p>

(7) Configure the solver's parameters.
<p align="center">
  <img src="\assets\blog\20231002\welsim_cfd2d_shockwave_study4.png" alt="welsim_cfd2d_shockwave_study4" />
</p>

(8) Set the conditions for the free-stream field. Here, specify a Mach number of 1.5, zero angle of attack, a pressure of 5.38e4 Pa, temperature of 210K, and a Reynolds number of 1.35e6.
<p align="center">
  <img src="\assets\blog\20231002\welsim_cfd2d_shockwave_free_stream.png" alt="welsim_cfd2d_shockwave_free_stream" />
</p>

(9) Define the boundary conditions at the inlet, which are numerically similar to the free-stream conditions.
<p align="center">
  <img src="\assets\blog\20231002\welsim_cfd2d_shockwave_inlet.png" alt="welsim_cfd2d_shockwave_inlet" />
</p>

(10) Set the boundary conditions at the outlet.
<p align="center">
  <img src="\assets\blog\20231002\welsim_cfd2d_shockwave_outlet.png" alt="welsim_cfd2d_shockwave_outlet" />
</p>


(11) Specify the symmetry boundary conditions.
<p align="center">
  <img src="\assets\blog\20231002\welsim_cfd2d_shockwave_symmetry.png" alt="welsim_cfd2d_shockwave_symmetry" />
</p>


(12) Set the thermal boundary conditions with a value of zero, indicating no convective heat transfer. This condition is similar to a wall.
<p align="center">
  <img src="\assets\blog\20231002\welsim_cfd2d_shockwave_heatflux.png" alt="welsim_cfd2d_shockwave_heatflux" />
</p>


Click the Solve button. Since this is a transient simulation, it will require a significant amount of physical computation time based on the mesh density and duration. After the calculation is complete, add nodes for Mach number and pressure results and display contour plots. The following figures show the Mach number in the flow field at 0.002 seconds and the pressure field at 0.00125 seconds. Clearly, shockwaves are generated and interact with each other.
<p align="center">
  <img src="\assets\blog\20231002\welsim_cfd2d_shockwave_result_mach.png" alt="welsim_cfd2d_shockwave_result_mach" />
</p>
<p align="center">
  <img src="\assets\blog\20231002\welsim_cfd2d_shockwave_result_pressure.png" alt="welsim_cfd2d_shockwave_result_pressure" />
</p>


The calculation results for this example are available in the following videos: 

Pressure Field.

[CFD for supersonic fluid with shock waves. Mach number is 1.5. Pressure result](https://www.youtube.com/watch?v=BMyif3nxh9w)

Velocity Field.

[CFD for supersonic fluid with shock waves. Mach number is 1.5. Pressure result](https://www.youtube.com/watch?v=UkCITPq_nVo)

Additionally, this example includes automated regression testing in WELSIM, which is beneficial for long-term maintenance of the solver and front-end software. The test files have been open-sourced and shared on GitHub at the following address:

[https://github.com/WelSimLLC/WelSimAutoTests](https://github.com/WelSimLLC/WelSimAutoTests)


## Conclusion
Simulations of supersonic flow with shockwaves demand high mesh density, with certain areas requiring increased density while others need lower density to save computational resources. Adaptive meshing can significantly improve computational efficiency. Modern CFD software also reduces physical computation time through GPU parallelization.


SU2 is an excellent open-source CFD solver with good performance and user-friendly protocols. It can rapidly solve transient supersonic flow problems with shockwaves. WELSIM simplifies the use of SU2 thanks to its user-friendly graphical interface. WELSIM seamlessly integrates with SU2 for solving and displaying results, or it can generate the SU2 input files that users need. Currently, WELSIM is one of the best pre-and post-processing software solutions for SU2 worldwide.

---

<small>
_WELSIM is the #1 engineering simulation CAE software for the open-source community._
</small>
