---
lang: en
layout: post
title:  "Generate the contact and boundary conditions for the CalculiX solver"
date:   2026-01-16
author: "[SimLet](https://twitter.com/getwelsim)"
---

CalculiX is a well-known open-source Finite Element Analysis software, focusing on structural mechanics (static, dynamic, nonlinear) and thermal analysis. It is suitable for scientific research, teaching, and small-to-medium engineering scenarios. 

The core advantages of CalculiX are as follows: 
Open-Source and Free. It is licensed under the GNU General Public License (GPL), allowing individuals, enterprises, and research institutions to freely use, modify, and distribute the source code. 

INP File Format Compatibility. It supports the INP input file format used by Abaqus. Most Abaqus models can be directly imported into CalculiX for solving, which shortens the learning curve for users. 

Lightweight Solver. The solver features streamlined code and has lower hardware resource requirements compared to commercial software, making it ideal for fast computation of small-to-medium scale models. 

Seamless Third-Party Integration. It offers excellent compatibility with third-party preprocessors and postprocessors, facilitating the integration of pre/post-processing tools with the solver.

<p align="center">
  <img src="\assets\blog\20260116\welsim_finite_element_thermal_exhaust_manifold.png" alt="welsim_finite_element_thermal_exhaust_manifold" />
</p>

In a previous article titled Generate CalculiX solver files using WELSIM, the author introduced methods to quickly generate CalculiX input scripts. Currently, WELSIM can serve as a robust preprocessor for CalculiX to generate input files, greatly simplifying the process of performing finite element analysis with CalculiX. This article elaborates on the commands for generating contact and boundary conditions in greater detail.

## Contact
In the finite element structural analysis of multi-body systems, contact setup is an essential step. This section describes the generation of two common contact types: bonded contact and separable contact.

### Bonded Contact
Bonded contact is a contact condition used to simulate a fully rigid connection between multiple bodies. It is applicable to scenarios where there is no relative sliding, separation, or gap between components (e.g., welded joints, adhesive bonds, cured interference fits, and rigid bolted connections). Bonded contact enforces identical nodal displacements across the contact interface, essentially "fusing" multiple independent components into a single integrated structure.

The setup interface for bonded contact is shown in the figure below.
<p align="center">
  <img src="\assets\blog\20260116\welsim_calculix_contact_bonded.png" alt="welsim_calculix_contact_bonded" />
</p>

When converting to CalculiX commands, the *TIE keyword is used. The generated input commands are as follows:
```
*Tie, Name=ID_15, Position tolerance=0.01, Adjust=No
Target_Surface_15, Master_Surface_15
```

The surface elements defined in the mesh file are as follows:
```
** Box_to_Box_1
*SURFACE, TYPE=ELEMENT, NAME=Master_Surface_15       
70, S2       63, S2       74, S2       61, S2       66, S1       69, S2
** Box_to_Box_1*SURFACE, TYPE=ELEMENT, NAME=Target_Surface_15      
166, S3      185, S2      160, S3      173, S2      171, S4      169, S3
```

### Separable Contact
Separable contact is a nonlinear contact condition used to simulate three interface states between multiple bodies: contact, sliding, and separation. Its core characteristic is that the contact interface only transmits normal pressure (no tensile forces) and allows free sliding or sticking in the tangential direction. It is suitable for scenarios involving dynamic contact and separation between components (e.g., gear engagement, sheet metal forming, bearing rolling, and mechanical impact). Based on friction assumptions, it can be further grouped into frictionless contact and frictional contact.

The contact setup interface in WELSIM is shown in the figure below.
<p align="center">
  <img src="\assets\blog\20260116\welsim_calculix_contact_frictional.png" alt="welsim_calculix_contact_frictional" />
</p>

When converting to CalculiX commands, the *CONTACT keyword is used. It is important to note that CalculiX specifies that the master surface (also known as the independent surface) must be defined using elements. The slave surface (also known as the dependent surface) can be defined using either elements or nodes.

