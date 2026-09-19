---
lang: en
layout: post
title:  "The mesh of engineering simulation 5: STL meshing"
date:   2026-09-16
author: "[SimLet](https://twitter.com/getwelsim)"
---

STL is a data format for representing outer surface models. It breaks down the surface of a 3D object into a large number of triangular facets. Each triangular facet stores the coordinates of three vertices and a unit normal vector (pointing outward from the model). Curved surfaces are not represented using analytical equations; instead, they are approximated and fitted using a massive number of small facets. Unlike parametric solid CAD data formats, STL only stores the surface and not the internal solid, as it lacks units, colors, materials, textures, CAD feature history, assembly trees, and other information.
<p align="center">
  <img src="\assets\blog\20260916\wlesim_stl_bracket.png" alt="wlesim_stl_bracket" />
</p>

The data in an STL file must be a closed manifold mesh—otherwise, it cannot be used for subsequent 3D printing or finite element computation. However, the vertices in STL data are stored redundantly, meaning there are no "edges," no "face ownership," no sharp angle features, and no concept of inside versus outside. This imposes certain limitations when setting boundary conditions for future finite element analysis, requiring the construction of curved surfaces or sharp edges through parameterization.

STL has a vast range of use cases. For example, in 3D printing and additive manufacturing, STL is the de facto standard exchange format. 3D scanners (laser or structured light) output point clouds that are reconstructed into triangular meshes, which can be used for part replication, cultural heritage digitization, and shape inspection. Moreover, it is widely used in geometric inspection, model repair, and visual preview.
<p align="center">
  <img src="\assets\blog\20260916\wlesim_stl_bracket_mesh.png" alt="wlesim_stl_bracket_mesh" />
</p>


# Mesh Generation Algorithms
STL surface mesh data cannot be directly used for finite element computation, as it needs to be remeshed into high-quality volumetric meshes. Typically, there are two classical methods: the Direct Method and the Facet Classification Method. The main difference between these two methods is whether facet clustering is performed on the STL data. The Direct Method has a simpler workflow, performs no sharp-edge recognition, and does not repair geometric defects, but the watertightness of the STL data follows more stringent requirements. The Facet Classification Method supports more flexible human-computer graphic interaction operations while simultaneously splitting multiple geometric faces to support more complex models.
<p align="center">
  <img src="\assets\blog\20260916\wlesim_stl_bracket2.png" alt="wlesim_stl_bracket2" />
</p>


### Direct Method
The Direct Method involves building a single closed shell directly based on the STL surface mesh. The steps are as follows:

1.Read STL data and build the enclosure topology.

* Vertex merging (removing duplicate vertices): Each triangle in an STL file stores its vertices independently, resulting in a large number of duplicate coordinate points. Coincident vertices are merged based on a floating-point tolerance to establish a global vertex list.
* Build edge-triangle adjacency relationships: Iterate through all triangles, extract each edge, and record how many triangular facets share each edge.
* Topology checking: Identify boundary edges (belonging to only 1 triangle) and internal edges (belonging to 2 triangles); detect non-manifold edges (≥ 3 triangles sharing a single edge). Check if the shell is closed: if isolated boundary edges exist, determine that the shell surface is not closed.
* Facet normal consistency check: Iterate through the facets and attempt to unify the outward normals. If the normals in the STL file are disorganized, it may lead to errors in ensuing mesh generation.
* Build shell topology: Assemble the complete boundary triangular facet data structure for subsequent meshing algorithms (such as the Advancing Front method) to read boundaries.
<p align="center">
  <img src="\assets\blog\20260916\wlesim_stl_bracket3_mesh.png" alt="wlesim_stl_bracket3_mesh" />
</p>


2.Perform 1D edge meshing, 2D surface meshing, and 3D volumetric meshing respectively. For 3D volumetric meshing, the classical Advancing Front method or parallel tetrahedral Delaunay method can be used.
3.Mesh optimization. Optimize the overall mesh by inspecting element quality. Element quality optimization removes flat "thin elements" and improves the convergence of finite element computation.


### Facet Classification Method
In many practical applications, we hope to generate a topology similar to a CAD model to facilitate setting up finite element boundary and other conditions later. In this case, the Facet Classification Method can be used to combine all facets into multiple geometric faces, effectively generating discrete B-Rep data. This method also handles complex or defective STL data better. The steps for the Facet Classification Method are as follows:

1.Read STL data and directly build the shell topology.

* Classify triangular facets based on normal angles: If the normal angle between adjacent triangles - namely the dihedral angle - is less than the threshold, they are grouped into the same smooth surface. If it exceeds the threshold, it is determined to be a sharp edge and used to capture corners.
* Determine and store the correspondence between edges and triangular facets.
* Perform classification and grouping on a large number of discrete STL facets using the surface mesh's adjacency relationships, dihedral angles, curvature, and non-manifold markers. Triangles belonging to the same smooth geometric surface are categorized into one group, and the dividing boundaries (edges, non-manifold edges) are marked. The output is a set of connected facet regions.

<p align="center">
  <img src="\assets\blog\20260916\wlesim_stl_hinge.png" alt="wlesim_stl_hinge" />
</p>


2.Build discrete solid.
Based on the categorized facets, reconstruct geometric solids (faces, lines, points) to transform the discrete triangular mesh into a geometric model resembling a B-Rep. The aim is to create a B-Rep geometric entity for each cluster. If high-order elements need to be created, the discrete surface can be fitted into a UV-parameterized surface. This upgrades the pure surface mesh into geometric faces or lines that can be recognized and manipulated by CAD modules.
3.Combine all outer surfaces into a closed surface loop to define a closed shell. Typically, the first surface loop is used as the outer closed shell, and all subsequent surface loops are internal cavities (holes), which are excavated from the outer domain. A 3D solid domain is then built on the basis of this shell to serve future 3D volumetric meshing.
4.Perform 1D edge meshing, 2D surface meshing, and 3D volumetric meshing respectively. (Same as the Direct Method)
5.Mesh optimization. (Same as the Direct Method)
<p align="center">
  <img src="\assets\blog\20260916\wlesim_stl_hinge_mesh.png" alt="wlesim_stl_hinge_mesh" />
</p>

# Conclusion

This article introduced two classical methods for generating finite element meshes from STL models. Unlike CAD models like B-Rep, STL data lacks topological data, considerably complicating mesh generation. In practical engineering, one often encounters defective STL files—such as those that are insufficiently airtight, contain holes, non-manifold edges, self-intersections, or inverted facet normals—which further increase the difficulty of meshing and place high demands on the robustness of the mesher.

The algorithms introduced in this text can also be used to repair STL files and reduce various issues that arise during subsequent meshing. Furthermore, these algorithms can also be applied to finite element meshing for other surface models such as OBJ, 3MF, OFF, and PLY.
