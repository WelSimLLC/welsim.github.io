---
lang: en
layout: post
title:  "Methods for Automatic Particle Generators"
date:   2025-08-20
author: "[SimLet](https://twitter.com/getwelsim)"
---


Modern engineering simulation software is not only capable of analyzing continuous domains, for instance, using the finite element method (FEM) to compute structures, fluids, or electromagnetic fields, but it also has enough computational process for discontinuous particle systems. Examples include pure particle molecular dynamics, discrete element methods (DEM), smoothed particle hydrodynamics (SPH), and coupled simulations with FEM. The primary prerequisite to compute particle systems is having the ability to generate particles within a model, including data of the particle positions, shapes, and volumes. This is similar to how in finite element analysis, a mesh containing nodes and element information must first be created.
<p align="center">
  <img src="\assets\blog\20250820\welsim_sph_analysis.png" alt="welsim_sph_analysis" />
</p>


When simulating particle systems, the first step is to generate the position, size, and shape of the particles. Thus, the particle generator becomes a critical component of the entire analysis system. A good particle generator should be able to quickly produce initial-state particles and generate particles according to various shapes and boundary conditions. Common automated particle generation methods are lattice structures, finite element mesh conversion, and network growth. This article discusses these well-known particle generation methods for SPH systems and their implementation mechanisms.


## Lattice Structures
Lattice-based generation is particularly suitable for microscale materials. Typical structures include FCC (face-centered cubic) and BCC (body-centered cubic) lattices, which are often found in crystalline materials. Once the initial lattice structure is defined, the particle generator replicates this structure to fill the entire region.
<p align="center">
  <img src="\assets\blog\20250820\welsim_lattice_types.png" alt="welsim_lattice_types" />
</p>

For this method of particle generation, the user needs to provide the boundary of the simulation domain (usually a bounding box), the particle type within each lattice, and the spacing between particles. Algorithmically, this is a straightforward approach, so it is widely applied in molecular dynamics and similar particle-based simulations.


## Finite Element Mesh Conversion
A finite element mesh consists of nodes and elements; the element types vary depending on the model. Instances include tetrahedral and hexahedral solid meshes, as well as triangular and quadrilateral surface meshes. Since meshes can represent irregular geometries, the irregular shape stays captured once converting them into particles. In particle systems coupled with FEM, this particle generation approach allows for convenient coupling with finite element computations, as commonly seen in particle-FEM and SPH analyses.
<p align="center">
  <img src="\assets\blog\20250820\welsim_mesh_to_particles.png" alt="welsim_mesh_to_particles" />
</p>


The general procedure for converting a mesh into particles involves calculating the centroid of each element and its characteristic size. These values determine the position and size of each particle. In principle, each finite element corresponds to one particle. However, because FEM meshes may be non-uniform, it may cause the resulting particle distribution to be uneven. Additional integration may be required to refine the generated particles, and boundary particles may also require special marking to enable the addition of boundary conditions in later simulations. In computational fluid dynamics (CFD), particles can also enter the simulation domain continuously through specified inflow boundaries. Currently, WELSIM supports particle generation from finite element meshes.


## Network-Based Generation
Another common particle generation method is based on network growth, often implemented with tree and branching algorithms. Starting from an initial trunk structure, branches are allowed to grow within a fixed region according to specific rules, generating new branches (particles). By providing parameters such as a starting point, second point, segment length, gradient, and initial shape, particles can be generated iteratively. This is how new branches are created. Typically, if a new branch is too close to an existing one or belongs to the same parent particle, it is discarded. This approach incorporates randomness through stochastic processes, resulting in particle distributions with a degree of variability.
<p align="center">
  <img src="\assets\blog\20250820\welsim_network_growth.png" alt="welsim_network_growth" />
</p>


## Conclusion
This article introduced conventionally used automated particle generation methods in simulation software. For FEM-related software, mesh-to-particle conversion is particularly practical, as the generated particles can be directly applied to FEM-coupled simulations. The general-purpose FEM software WELSIM already supports mesh-to-particle conversion, and users are able to export the generated particles to utilize in other analyses.



