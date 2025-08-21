---
lang: en
layout: post
title:  "Methods for Automatic Particles Generators"
date:   2025-08-20
author: "[SimLet](https://twitter.com/getwelsim)"
---


Modern engineering simulation software not only provides capabilities for analyzing continuous domain, such as using the finite element method (FEM) to compute structures, fluids, or electromagnetic fields, but also has enhanced computational power for discontinuous particle systems. Examples include pure particle molecular dynamics, discrete element methods (DEM), smoothed particle hydrodynamics (SPH), as well as coupled simulations with FEM. The primary prerequisite for computing particle systems is the ability to generate particles within a model, including data such as particle positions, shapes, and volumes. This is similar to finite element analysis, where a mesh containing nodes and element information must first be created.
<p align="center">
  <img src="\assets\blog\20250820\welsim_sph_analysis.png" alt="welsim_sph_analysis" />
</p>


When simulating particle systems, the first step is to generate the position, size, and shape of the particles. Thus, the particle generator becomes a critical component of the entire analysis system. A good particle generator can not only quickly produce initial-state particles but also generate particles according to various shapes and boundary conditions. Common automated particle generation methods include lattice structures, network growth, and finite element mesh conversion. This article discusses commonly used particle generation methods for SPH systems and their implementation mechanisms.


## Lattice Structures
Using lattice-based generation is one of the most common methods, particularly suitable for microscale materials. Typical structures include FCC (face-centered cubic) and BCC (body-centered cubic) lattices, which are often found in crystalline materials. Once the initial lattice structure is defined, the particle generator replicates this structure and fills the entire region.
<p align="center">
  <img src="\assets\blog\20250820\welsim_lattice_types.png" alt="welsim_lattice_types" />
</p>

For this type of particle generation, the user needs to provide the boundary of the simulation domain (usually a bounding box), the particle type within each lattice, and the spacing between particles. Algorithmically, this is a straightforward approach and is widely applied in molecular dynamics and similar particle-based simulations.


## Finite Element Mesh Conversion
A finite element mesh consists of nodes and elements, and the element types vary depending on the model. Representative examples include tetrahedral and hexahedral solid meshes, as well as triangular and quadrilateral surface meshes. Since meshes can represent irregular geometries, converting them into particles can also capture irregular shapes. In particle systems coupled with FEM, this particle generation method allows convenient coupling with finite element computations, as commonly seen in particle-FEM and SPH analyses.
<p align="center">
  <img src="\assets\blog\20250820\welsim_mesh_to_particles.png" alt="welsim_mesh_to_particles" />
</p>


The common method for converting a mesh into particles involves calculating the centroid of each element and its characteristic size. These values determine the position and size of each particle. In principle, each finite element corresponds to one particle. However, because FEM meshes may be non-uniform, the resulting particle distribution may also be uneven. Additional homogenization may be required to refine the generated particles. Boundary particles may also require special marking to facilitate the application of boundary conditions in later simulations. For example, in computational fluid dynamics (CFD), particles may continuously enter the simulation domain through specified inflow boundaries. WELSIM already supports the functionality of generating particles from finite element meshes.


## Network-Based Generation
Another commonly used particle generation method is based on network growth, often implemented with tree and branching algorithms. Starting from an initial trunk structure, branches are allowed to grow within a fixed region according to specific rules, generating new branch (particles). By providing parameters such as the starting point, second point, segment length, gradient, and initial shape, particles can be generated iteratively. The principle of this method is how new branches are created. Typically, if a new branch is too close to an existing one or belongs to the same parent particle, it is discarded. This method incorporates randomness through stochastic processes, resulting in particle distributions with a degree of variability.
<p align="center">
  <img src="\assets\blog\20250820\welsim_network_growth.png" alt="welsim_network_growth" />
</p>


## Conclusion
This article introduced commonly used automated particle generation methods in simulation software. For FEM-related software, mesh-to-particle conversion is particularly practical, as the generated particles can be directly applied to FEM-coupled simulations. The general-purpose FEM software WELSIM already supports mesh-to-particle conversion, and users can also export the generated particles for use in other types of analyses.



