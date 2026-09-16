---
lang: en
layout: post
title:  "The mesh of engineering simulation 5: STL meshing"
date:   2026-09-16
author: "[SimLet](https://twitter.com/getwelsim)"
---

STL is a data format for representing outer surface models. Its principle is to break down the surface of a 3D object into a large number of triangular facets. Each triangular facet stores the coordinates of three vertices and a face normal vector (pointing to the outside of the model). Curved surfaces are not represented using analytical equations; instead, they are approximated and fitted using a massive number of small triangles. Unlike parametric solid CAD data formats, STL only stores the surface, not the internal solid; it lacks units, colors, materials, textures, CAD feature history, assembly trees, and other information.
<p align="center">
  <img src="\assets\blog\20260916\wlesim_stl_bracket.png" alt="wlesim_stl_bracket" />
</p>

The data in an STL file must be a closed manifold mesh; otherwise, it cannot be used for subsequent 3D printing or finite element computation. At the same time, the vertices in STL data are stored redundantly, meaning there are no "edges," no "face ownership," no sharp angle features, and no concept of inside versus outside. This imposes certain limitations on setting boundary conditions for subsequent finite element analysis, requiring the construction of curved surfaces or sharp edges through parameterization.

STL has a vast range of use cases. For example, in 3D printing and additive manufacturing, STL is the de facto standard exchange format. 3D scanners (laser or structured light) output point clouds that are reconstructed into triangular meshes, which can be used for part replication, cultural heritage digitization, and shape inspection. In addition, it is widely used in geometric inspection, model repair, and visual preview.
<p align="center">
  <img src="\assets\blog\20260916\wlesim_stl_bracket_mesh.png" alt="wlesim_stl_bracket_mesh" />
</p>


# Mesh Generation Algorithms
STL surface mesh data cannot be directly used for finite element computation; it needs to be remeshed into high-quality volumetric meshes. There are two common classical methods: the Direct Method and the Surface Classfication Method. The main difference between these two methods is whether facet clustering is performed on the STL data. The Direct Method has a simpler workflow, performs no sharp-edge recognition, and does not repair geometric defects, but it has more stringent requirements for the watertightness of the STL data. The Surface Classfication Method supports more flexible human-computer graphic interaction operations while simultaneously splitting multiple geometric faces to support more complex models.
<p align="center">
  <img src="\assets\blog\20260916\wlesim_stl_bracket2.png" alt="wlesim_stl_bracket2" />
</p>


### Direct Method
The Direct Method involves building a single closed shell directly based on the STL surface mesh. The steps are as follows:

1.Read STL data and build the enclosure topology.

* Vertex merging (removing duplicate vertices): Each triangle in an STL file stores its vertices independently, resulting in a large number of duplicate coordinate points. Coincident vertices are merged based on a floating-point tolerance to establish a global vertex list.
* Build edge-triangle adjacency relationships: Iterate through all triangles, extract each edge, and record how many triangular facets share each edge.
* Topology checking: Identify boundary edges (belonging to only 1 triangle) and internal edges (belonging to 2 triangles); detect non-manifold edges (≥ 3 triangles sharing a single edge); check if the shell is closed: if isolated boundary edges exist, determine that the shell surface is not closed.
* Facet normal consistency check: Iterate through the facets and attempt to unify the outward normals. If the normals in the STL file are disorganized, it may lead to errors in subsequent mesh generation.
* Build shell topology: Assemble the complete boundary triangular facet data structure for subsequent meshing algorithms (such as the Advancing Front method) to read boundaries.
<p align="center">
  <img src="\assets\blog\20260916\wlesim_stl_bracket3_mesh.png" alt="wlesim_stl_bracket3_mesh" />
</p>


2.Perform 1D edge meshing, 2D surface meshing, and 3D volumetric meshing respectively. For 3D volumetric meshing, the classical Advancing Front method or parallel tetrahedral Delaunay method can be used.
3.Mesh optimization. Optimize the overall mesh by inspecting element quality. Element quality optimization removes flat "thin elements" and improves the convergence of finite element computation.