The corresponding generated CalculiX commands are as follows:
```
** Box_to_Box 1
*Surface interaction, Name=SurfaceInteraction_15
*Surface behavior, Pressure-overclosure=Hard
*Friction 0.15
*Contact Pair, Interaction=SurfaceInteraction_15, Type=Surface to surface
Target_Surface_15, Master_Surface_15
```

## Boundary conditions in structural analysis
Setting boundary conditions is a critical step in finite element analysis and a key function of preprocessing software for generating solver commands. WELSIM supports a wide range of CalculiX boundary conditions. This section demonstrates how a preprocessor generates boundary conditions for structural analysis and presents the corresponding solver commands.

### Constraints or Displacement
Displacement boundary conditions are essential (Dirichlet) boundary conditions used to constrain the nodal displacement degrees of freedom (DOFs) of a model. Their role is to restrict the rigid-body motion of the structure and simulate real-world support constraints (e.g., fixed supports, pin supports), serving as the foundational conditions for static and dynamic structural analysis. For 3D models: For solid elements, translational DOFs in the X/Y/Z directions (Ux/Uy/Uz) can be constrained.
For shell elements, additional rotational DOFs about the X/Y/Z axes (Rx/Ry/Rz) can be constrained.
<p align="center">
  <img src="\assets\blog\20260116\welsim_calculix_bc_displacement.png" alt="welsim_calculix_bc_displacement" />
</p>

The corresponding generated CalculiX solver commands are as follows:
```
** BC Name: Displacement    
*Boundary    ID_22, 1, 1, 1    
*Boundary    ID_22, 2, 2, 2    
*Boundary    ID_22, 3, 3, 3    
*Boundary    ID_22, 6, 6, 0.523599
```

### Pressure
Pressure boundary conditions are surface loads applied to structural surfaces, classified as distributed loads. Their essence is to simulate engineering scenarios involving fluid pressure, contact pressure, gas loads, etc., by specifying the normal force per unit area (e.g., internal pressure in pressure vessels, wind loads, lateral soil pressure).

Pressure is one of the most common boundary conditions in structural finite element analysis. The sign convention for pressure determines the load direction: Positive Pressure: The load direction points toward the interior of the surface, causing a compressive effect on the structure (e.g., internal pressure in pressure vessels). Negative Pressure: The load direction points away from the exterior of the surface, causing a tensile effect on the structure (e.g., atmospheric pressure on the outer wall of a vacuum vessel). 

The pressure boundary condition setup is shown in the figure below.
<p align="center">
  <img src="\assets\blog\20260116\welsim_calculix_bc_pressure.png" alt="welsim_calculix_bc_pressure" />
</p>

The corresponding generated solver commands are as follows:
```
** BC Name: Pressure    
*DLOAD    ID_20, P, 123
```

### Force
Force boundary conditions are loads applied to geometric key points, edges, or surfaces, used to simulate localized loading scenarios in engineering (e.g., bolt preload, lifting eye tension, pin forces). Force is one of the most fundamental boundary conditions in structural mechanics.

However, applying force on geometric surfaces in the finite element numerical method is non-trivial. It typically involves coupling the DOFs of multiple nodes to a single reference node, which is often used to distribute a concentrated load across a group of nodes (e.g., applying the force to the reference node, which is then automatically distributed to the coupled group).

As shown in the figure, in the force setup interface of the preprocessor, the user can select surfaces, edges, or points of the geometry and specify the force magnitudes in the three coordinate directions.
<p align="center">
  <img src="\assets\blog\20260116\welsim_calculix_bc_force.png" alt="welsim_calculix_bc_force" />
</p>

The generated solver commands for the force are as follows:
```
*COUPLING, REF NODE=46, SURFACE=ID_17, CONSTRAINT NAME=c17    
*KINEMATIC    1    3
** BC Name: Force    
*CLOAD, OP=NEW    46, 1, 100    
*CLOAD, OP=NEW    46, 2, 200    
*CLOAD, OP=NEW    46, 3, 300
```

