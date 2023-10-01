---
lang: en
layout: post
title:  "Transient CFD Analysis of Unsteady Fluids"
date:   2023-09-28
author: "[SimLet](https://twitter.com/getwelsim)"
---


In engineering, there are many unsteady fluid problems that cannot be simply solved using steady-state methods. Unsteady flows are primarily caused by two factors. One is due to internal fluid instability or a non-equilibrium initial state of the fluid, such as turbulence of various scales, shockwaves, convection, etc. The other is due to changing boundary conditions or source terms, like pulsating flows or the rotation of rotor blades in machinery. For these unsteady flows, it is necessary to use transient analysis methods in order to understand the state of the fluid and its solid contact surfaces.
<p align="center">
  <img src="\assets\blog\20230928\welsim_turbulence.png" alt="welsim_turbulence" />
</p>



Transient analysis involves calculating the flow field for multiple time steps. The computational workload also increases linearly with the duration of the simulation. Therefore it is a common approach to compute a steady state within a short time interval at each time step, numerically. Then, the results of this steady state are used as the initial conditions for the next time step’s calculation. Depending on the time solver used, the choice of time step may vary slightly, with implicit solvers typically allowing for larger time steps than explicit solvers. The well-known open-source multi-physics solver SU2 has been proven to work well for unsteady CFD problems. WELSIM also added support for SU2 in its 2023R3 release; for more details, refer to the article “[Generate SU2 solver scripts using WELSIM](https://welsim.com/2023/04/21/generate-su2-solver-scripts-using-welsim.html).”

Steps for Unsteady CFD Analysis
Below is an example demonstrating how to perform transient CFD analysis:

(1) Using a 2D model as an example, open WELSIM and create a new project, setting the model as a 2D transient fluid model.
<p align="center">
  <img src="\assets\blog\20230928\welsim_cfd2d_analysis_type.png" alt="welsim_cfd2d_analysis_type" />
</p>

(2) Import the geometry model.
<p align="center">
  <img src="\assets\blog\20230928\welsim_cfd2d_import_naca0012.png" alt="welsim_cfd2d_import_naca0012" />
</p>

(3) Create the mesh, setting the maximum element size to 0.03 meter.
<p align="center">
  <img src="\assets\blog\20230928\welsim_cfd2d_mesh_settings.png" alt="welsim_cfd2d_mesh_settings" />
</p>

(4) Set the time step for the solver to 0.0005 second, with a total run time of 0.6 second.
<p align="center">
  <img src="\assets\blog\20230928\welsim_cfd2d_study01.png" alt="welsim_cfd2d_study01" />
</p>

(5) Use the SU2 solver.
<p align="center">
  <img src="\assets\blog\20230928\welsim_cfd2d_study02.png" alt="welsim_cfd2d_study02" />
</p>

(6) The governing equations use RANS for compressible fluids, and the turbulence model is Spalart-Allmaras.
<p align="center">
  <img src="\assets\blog\20230928\welsim_cfd2d_study03.png" alt="welsim_cfd2d_study03" />
</p>


(7) Configure relevant solver parameters.
<p align="center">
  <img src="\assets\blog\20230928\welsim_cfd2d_study04.png" alt="welsim_cfd2d_study04" />
</p>

(8) Set the free-stream field conditions, including a Mach number of 0.3, an angle of attack of 17 degrees, standard temperature and pressure, and a Reynolds number of 1000.
<p align="center">
  <img src="\assets\blog\20230928\welsim_cfd2d_free_stream_field.png" alt="welsim_cfd2d_free_stream_field" />
</p>


(9) Define the far-field boundary conditions.
<p align="center">
  <img src="\assets\blog\20230928\welsim_cfd2d_bc_farfield.png" alt="welsim_cfd2d_bc_farfield" />
</p>

(10) Specify the thermal boundary conditions with a value of zero for heat flux and no heat convection.
<p align="center">
  <img src="\assets\blog\20230928\welsim_cfd2d_bc_flux.png" alt="welsim_cfd2d_bc_flux" />
</p>


Click the solve button. Since it is a transient computation, it will require a significant amount of computational time based on the mesh density and duration. After the calculation is complete, add a Mach number result object and display contour plots. The images below show the Mach number in the flow field at 0.027 seconds and 0.597 seconds, respectively.

<p align="center">
  <img src="\assets\blog\20230928\welsim_cfd2d_sol1.jpeg" alt="welsim_cfd2d_sol1" />
</p>

<p align="center">
  <img src="\assets\blog\20230928\welsim_cfd2d_sol2.jpeg" alt="welsim_cfd2d_sol2" />
</p>


The calculation result video for this case is as follows.
<iframe width="560" height="315" src="https://www.youtube.com/embed/wjiuKQ_hsLc?si=Egc7Lnpq0czVOJd4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>


Additionally, this case has been integrated into WELSIM’s automated regression testing library, which can be beneficial for the long-term maintenance of the solver and front-end software. The test files have been open-sourced and shared on GitHub at the following address:


[https://github.com/WelSimLLC/WelSimAutoTests](https://github.com/WelSimLLC/WelSimAutoTests)



## WELSIM’s Support for SU2 Commands
The config file of SU2 is the main solver input file, and currently, WELSIM as a preprocessor supports a significant number of core commands. SU2 version 7.5.1 includes a total of 671 commands, and WELSIM already supports 134 commands, accounting for 20% of the total. The supported commands are listed below.

* SOLVER
* MATH_PROBLEM
* KIND_TURB_MODEL
* KIND_TRANS_MODEL
* BODY_FORCE
* BODY_FORCE_VECTOR
* RESTART_SOL
* FLUID_MODEL
* SPECIFIC_HEAT_CP
* VISCOSITY_MODEL
* MU_CONSTANT
* CONDUCTIVITY_MODEL
* THERMAL_CONDUCTIVITY_CONSTANT
* REYNOLDS_NUMBER
* REYNOLDS_LENGTH
* PRANDTL_LAM
* PRANDTL_TURB
* MACH_NUMBER
* INIT_OPTION
* FREESTREAM_OPTION
* FREESTREAM_PRESSURE
* FREESTREAM_DENSITY
* FREESTREAM_TEMPERATURE
* FREESTREAM_TEMPERATURE_VE
* INC_DENSITY_MODEL
* INC_ENERGY_EQUATION
* INC_DENSITY_INIT
* INC_VELOCITY_INIT
* INC_TEMPERATURE_INIT
* FREESTREAM_VELOCITY
* FREESTREAM_VISCOSITY
* FREESTREAM_INTERMITTENCY
* FREESTREAM_TURBULENCEINTENSITY
* FREESTREAM_NU_FACTOR
* SIDESLIP_ANGLE
* AOA
* REF_ORIGIN_MOMENT_X
* REF_ORIGIN_MOMENT_Y
* REF_ORIGIN_MOMENT_Z
* REF_AREA
* REF_LENGTH
* REF_DIMENSIONALIZATION
* MARKER_PLOTTING
* MARKER_MONITORING
* MARKER_ANALYZE
* MARKER_DESIGNING
* MARKER_EULER
* MARKER_FAR
* MARKER_SYM
* MARKER_NEARFIELD
* INLET_TYPE
* INC_INLET_TYPE
* MARKER_INLET
* MARKER_INLET_SPECIES
* MARKER_INLET_TURBULENT
* MARKER_SUPERSONIC_INLET
* MARKER_SUPERSONIC_OUTLET
* MARKER_OUTLET
* INC_OUTLET_TYPE
* MARKER_ISOTHERMAL
* MARKER_HEATFLUX
* MARKER_HEATTRANSFER
* MARKER_PRESSURE
* MARKER_DAMPER
* TIME_MARCHING
* CFL_NUMBER
* CFL_ADAPT
* CFL_ADAPT_PARAM
* RK_ALPHA_COEFF
* TIME_DISCRE_FLOW
* TIME_DISCRE_FEM_FLOW
* TIME_DISCRE_ADJFLOW
* TIME_DISCRE_TURB
* LINEAR_SOLVER
* LINEAR_SOLVER_PREC
* LINEAR_SOLVER_ERROR
* LINEAR_SOLVER_ITER
* CONV_RESIDUAL_MINVAL
* CONV_STARTITER
* CONV_CAUCHY_ELEMS
* CONV_CAUCHY_EPS
* CONV_FIELD
* MGLEVEL
* MGCYCLE
* MG_PRE_SMOOTH
* MG_POST_SMOOTH
* MG_CORRECTION_SMOOTH
* MG_DAMP_RESTRICTION
* MG_DAMP_PROLONGATION
* NUM_METHOD_GRAD
* NUM_METHOD_GRAD_RECON
* VENKAT_LIMITER_COEFF
* ADJ_SHARP_LIMITER_COEFF
* CONV_NUM_METHOD_FLOW
* MUSCL_FLOW
* SLOPE_LIMITER_FLOW
* JST_SENSOR_COEFF
* LAX_SENSOR_COEFF
* CONV_NUM_METHOD_ADJFLOW
* MUSCL_ADJFLOW
* SLOPE_LIMITER_ADJFLOW
* MESH_FORMAT
* MESH_FILENAME
* MESH_OUT_FILENAME
* CONV_FILENAME
* SOLUTION_FILENAME
* SOLUTION_ADJ_FILENAME
* RESTART_FILENAME
* RESTART_ADJ_FILENAME
* VOLUME_FILENAME
* VOLUME_ADJ_FILENAME
* GRAD_OBJFUNC_FILENAME
* VALUE_OBJFUNC_FILENAME
* SURFACE_FILENAME
* SURFACE_ADJ_FILENAME
* SURFACE_SENS_FILENAME
* VOLUME_SENS_FILENAME
* TIME_DOMAIN
* TIME_ITER
* ITER
* RESTART_ITER
* TIME_STEP
* SCREEN_OUTPUT
* HISTORY_OUTPUT
* VOLUME_OUTPUT
* OUTPUT_WRT_FREQ
* OUTPUT_FILES



## Conclusion
SU2 is an excellent open-source CFD solver known for its performance and accessible licensing. It is capable of rapidly solving unsteady fluid problems involving turbulence. With its user-friendly graphical interface, WELSIM makes working with SU2 easier. WELSIM seamlessly integrates with SU2 for solving and displaying results, as well as generating SU2 computation input scripts as needed. Currently, WELSIM is recognized as the leading pre- and post-processing software worldwide for supporting SU2.


<small>
_WELSIM is the #1 engineering simulation CAE software for the open-source community._
</small>
