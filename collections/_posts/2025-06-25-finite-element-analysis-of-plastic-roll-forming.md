---
lang: en
layout: post
title:  "Finite Element Analysis of Plastic Roll Forming"
date:   2025-06-25
author: "[SimLet](https://twitter.com/getwelsim)"
---


Roll forming, also known as cold roll forming, is an industry-wide process used to manufacture and form metal. Through successive deformation, it shapes the metal workpiece into specific profiles using a series of forming rollers arranged in sequence. This forming method offers high production efficiency, reduced waste, and enhanced product strength. Roll forming is widely applied in industrial sectors such as automotive manufacturing.
<p align="center">
  <img src="\assets\blog\20250625\welsim_roll_forming_sketch.png" alt="welsim_roll_forming_sketch" />
</p>


Simulation of roll forming is a common type of finite element analysis (FEA). With this analysis, one can predict the degree of deformation of the workpiece, the stresses and strains it undergoes, as well as determine the roller dimensions and operating speeds required for success. Since this type of analysis involves nearly all aspects of structural calculations, such as multi-load steps, nonlinear plasticity, various types of contact algorithms, rigid body dynamics, and both solid and shell elements, it is considered one of the most copmlex and difficult-to-converge models in structural analysis. An analysis of roll forming not only places high pressure on the solver, but also on the skill of its pre- and post-processors.

The general-purpose engineering simulation software WelSim, when combined with the powerful open-source FEA solver OpenRadioss, can effectively simulate various plastic forming and forging processes. This article demonstrates how to perform a roll forming simulation from a practical perspective.


## Analysis Steps

1.Open WelSim and set units. In this case, we use the kg-mm-s system.
<p align="center">
  <img src="\assets\blog\20250625\welsim_roll_forming_perference_units.png" alt="welsim_roll_forming_perference_units" />
</p>

2.Create a new aluminum alloy material named myPlastic, with the following properties:
* Density: 2.7e-6 kg/mm³
* Young's Modulus: 70 GPa
* Poisson's Ratio: 0.33
* Johnson-Cook Plasticity Properties:
  * Initial Yield Stress: 300 MPa
  * Hardening Constant: 360 MPa
  * Hardening Exponent: 0.08
<p align="center">
  <img src="\assets\blog\20250625\welsim_roll_material_plastic.png" alt="welsim_roll_material_plastic" />
</p>


After editing the material parameters, close the material window to proceed with the analysis.

3.Create a new FEM project and set the analysis type to Explicit Transient Structural Analysis in the Properties window.
<p align="center">
  <img src="\assets\blog\20250625\welsim_roll_forming_fem_project.png" alt="welsim_roll_forming_fem_project" />
</p>


4.Import the geometry model as shown below:
<p align="center">
  <img src="\assets\blog\20250625\welsim_roll_forming_import_shapes.png" alt="welsim_roll_forming_import_shapes" />
</p>


In this assembly, the bottom two rotating rollers transport the workpiece, while the top roller presses down on the workpiece. The workpiece is a square tube with chamfered corners. The cross-section of the tube is shown below:
<p align="center">
  <img src="\assets\blog\20250625\welsim_roll_forming_square_pipe_section.png" alt="welsim_roll_forming_square_pipe_section" />
</p>


For the three cylindrical rollers, set them as Shell structures. The Material is Structural Steel; Thickness is 1 mm. Set the Integration Points property to 3, and set the Rigid Body property to true.
<p align="center">
  <img src="\assets\blog\20250625\welsim_roll_forming_geometry_property_rigid_body.png" alt="welsim_roll_forming_geometry_property_rigid_body" />
</p>



For the deformable square tube workpiece, define it as a Solid structure, and assign the aluminum alloy created in Step 2 to the Material.
<p align="center">
  <img src="\assets\blog\20250625\welsim_roll_forming_geometry_property_tube.png" alt="welsim_roll_forming_geometry_property_tube" />
</p>



5.In the Mesh Settings window, set the Maximum Element Size to 10 mm. WelSim automatically meshes based on geometry type. The square tube is meshed with solid elements. The thin-walled rollers are meshed with shell elements. 
<p align="center">
  <img src="\assets\blog\20250625\welsim_roll_forming_mesh.png" alt="welsim_roll_forming_mesh" />
</p>


6.In the Contact property windows, this model defines three contact pairs: two frictionless, and one frictional. 

6.1 The first contact pair is frictional; it is between the bottom front roller and square tube. The friction coefficient is 0.9 to provide driving force as the roller rotates.
<p align="center">
  <img src="\assets\blog\20250625\welsim_roll_forming_contact1.png" alt="welsim_roll_forming_contact1" />