### Nodal Force
Nodal force boundary conditions are concentrated load applied directly to single or multiple nodes. They represent the most fundamental form of load application after meshing. Nodal forces are more oriented toward direct post-meshing operations, making them suitable for refined load control or special scenario simulations.

Nodal forces are loads applied directly to the mesh nodes. The total applied force is the superposition of forces based on the number of nodes selected.
<p align="center">
  <img src="\assets\blog\20260116\welsim_calculix_bc_nodalforce.png" alt="welsim_calculix_bc_nodalforce" />
</p>

The generated solver commands are straightforward, using *CLOAD to apply loads based on the selected nodes:
```
** BC Name: Nodal Force    
*CLOAD    ID_18, 1, 10    
*CLOAD    ID_18, 2, 20    
*CLOAD    ID_18, 3, 30
** Nodal_Force
*NSET, NSET=ID_18        
82, 84, 86, 88, 95, 96, 103, 104, 107, 108,         
111, 112, 145, 146, 147, 148, 149, 150
```

### Gravity
Gravity boundary conditions fall under the category of body forces, used to simulate the effect of the Earth's gravitational field on the structure. They work by assigning an inertial force proportional to the mass to each element of the model. Gravity is applicable to almost all structural analyses involving self-weight effects (e.g., building beams and slabs, mechanical components, ground-based spacecraft conditions).

Gravity is essentially a body force induced by acceleration, and its magnitude is directly proportional to the mass of the elements. The preprocessor setup is shown in the figure below.
<p align="center">
  <img src="\assets\blog\20260116\welsim_calculix_dc_gravity.png" alt="welsim_calculix_dc_gravity" />
</p>

The generated solver commands are as follows:
```
** DC Name: Earth Gravity    
*Dload    Eall, Grav, 9.807, 0, 0, -1
```

### Rotational Velocity
Rotational velocity boundary conditions are used to simulate the scenario where a structure rotates uniformly around an axis. This condition induces centrifugal forces and Coriolis forces (which need to be considered for high-speed rotation) within the structure. Classified as inertial loads, they are widely applied in the analysis of rotating machinery (e.g., flywheels, impellers, centrifuges, turbine rotors).

The input parameters include the axis of rotation, the origin of rotation, and the magnitude of the rotational velocity. The input interface is shown in the figure below.
<p align="center">
  <img src="\assets\blog\20260116\welsim_calculix_dc_rotationalvelocity.png" alt="welsim_calculix_dc_rotationalvelocity" />
</p>

The generated solver commands are as follows:
```
** DC Name: Rotational Velocity    
*Dload    ID_21, CENTRIF, 100, 5, 5, 0, 0, 0, 1
```

## Common boundary in thermal analysis
### Temperature
In finite element thermal analysis, temperature boundary conditions are essential (Dirichlet) boundary conditions that directly define the temperature values of specific regions of the model. They are suitable for scenarios where the surface or nodal temperatures are known (e.g., the wall of a constant-temperature water tank, components in contact with a large heat source, temperature-controlled surfaces of thermal equipment).

In the heat conduction governing equation, temperature boundary conditions act as enforced constraints, directly fixing the temperature DOFs of the boundary nodes. The solver prioritizes satisfying these constraints before calculating the internal temperature field distribution. The preprocessor setup is shown in the figure below.
<p align="center">
  <img src="\assets\blog\20260116\welsim_calculix_bc_temperature.png" alt="welsim_calculix_bc_temperature" />
</p>

The generated CalculiX solver commands are as follows,
```
** BC Name: Temperature    
*Boundary, op=New    ID_23, 11, 11, 0
```

### Heat Flux
The heat flux boundary condition is a thermal load that directly defines the heat flow rate per unit area across a solid surface. It is suitable for scenarios where the heat input or output on a surface is known (e.g., the surface of an electric heater, solar collectors, walls subjected to high-temperature gas impingement).

Heat flux is a core parameter, with the positive direction indicating heat flowing into the solid and the negative direction indicating heat flowing out of the solid. The input interface is shown below.
<p align="center">
  <img src="\assets\blog\20260116\welsim_calculix_bc_heatflux.png" alt="welsim_calculix_bc_heatflux" />
