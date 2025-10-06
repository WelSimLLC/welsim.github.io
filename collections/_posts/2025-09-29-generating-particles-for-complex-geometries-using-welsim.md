---
lang: en
layout: post
title:  "Generating Particles for Complex Geometries Using WELSIM"
date:   2025-09-29
author: "[SimLet](https://twitter.com/getwelsim)"
---


With the development of modern engineering simulation, particle-based simulation has been increasingly adopted by the industry; the need for particle-related computations and software has emerged in various fields of engineering and science. In addition to pure particle simulation, such as molecular dynamics, there are also coupled methods with continuum approaches that enable further sophistication, like the finite element method. One example is the SPH (Smoothed Particle Hydrodynamics) method, which simulates the motion of fluids and granular materials.

As a result of this increased complexity, the demands on particle simulation are also rising which places special emphasis on particle generation specifically, as it is the first and most critical step in the entirity of the simulation. Therefore, algorithms and processes to generate particles are particularly vital. SimLet has previously discussed the numerical methods for generating particles in the article titled “Automatic Generation of Simulation Particles.”

<p align="center">
  <img src="\assets\blog\20250929\welsim_sph_demo_crank_shaft.png" alt="welsim_sph_demo_crank_shaft" />
</p>


Generating particles for simple geometric models, like cubes, is not difficult. However, when the geometry becomes more complex, particle generation becomes challenging, so currently there are not many software solutions on the market that can generate particles for arbitrary shapes. WELSIM is already capable of handling complex geometry and can even export particles as external files for use in other software. This article provides a brief introduction on how to generate particles in WELSIM.

1. Open WELSIM and Import a STEP Geometry Model

In this example, a cylindrical model with a circular hole is imported. Set the geometry’s Create Particles property to True.
<p align="center">
  <img src="\assets\blog\20250929\welsim_sph_generate_particles_geometry.png" alt="welsim_sph_generate_particles_geometry" />
</p>


2. Click the Meshing Button to Automatically Generate Particles

In this setup, 441 particles are generated.
<p align="center">
  <img src="\assets\blog\20250929\welsim_sph_generate_particles_mesh.png" alt="welsim_sph_generate_particles_mesh" />
</p>


3. Increase Particle Density

Modify the Maximum Size value in the Mesh Settings. When set to 0.01 m, the particle density increases.
<p align="center">
  <img src="\assets\blog\20250929\welsim_sph_generate_particles_mesh_settings.png" alt="welsim_sph_generate_particles_mesh_settings" />
</p>



4. Adjust Particle Display Size for Clarity

When the number of particles increases, it helps to reduce their display size for better visibility. In the 3D View of the mesh object, set the Particle Size value. Here, it is set to 0.001.
<p align="center">
  <img src="\assets\blog\20250929\welsim_sph_generate_particles_mesh_3dview.png" alt="welsim_sph_generate_particles_mesh_3dview" />
</p>


Now, a larger number of particles can be seen — 16,060 in total. Easy and efficient generation of particles at any desired density is supported by WELSIM.
<p align="center">
  <img src="\assets\blog\20250929\welsim_sph_generate_particles_mesh_denser.png" alt="welsim_sph_generate_particles_mesh_denser" />
</p>

5. Export the Particles

Once particle generation is complete, export the particle file. Right-click the Mesh object and select Export Particles from the context menu.
<p align="center">
  <img src="\assets\blog\20250929\welsim_sph_export_particles.png" alt="welsim_sph_export_particles" />
</p>


6. Once in the Export Dialog

Enter the file name and select the export format. WELSIM currently supports the VTK PolyData format; more formats will be included in future versions.
<p align="center">
  <img src="\assets\blog\20250929\welsim_sph_export_dialog.png" alt="welsim_sph_export_dialog" />
</p>


The exported file can be loaded and used by other software. For example, ParaView is used here to visualize the exported particles as shown in the image.
<p align="center">
  <img src="\assets\blog\20250929\welsim_sph_export_vtp_paraview.png" alt="welsim_sph_export_vtp_paraview" />
</p>

## Conclusion
This article outlines the steps for generating particles using WELSIM. Users simply import a geometry in STEP format, through an automatic mesh-like method, to quickly generate particles at various densities. Although a simple geometry was used here, the same process can be applied to complex models. WELSIM also allows for particle data to be exported and used in other applications. This particle generation feature is already available in version 2025R3 and will continue to be improved in future releases.


<small>
WELSIM has no direct affiliation with the author or the developers of ParaView. ParaView is referenced here purely as a technical example for demonstration purposes.
</small>

