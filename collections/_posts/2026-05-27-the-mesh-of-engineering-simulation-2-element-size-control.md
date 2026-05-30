---
lang: en
layout: post
title:  "The mesh of engineering simulation 2: element size control"
date:   2026-05-27
author: "[SimLet](https://twitter.com/getwelsim)"
---

Most modern engineering simulation software can perform complex meshing, making controlling mesh element size one of the most commonly used features in every operation. Categorized by specific geometric entities, common element size controls span across four levels: vertex, edge, face, and volume. A robust element size control feature helps users quickly obtain high-quality, optimized meshes, which benefits subsequent numerical computations. From a developer’s perspective, this article discusses the application and technical details on how to precisely control element size.
<p align="center">
  <img src="\assets\blog\20260527\welsim_mesh_sizing_crankshift.png" alt="welsim_mesh_sizing_crankshift" />
</p>

## Characteristic Length

Characteristic length is the most critical numerical value in mesh generation. When performing finite element meshing on a geometric shape (such as a BRep entity imported from a STEP file), we always set one or more global characteristic lengths. The most ubiquitious characteristic length is the maximum element size, which limits the size of the elements to control mesh density. Of course, algorithmically, certain characteristic lengths are internally generated. Calculating based on the geometric body’s bounding box size or curve curvature, the algorithm compares characteristic lengths at each node location and chooses the minimum value.

In practicality, due to the complexity of the geometry, users often need to manually refine the mesh at specific locations. This requires setting a local characteristic length for that area which maintains a higher priority than the global characteristic length, overriding it during the meshing process. Although the local locations chosen by users can be points, lines, or faces, these selected regions will all convert into Cartesian coordinates within the mesh space. When generating the mesh, the algorithm determines the final characteristic length size through evaluation and comparison of the current node’s position.

## Example

Taking a 3D cube model as an example, select one of the six faces and set the maximum element size of the chosen face to 0.2.
<p align="center">
  <img src="\assets\blog\20260527\welsim_mesh_sizing_selection.png" alt="welsim_mesh_sizing_selection" />
</p>

After meshing, we observe that the mesh density on and near the selected face is significantly higher than in other areas.
<p align="center">
  <img src="\assets\blog\20260527\welsim_mesh_sizing_meshed.png" alt="welsim_mesh_sizing_meshed" />
</p>

In this example, only one face was selected, but if desired users can select multiple. If dealing with an assembly model, different faces across multiple bodies can be selected. Similarly, mesh refinement can be achieved by selecting a geometric edge.
<p align="center">
  <img src="\assets\blog\20260527\welsim_mesh_sizing_meshed_edge.png" alt="welsim_mesh_sizing_meshed_edge" />
</p>

Alternatively, selecting a geometric vertex allows for local mesh refinement around that specific vertex.
<p align="center">
  <img src="\assets\blog\20260527\welsim_mesh_sizing_meshed_vertex.png" alt="welsim_mesh_sizing_meshed_vertex" />
</p>

## Conclusion
The local density of a finite element mesh depends on the characteristic length of the local elements. When multiple characteristic lengths exist in the same region, the algorithm compares them to determine the minimum characteristic length to use for meshing. For common Delaunay or Advancing Front algorithms, the characteristic length is used to determine the position of the next adjacent mesh node. Because the selected geometric entities are all converted into Cartesian spatial coordinates, there is no difference at the algorithmic level whether the front-end GUI selects a geometric face, edge, or vertex: the characteristic length is always determined based on the spatial position of each node.


