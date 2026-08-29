---
lang: en
layout: post
title:  "The mesh of engineering simulation 4: node renumbering"
date:   2026-08-28
author: "[SimLet](https://twitter.com/getwelsim)"
---

After finite element mesh generation, node renumbering can be applied. This process does not alter the geometric coordinates; it only changes the memory storage order of the nodes. By modifying the node indexing of large sparse finite element matrices, it optimizes non-zero element distribution, bandwidth, profile, and cache hit rates - thereby reducing matrix bandwidth, memory consumption, and solver runtimes. Node renumbering does not alter the numerical simulation results, but it significantly enhances computational efficiency.
<p align="center">
  <img src="\assets\blog\20260828\welsim_mesh_renumbering_2.png" alt="welsim_mesh_renumbering_2" />
</p>


From both practical development and application perspectives, this article discusses two commonly used node renumbering algorithms: the Reverse Cuthill-McKee (RCM) algorithm and the Hilbert Space-Filling Curve algorithm. Each method has distinct advantages and is suited for different types of matrix computations. Their key features and trade-offs are summarized in the table below:

| Algorithm | Reverse Cuthill-McKee (RCM) | Hilbert |
| --- | --- | --- |
| Input Information | Topological connectivity (no coordinates required) | XYZ geometric coordinates (no element connectivity used) |
| Optimization Target | Minimum matrix bandwidth / profile | Spatial locality, CPU/GPU cache |
| Target Solvers | Direct sparse solvers (SPARSELU, MUMPS) | Iterative solvers (CG, GMRES), GPU FE |
| Multi-Disjoint-Component Performance | Robust | Degrades when components are far apart |
| Computational Overhead | BFS graph traversal (moderate) | Coordinate transformation + large array sorting (typically faster) |
| Matrix Bandwidth | Excellent | Average, often larger |
| Spatial Locality | No guarantee | Excellent |

## Reverse Cuthill-McKee (RCM) Algorithm
RCM is a classic graph reordering algorithm. When applied to FEA node renumbering, it reduces the bandwidth and profile of stiffness matrices by pulling non-zero elements closer to the main diagonal. This minimizes memory overhead during solving and boosts the performance of direct sparse solvers. Because RCM relies purely on graph topological connectivity without using spatial coordinates, geographically adjacent nodes are not necessarily indexed sequentially after reordering.

### Algorithm Flow
1. Graph Construction: Collect participating mesh nodes and construct an adjacency graph (node-node graph).
2. Pseudo-Peripheral Node Search: Locate a pair of nodes with the maximum graph distance to serve as starting points. This minimizes final bandwidth and sets the root for Breadth-First Search (BFS) traversal.
3. Cuthill-McKee BFS Traversal: Perform level-set BFS traversal to obtain an initial ordering sequence.
4. Sequence Reversal: Reverse the sequence to obtain the final RCM node ordering.

### Implementation Details
* Graph Filtering & Component Decomposition: Construct the graph using solid mesh nodes only, ignoring isolated nodes. The graph is undirected, where edges represent vertices sharing at least one element. Decompose the graph into connected components; if a model consists of multiple disconnected parts, process each connected component independently.
* Pseudo-Peripheral Node Search: The search for pseudo-peripheral nodes utilizes iterative BFS passes rather than a strict computation of the graph diameter. This engineering approximation significantly improves search traversal efficiency.
* Element Compatibility: RCM performs well on hybrid tetrahedral and hexahedral meshes. It yields optimal results for continuum meshes with high topological connectivity, but performance degrades on highly disconnected models with multiple separate components.

## Hilbert Space-Filling Curve Algorithm
Sorting nodes via a 3D Hilbert space-filling curve ensures that geographically adjacent nodes remain close in memory layout. This improves sparse matrix processing by optimizing CPU L1/L2 cache hit rates and memory bandwidth - delivering noticeable gains for iterative solvers and large-scale unstructured meshes. The Hilbert method incurs minimal memory overhead; it avoids building massive node-adjacency graphs and requires only node pointers and a small recursion stack.

### Algorithm Flow
1. Coordinate Extraction: Fetch all mesh nodes and extract their (x, y, z) spatial coordinates.
2. Bounding Box Calculation: Compute the global bounding box for the entire mesh model. Multi-part models can also be mapped directly into the same Hilbert space.
3. Octree Recursive Sorting: A 3D Hilbert curve divides a unit cube [0, 1]³ into 2³ = 8 sub-cubes, passing through them sequentially. Node sorting is implemented via an octree recursion. Instead of computing explicit integer Hilbert keys, array partitions are reordered in-place during recursive traversal.
4. Remapping: Generate a permutation array and perform global node and connectivity table remapping (identical to the post-processing phase of RCM).

### Implementation Details
This algorithm avoids generating explicit 64-bit or 128-bit Hilbert integer indices. By leveraging in-place octree recursive partitioning combined with Gray code transformations directly on node pointer arrays, it prevents large-integer overflow issues. Note that the Hilbert method does not explicitly minimize matrix bandwidth; the resulting bandwidth is often larger than that produced by RCM, making its direct solver performance generally inferior to RCM.


## Conclusion

Node reordering changes neither the underlying mathematical FEA solution, element/face IDs, nor node coordinates. It purely optimizes solving efficiency by reorganizing memory storage, producing identical simulation results. 
When selecting between these methods:
* Solver Type: Use RCM for direct solvers; use Hilbert for iterative solvers.
* Model Topology: For assemblies containing many spatially separate parts, RCM is preferred. If Hilbert must be used on such models, it is recommended to process physical parts in localized sub-domains.

Ultimately, implementations of mesh renumbering algorithms may vary; any approach that correctly and efficiently reindexes nodes while speeding up solver performance represents a robust solution.