### Facet Classification Method
In many practical applications, we hope to generate a topology similar to a CAD model to make it easier to set up finite element boundary and other conditions later. In this case, the Facet Classification Method can be used to combine all facets into multiple geometric faces, effectively generating discrete B-Rep data. This process also handles complex or defective STL data better. The steps for the Facet Classification Method are as follows:

1.Read STL data and directly build the shell topology.

* Classify triangular facets based on normal angles: If the normal angle between adjacent triangles - namely the dihedral angle - is less than a threshold, they are grouped into the same smooth surface; if it exceeds the threshold, it is determined to be a sharp edge, used to capture corners.
* Determine and store the correspondence between edges and triangular facets.
* Perform classification and grouping on a large number of discrete STL triangular facets based on the surface triangular mesh's adjacency relationships, dihedral angles, curvature, and non-manifold markers. Triangles belonging to the same smooth geometric surface are categorized into one group, and the dividing boundaries (edges, non-manifold edges) are marked, outputting a set of connected facet regions.

<p align="center">
  <img src="\assets\blog\20260916\wlesim_stl_hinge.png" alt="wlesim_stl_hinge" />
</p>


2.Build discrete solid.
Based on the categorized facets, reconstruct geometric solids (faces, lines, points) to transform the discrete triangular mesh into a geometric model resembling a B-Rep. The method is to create a B-Rep geometric entity for each cluster. If high-order elements need to be created, the discrete surface can also be fitted into a UV-parameterized surface, upgrading the pure surface mesh into geometric faces or lines that can be recognized and manipulated by CAD modules.
3.Combine all outer surfaces into a closed surface loop to define a closed shell. Typically, the first surface loop is used as the outer closed shell; all subsequent incoming surface loops are internal cavities (holes), which are excavated from the outer domain. A 3D solid domain is then built on the basis of this shell to serve subsequent 3D volumetric meshing.
4.Perform 1D edge meshing, 2D surface meshing, and 3D volumetric meshing respectively. (Same as the Direct Method)
5.Mesh optimization. (Same as the Direct Method)
<p align="center">
  <img src="\assets\blog\20260916\wlesim_stl_hinge_mesh.png" alt="wlesim_stl_hinge_mesh" />
</p>

# Conclusion

This article introduced two classical methods for generating finite element meshes from STL models. Because STL data lacks topological data compared to CAD models like B-Rep, it brings more challenges to mesh generation. In practical engineering, one often encounters defective STL files - such as those that are insufficiently airtight, contain holes, non-manifold edges, self-intersections, or inverted facet normals - which further increase the difficulty of meshing and place high demands on the robustness of the mesher.

The algorithms introduced in this text can also be used to repair STL files to reduce various issues that arise during subsequent meshing. Furthermore, these algorithms can also be applied to finite element meshing for other surface models such as OBJ, 3MF, OFF, and PLY.


























After finite element mesh generation, a process called node renumbering can be applied. It only changes the order of the nodes' memory storage, not altering the geometric coordinates. By modifying the node indexing of large sparse finite element matrices, it optimizes non-zero element distribution, bandwidth, profile, and cache hit rates, which consequently reduces matrix bandwidth, memory consumption, and solver runtimes. Node renumbering does not alter the numerical simulation results, but it significantly enhances computational efficiency.
<p align="center">
  <img src="\assets\blog\20260828\welsim_mesh_renumbering_2.png" alt="welsim_mesh_renumbering_2" />
</p>


From both practical development and application perspectives, this article discusses two established node renumbering algorithms: the Reverse Cuthill-McKee (RCM) algorithm and the Hilbert Space-Filling Curve algorithm. Each method has distinct advantages, making them suitable for different types of matrix computations. Their key features and trade-offs are summarized in the table below:

| Algorithm | RCM | Hilbert |
| --- | --- | --- |
| Input Information | Topological connectivity (no coordinates required) | XYZ geometric coordinates (no element connectivity used) |
| Optimization Target | Minimum matrix bandwidth / profile | Spatial locality, CPU/GPU cache |
| Target Solvers | Direct sparse solvers (SPARSELU, MUMPS) | Iterative solvers (CG, GMRES), GPU |
| Multi-Disjoint-Component Performance | Robust | Degrades when components are far apart |
| Computational Overhead | BFS graph traversal (moderate) | Coordinate transformation and large array sorting (typically faster) |
| Matrix Bandwidth | Excellent | Average, often larger |
| Spatial Locality | No guarantee | Excellent |

