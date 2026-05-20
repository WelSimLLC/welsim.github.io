---
lang: en
layout: post
title:  "The mesh of engineering simulation 1: data structures"
date:   2026-05-17
author: "[SimLet](https://twitter.com/getwelsim)"
---


Modern engineering simulation software is feature-rich. Being the first stage of any simulation pipeline, meshing plays a critical role across the entire software system. The functionality, stability, and efficiency of the meshing module directly impact the usability of the overall software, as meshing is intimately linked to computational functionality, 3D visualization, and human-computer interaction. This blog series will explore the meshing module in engineering simulation software from a developer’s perspective, covering mesh generation, algorithms, data structures, and specialized features. As the first article in the series, this piece discusses mesh data structures and their import/export operations.
<p align="center">
  <img src="\assets\blog\20260517\welsim_mesh_bracket_generator.png" alt="welsim_mesh_bracket_generator" />
</p>

## Data structures of finite element meshes
Finite element software connects CAD software to solvers; it takes in geometric topology data from upstream CAD models and generates meshes for downstream solvers. Thus, finite element mesh data structure must bridge the gap between the two by incorporating information from both fields. On top of that, it must support 3D mesh visualization, requiring developers to meticulously develop the underlying data structures. The most common approach is to anchor the design in geometric topology, having each geometric entity contain its lower-level constituents along with the associated finite element node and element information.
<p align="center">
  <img src="\assets\blog\20260517\welsim_mesh_db_diagram.png" alt="welsim_mesh_db_diagram" />
</p>

For example, a geometric model, named Model in the diagram above, might contain data blocks named Region, Face, Edge, and Vertex. This is essentially a simplified Boundary Representation (B-Rep) format—a method that represents solid objects using their boundaries (faces, edges, and vertices), allowing exact curved surfaces and precise topological geometry. Ranked from the highest to the lowest hierarchical level, the topology follows:

Compound -> CompSolid -> Solid -> Shell -> Face -> Loop -> Wire -> Edge -> Vertex

This is the standard B-Rep data scheme used by most CAD engines. In this hierarchy:

* A Wire differs from an Edge in that a Wire possesses curvature.
* A Loop is a closed sequence of edges that forms the boundary of a Face.
* A Shell is a connected set of Faces.
* A CompSolid consists of multiple attached Solids, representing the data format for multi-body parts. Mesh generation requires the special handling of a CompSolid to ensure that the mesh aligns perfectly along embedded faces and embedded edges. (The details of B-Rep data will be discussed in depth in future).

The mapping of individual data components is structured as follows:

* Region: Points to CompSolid and Solid geometries. It contains all geometric face information, all embedded geometric entities, and mesh volumetric element information.
* Face: Points to Face and Shell geometries. It contains all geometric edge information, the parent geometry it belongs to, embedded geometric entities, and mesh face element information (such as triangular, quadrilateral, and polygonal elements).
* Edge: Points to Wire and Edge geometries. It contains all geometric vertex information, the parent geometric faces, and the associated mesh line elements.
* Vertex: Points to Vertex geometries. It contains information about the associated geometric vertex, mesh nodes, and the parent geometric edges.

This mapping approach enables rapid queries between mesh and geometry data—such as retrieving all surface elements or nodes on a specific geometric face—which is frequently needed when applying boundary conditions in finite element analysis.

## Geometry-to-Mesh Conversions
There are two primary types of conversions from B-Rep to mesh data:

1. Tessellation/Triangulation: Converts geometry into surface meshes purely for visualization purposes.
2. Solid Meshing: Generates volumetric meshes used for both finite element computation and mesh visualization (e.g., using VTK’s unstructured grid data format).

Modern finite element software should support both of these conversions, meanwhile reverse-engineering a mesh back into a B-Rep model is rarely implemented because it is nearly impossible to achieve flawlessly. 

## Import and export of mesh data
Mesh data involves heavy traffic. Beyond supporting their own proprietary mesh formats, modern simulation software must also support universal formats. For finite element, finite volume, and spectral element meshes, widely used formats include UNV, VTU (PVTU), GMSH, EXO, CGNS, MED, and INP, each offering unique advantages.
<p align="center">
  <img src="\assets\blog\20260517\welsim_mesh_gears.png" alt="welsim_mesh_gears" />
</p>

Developers can directly leverage these formats or their corresponding SDKs to build core software data structures and handle mesh file I/O:

* UNV is a feature-rich and easy-to-use mesh format that supports a wide array of mesh elements. It allows the definition of group information (vital for boundary conditions) and supports both ASCII and Binary formats for read/write operations.
* VTU holds a natural advantage in graphical visualization. It's backed by the entire open-source VTK source code and ecosystem, making it an excellent format for mesh data I/O.

Currently, WELSIM primarily utilizes the UNV and VTU formats as its foundational mesh data structure, fully supporting data import and export for both.

As simulation software scales with additional features, developers often need to incorporate supplementary data. This includes mapping relationships between CAD topology and the mesh, hierarchical relationships for remeshing, and mesh mapping between sub-models and global models. Because these datasets vary in size, they require a flexible, compressible data format—ideally the HDF5 file format. Upon completing a mesh generation, WELSIM produces a file named s2m.h5 to store the mapping relationships between the geometric topology and the mesh.

## Conclusion
This article discussed the mesh data structures and I/O methodologies use in simulation software—establishing a proven framework for the meshing modules of general-purpose simulation platforms. It fulfills most functional requirements and adapts exceptionally well to advanced meshing features, like real-time simulation and parallel computing. Furthermore, other complex, specialized features can be successfully developed on top of this foundational data structure, such as boundary layer meshing and internal embedded surface meshing for multi-body parts.