</p>

6.2 The second contact pair is frictionless and is between the rear bottom roller and tube.
<p align="center">
  <img src="\assets\blog\20250625\welsim_roll_forming_contact2.png" alt="welsim_roll_forming_contact2" />
</p>

6.3 The third contact pair is frictionless and is between the top pressing roller and tube. 
<p align="center">
  <img src="\assets\blog\20250625\welsim_roll_forming_contact3.png" alt="welsim_roll_forming_contact3" />
</p>


7.Now, define this analysis to be multi-step. In the properties of Study Settings object, set up 3 load steps. The end times for each step are: 0.04s, 0.045s, and 0.1s. Set the solver to OpenRadioss, or leave it as the default (Program Controlled). When performing explicit structural dynamics, WelSim defaults to OpenRadioss as the solver.
<p align="center">
  <img src="\assets\blog\20250625\welsim_roll_forming_study_settings.png" alt="welsim_roll_forming_study_settings" />
</p>


8.Next, define four boundary conditions for this analysis.

8.1. The Displacement boundary is set for the top roller. The roller moves downward 20 mm at a constant speed during first load step, then holds position.
<p align="center">
  <img src="\assets\blog\20250625\welsim_roll_forming_bc_displacement.png" alt="welsim_roll_forming_bc_displacement" />
</p>

8.2. A Constraint condition is set for top roller to prevent some rotation during simulation, only Z direction translation and X axis rotation are allowed.
<p align="center">
  <img src="\assets\blog\20250625\welsim_roll_forming_bc_constrant1.png" alt="welsim_roll_forming_bc_constrant1" />
</p>

8.3. Now, define the constraints for the bottom rollers to only allow rotation around the X-axis by setting X to False.
<p align="center">
  <img src="\assets\blog\20250625\welsim_roll_forming_bc_constrant2.png" alt="welsim_roll_forming_bc_constrant2" />
</p>

8.4. The last boundary condition is the angular velocity of the front bottom roller, which is set to a speed of 200 rad/s, and it starts in the second load step.
<p align="center">
  <img src="\assets\blog\20250625\welsim_roll_forming_bc_velocity.png" alt="welsim_roll_forming_bc_velocity" />
</p>

9.Now it's time to solve the Model. You can simply click the Solve button to begin the computation. If it's your first time using WelSim with OpenRadioss locally, you'll need to download the OpenRadioss solver and configure its path in WelSim's Preferences.
<p align="center">
  <img src="\assets\blog\20250625\welsim_roll_forming_preferences_solvers.png" alt="welsim_roll_forming_preferences_solvers" />
</p>

10.After computation, you can view results by clicking the Answer object. The Table and Chart display energy and kinetic quantities over time. These quantities include: Contact energy, External work, Internal energy, Kinetic energy, Mass, Momentum, etc.
<p align="center">
  <img src="\assets\blog\20250625\welsim_roll_forming_solution_energies.png" alt="welsim_roll_forming_solution_energies" />
</p>

11.You also can add result objects like stress, strain, displacement to evaluate the specific results of the domain. To see the deformation, you need to enable the Show Deformation property in the 3D View tab. The figure below displays the von-Mises stress contour; the Table and Chart display how stress evolves over time.
<p align="center">
  <img src="\assets\blog\20250625\welsim_roll_forming_rst_vmstress.png" alt="welsim_roll_forming_rst_vmstress" />
</p>


WelSim also supports the generation of animation, just click the record button in the Chart window to create an animation of the 3D view. The example animation is shown here:
[![roll forming von mises stress](https://img.youtube.com/vi/-38eodbujns/0.jpg)](https://youtu.be/-38eodbujns)


## Conclusion
This article demonstrates how to build and analyze a plastic roll forming simulation using a real-world example. OpenRadioss proves to be a powerful tool for transient structural analysis. Paired with WelSim's convenient pre- and post-processing capabilities, OpenRadioss becomes easier to use and integrate.

WelSim acts as both the pre- and post-processors in this case, efficiently generating complex input scripts and directly reading the result files for display. WelSim seamlessly integrates with the OpenRadioss solver.

The geometry and test files used in this article are open-sourced and available in WelSim's official test case repository:
 🔗 [https://github.com/WelSimLLC/WelSimAutoTests](https://github.com/WelSimLLC/WelSimAutoTests)


---
<small>
WelSim has no direct affiliation with the developers of OpenRadioss. References to OpenRadioss are for technical blog and software usage purposes only.
</small>