## Reverse Cuthill-McKee (RCM) Algorithm
RCM is a classic graph reordering algorithm. When applied to FEA node renumbering, it reduces the bandwidth and profile of stiffness matrices by pulling non-zero elements closer to the main diagonal. This minimizes memory overhead during solving and boosts the performance of direct sparse solvers. Because RCM relies purely on graph topological connectivity and not spatial coordinates, geographically adjacent nodes are not necessarily indexed sequentially after reordering.

### Algorithm Flow
1. Graph Construction: Collect participating mesh nodes and construct an adjacency graph (node-node graph).
2. Pseudo-Peripheral Node Search: Locate a pair of nodes with the maximum graph distance to serve as starting points. This minimizes final bandwidth and sets the root for Breadth-First Search (BFS) traversal.
3. Cuthill-McKee BFS Traversal: Perform level-set BFS traversal to obtain an initial ordering sequence.
4. Sequence Reversal: Reverse the sequence to obtain the final RCM node ordering.

### Implementation Details
* Graph Filtering & Component Decomposition: Construct the graph using solid mesh nodes only, ignoring isolated nodes. The graph should be undirected, where edges represent vertices sharing at least one element. Decompose the graph into connected components; if a model consists of multiple disconnected segments, process each connected component independently.
* Pseudo-Peripheral Node Search: The search for pseudo-peripheral nodes utilizes iterative BFS passes rather than a strict computation of the graph diameter. This engineering approximation significantly improves search traversal efficiency.
* Element Compatibility: RCM performs well on hybrid tetrahedral and hexahedral meshes. It yields optimal results for continuum meshes with high topological connectivity, but performance deteriorates on highly disconnected models with multiple separate components.
<p align="center">
  <img src="\assets\blog\20260828\welsim_mesh_renumbering_1.png" alt="welsim_mesh_renumbering_1" />
</p>

## Hilbert Space-Filling Curve Algorithm
Sorting nodes via a 3D Hilbert space-filling curve allows for geographically adjacent nodes to remain close in memory layout. This improves sparse matrix processing by optimizing CPU L1/L2 cache hit rates and memory bandwidth -noticeably improving performance for iterative solvers and large-scale unstructured meshes. The Hilbert method incurs minimal memory overhead; it avoids building massive node-adjacency graphs and requires only node pointers and a small recursion stack.

### Algorithm Flow
1. Coordinate Extraction: Fetch all mesh nodes and extract their (x, y, z) spatial coordinates.
2. Bounding Box Calculation: Compute the global bounding box for the entire mesh model. Multi-part models can be mapped directly into the same Hilbert space.
3. Octree Recursive Sorting: A 3D Hilbert curve divides a unit cube [0, 1]³ into 2³ = 8 sub-cubes, passing through them sequentially. Node sorting is implemented via an octree recursion. Instead of computing explicit integer Hilbert keys, array partitions are reordered in-place during recursive traversal.
4. Remapping: Generate a permutation array and perform global node and connectivity table remapping (identical to the post-processing phase of RCM).

### Implementation Details
This algorithm avoids generating explicit 64-bit or 128-bit Hilbert integer indices. By applying in-place octree recursive partitioning combined with Gray code transformations directly on node pointer arrays, it prevents large-integer overflow issues. Note that the Hilbert method does not explicitly minimize matrix bandwidth; the resulting bandwidth is often larger than that produced by RCM, generally making its direct solver performance lower compared to RCM.


## Conclusion

Node reordering changes neither the underlying mathematical FEA solution, element/face IDs, nor node coordinates. It optimizes solving efficiency purely by reorganizing memory storage, which maintains identical simulation results. 
When selecting between these methods:
* Solver Type: Use RCM for direct solvers; use Hilbert for iterative solvers.
* Model Topology: For models containing many spatially separate parts, RCM is preferred. If Hilbert must be used on such models, it is recommended to process physical parts in localized sub-domains.

Ultimately, implementations of mesh renumbering algorithms may vary, so any approach that can correctly and efficiently reindex nodes while speeding up solver performance is a robust solution.