</p>
The generated CalculiX solver commands are as follows:
```
** BC Name: Heat Flux    
*Dflux    ID_24, S, 0.5
```


### Body Heat Flux
Body heat flux is a volumetric thermal load used to simulate heat generation or dissipation from internal heat sources within a solid. Unlike surface heat flux boundary conditions that act on surfaces, body heat flux is applied directly to the volume elements of the model, making it suitable for temperature field analysis driven by internal heat sources.

The unit of body heat flux in the SI system is W/m³, where positive values indicate heat generation and negative values indicate heat absorption. The user input interface is shown below.
<p align="center">
  <img src="\assets\blog\20260116\welsim_calculix_dc_heat_generation.png" alt="welsim_calculix_dc_heat_generation" />
</p>

The generated CalculiX solver commands are as follows:
```
*DFLUX
ID_31,BF,10.
```

### Convection
Convection boundary conditions, also known as film boundary conditions, are used to simulate convective heat transfer between a solid surface and the adjacent fluid (gas or liquid). They are one of the most commonly used boundary conditions in engineering thermal analysis, with applications in electronic device cooling, pipe heat exchange, automotive engine cooling, and other scenarios.

The convection heat transfer coefficient is the core parameter characterizing the intensity of convective heat transfer, while the ambient temperature parameter refers to the temperature of the mainstream fluid far from the solid surface. The input interface in the preprocessor is shown below.
<p align="center">
  <img src="\assets\blog\20260116\welsim_calculix_bc_convection.png" alt="welsim_calculix_bc_convection" />
</p>

The generated CalculiX solver commands are as follows:
```
** BC Name: Convection    
*Film, op=New    
ID_29_S1, F1, 80, 123    
ID_29_S2, F2, 80, 123    
ID_29_S3, F3, 80, 123    
ID_29_S4, F4, 80, 123
```

### Thermal radiation
The radiation boundary condition is used to simulate heat transfer between a solid surface and the surrounding environment (or other solid surfaces) via thermal radiation. It is fundamentally governed by the Stefan–Boltzmann law and is suitable for heat exchange scenarios in media such as vacuum or gas (e.g., spacecraft thermal control, heat dissipation from high-temperature equipment). As a nonlinear boundary condition, the heat flux is proportional to the fourth power of the temperature, requiring iterative calculations for solution.

Users are required to input two parameters: emissivity (a value between 0 and 1) and the ambient temperature. The input interface is shown below.
<p align="center">
  <img src="\assets\blog\20260116\welsim_calculix_bc_radiate.png" alt="welsim_calculix_bc_radiate" />
</p>

The generated commands for the thermal radiation boundary condition are as follows:
```
** BC Name: Radiation    
*Radiate, op=New    
ID_30_S1, R1, 30, 0.9    
ID_30_S2, R2, 30, 0.9    
ID_30_S3, R3, 30, 0.9    
ID_30_S4, R4, 30, 0.9
```

## Conclusion
In finite element analysis, there is a wide variety of boundary conditions, which involve not only the parameters of the conditions themselves but also the selected elements or nodes. For preprocessing software, generating commands for various boundary conditions is a complex undertaking.

WELSIM is capable of setting up a comprehensive range of boundary conditions and can quickly generate the input files required by the CalculiX solver, which can be directly used for computations. Users can leverage WELSIM as a preprocessor for CalculiX. 

CalculiX also supports a small number of additional boundary conditions, such as *CONSTRAINT and *EQUATION. These were not discussed in this article as they are less frequently used in standard analyses.

The input file format of CalculiX is highly similar to that of Abaqus. Therefore, the content described in this article can also be applied to the Abaqus solver.

---

*Disclaimer: WelSim and the author are not affiliated with CalculiX or Abaqus, and have no direct relationship with the development teams or organizations behind CalculiX and Abaqus. The use of open-source software names and images herein is solely for reference in technical blog articles and software usage guidance.*
