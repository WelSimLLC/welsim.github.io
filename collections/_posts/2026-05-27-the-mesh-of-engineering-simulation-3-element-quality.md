---
lang: en
layout: post
title:  "The mesh of engineering simulation 2: element quality"
date:   2026-07-20
author: "[SimLet](https://twitter.com/getwelsim)"
---


In simulation software such as Finite Element Analysis (FEA) tools, mesh quality is critical to the computation. High-quality elements improve computational speed, whereas low-quality elements compromise accuracy or may even fail the computation. Common metrics for evaluating element quality include aspect ratio, Jacobian ratio, maximum corner angle, parallel deviation, skewness, characteristic length, orthogonal quality, and warping factor. This article discusses these common mesh (element) quality parameters from the perspectives of practical application and software development.


## Aspect Ratio
The aspect ratio describes the elongation of an element. It is defined as the ratio of the longest edge to the shortest edge, indicating whether the element is excessively elongated. Elongated elements fail to accurately capture gradients along their short-edge direction, leading to significant errors in bending and boundary layer stress calculations. The ideal value is 1; higher values ​​indicate poorer element quality. Aspect ratios are useful for checking meshes in boundary layers, thin-walled structures, and stretched regions.
<p align="center">
  <img src="\assets\blog\20260720\welsim_mesh_aspect_ratio_3d.png" alt="welsim_mesh_aspect_ratio_3d" />
</p>


For general models, the overall aspect ratio should be less than 20, and less than 10 in areas of stress concentration. When the aspect ratio exceeds 20, elements become severely stretched, resulting in poor FEA accuracy and convergence difficulties. In CFD boundary layer regions where the mesh is refined in the normal direction, aspect ratios between 30 and 100 are permissible.

The numerical methods for calculating aspect ratios are straightforward. For triangles, the aspect ratio is the ratio of the longest edge to the diameter of the equivalent inscribed circle. For quadrilaterals, it is the ratio of the average lengths of the two pairs of opposite edges: max(L1, L2) / min(L1, L2). Tetrahedra are treated similarly to triangles, with the aspect ratio derived from the ratio of the inscribed sphere radius (r) to the circumscribed sphere radius (R). For hexahedra, the aspect ratio is the ratio of the maximum to the minimum length among the 12 edges. As these methods demonstrate, the aspect ratio is a purely geometric length-based calculation that does not utilize Gaussian points or Jacobian determinants.


## Jacobian Ratio
The Jacobian ratio is the ratio of the minimum Jacobian determinant to the maximum Jacobian determinant within an element. The Jacobian uniformity metric reflects distortion gradients and measures the uniformity of the mapping within an element. It is specifically designed to capture nodal distortion and local contraction or expansion in high-order elements, serving as a core quality control indicator for higher-order elements. The value ranges from -1 to 1; a ratio of 1 indicates a uniform, undistorted element, while values ​​closer to zero indicate significant distortion. The empirical standards are as follows:

| Jacobian Ratio | 0.3–1.0 | 0.1–0.3 | 0–0.1 | ≤ 0 |
| Element Quality | High-quality element; stable solution | Distorted; reduced stress accuracy; prone to oscillation | Severely distorted; not recommended for high-precision calculations | Negative Jacobian / Degenerate; solver error | 

There are two standards for calculating the Jacobian ratio, based respectively on Gaussian points and corner nodes. The Gaussian point method aligns with the integration locations of the solver's stiffness matrix, making it a reliable mesh metric for the finite element method. The corner node method checks only geometric vertices; while computationally efficient, it may fail to detect cases where vertices are positive but integration points are negative, so it is typically used for rapid geometric screening.
<p align="center">
  <img src="\assets\blog\20260720\welsim_mesh_jacobian_2d.png" alt="welsim_mesh_jacobian_2d" />
</p>



For linear elements, the Jacobian determinant is constant throughout the element, and the Jacobian ratio remains consistently 1, failing to reflect the element's quality. In this case, comparing the element's Jacobian determinant against that of an ideal element yields a Jacobian ratio that is not constant at 1. Additionally, since the Jacobian determinant is constant within the element, the calculation needs to be performed only once per linear element, without iterating through all nodes or Gaussian points.
For nonlinear elements - such as second-order elements with midside nodes or higher-order elements - shape functions are of higher degree. Consequently, the Jacobian matrix varies across different integration points within the element, requiring dynamic calculation by substituting coordinates at each integration point.


## Maximum Corner Angle
The maximum corner angle is an intuitive metric for assessing element quality, capable of identifying elements with extremely obtuse angles or those that are nearly flat (degenerate). The maximum angle within the element is reported, typically in degrees. A larger value indicates more severe element distortion; values ​​closer to the ideal equiangular state are preferable. The optimal angle for a quadrilateral is 90° (a right angle), while for a triangle, it is 60°; angles exceeding 150° indicate a poor-quality element. Elements with angles exceeding 165° are not recommended for solver.
<p align="center">
  <img src="\assets\blog\20260720\welsim_mesh_max_corner_angle_2d.png" alt="welsim_mesh_max_corner_angle_2d" />
</p>

Angles (measured in degrees) can be calculated using the formula: θ = arccos(u·v/(\|u\|·\|v\|))·180/π, where u and v represent the vectors of the two sides forming the angle. For a triangular element, the angles θ0, θ1, and θ2 at the three vertices are calculated; the maximum value among them - max{θ0, θ1, θ2} - is defined as the maximum corner angle. Similarly, the maximum corner angle of a quadrilateral element is max{θ0, θ1, θ2, θ3}.

For 3D elements, the maximum corner angle of the element is determined by identifying the maximum corner angle on each face and then comparing these values. For a tetrahedral element, which has four triangular faces (each with three interior angles), the maximum of all 12 interior angles is taken. A hexahedral element has six quadrilateral faces (each with four vertex angles); by evaluating all 24 angles across these faces, the maximum corner angle of the hexahedron is obtained.


## Skewness
Skewness describes the tilt and distortion of an element, measuring the extent to which a quadrilateral or hexahedron deviates from a perfect rectangle or cube. It is a normalized, comprehensive metric that penalizes both excessively large and excessively small angles. As a key indicator of element quality for finite element solvers, it is one of the most commonly used general metrics. The value ranges from 0 to 1: a value of 0 indicates an ideal, orthogonal, and perfectly regular element, while a value of 1 indicates a completely skewed element unsuitable for finite element analysis. Generally, values ​​below 0.2 indicate high-quality elements, and values ​​below 0.5 are acceptable. Values ​​above 0.8 indicate poor element quality, leading to reduced numerical accuracy, convergence difficulties in iterative calculations, and potential stress singularities.
<p align="center">
  <img src="\assets\blog\20260720\welsim_mesh_skewness_2d.png" alt="welsim_mesh_skewness_2d" />
</p>


The general calculation method for skewness is as follows:
S = max{ (θmax − θideal) / (180 − θideal), (θideal − θmin) / θideal }
Here, θmax is the maximum corner angle, θmin is the minimum interior angle, and θideal is the ideal interior angle. The ideal internal angle for a triangle is 60°, and for a quadrilateral, it is 90°; the ideal dihedral angle for a tetrahedron is approximately 70.5°, while for a hexahedron, it is 90°. For 3D elements such as tetrahedra and hexahedra, skewness is calculated using the maximum or minimum dihedral angle. This method, also known as the equiangular method, supports all element types, including prisms and pyramids.

For triangular and tetrahedral elements, skewness can also be calculated using the equi-volume method. The formula is: S = (V_ideal - V_actual) / V_ideal, where V_ideal is the volume of a standard equilateral element sharing the same circumsphere.

For pyramid and wedge elements, equiangular skewness is calculated for all quadrilateral faces and equi-volume skewness for all triangular faces; the maximum value obtained is taken as the skewness.


## Element Quality
Element quality is a comprehensive metric for evaluating mesh quality, with values ​​ranging from 0 to 1. A value of 1 represents a perfect square (2D) or a perfect cube (3D), while a value of 0 indicates zero volume or negative volume (indicating mesh distortion failure).
<p align="center">
  <img src="\assets\blog\20260720\welsim_mesh_element_quality_2d.png" alt="welsim_mesh_element_quality_2d" />
</p>


The metric is calculated as follows: For 2D quadrilateral or triangular elements, the calculation uses the ratio of the element area to the sum of the squares of the edge lengths: Q = C * (A / ΣL²). The area of ​​a triangular element can be obtained as half the magnitude of the vector cross product. Quadrilateral elements can be divided into two adjacent triangles to calculate their area.

For 3D elements, the calculation uses the ratio of the element volume to the square root of the cube of the sum of the squares of the edge lengths: Q = C * (V / (ΣL²)^1.5). The volume of a 3D element can be determined by calculating the determinant of the element's Jacobian matrix. The value of constant C depends on the element type, as specified below:

| Element | Triangle | Quadrilateral | Tetrahedron | Hexahedron | Wedge | Pyramid |
| Constant Value | 6.928 | 4.0 | 124.70 | 41.57 | 62.354 | 96 |

In element quality assessment, a quality value greater than 0.7 indicates an acceptable element; for elements in stress concentration zones, a value greater than 0.8 is desirable. Elements with values ​​below 0.05 are considered severely defective and must be repaired.


## Conclusion
This article discusses the quality of common element types; calculating and visualizing element quality is an essential feature of modern general-purpose finite element analysis software. These quality metrics are used not only for finite element meshing but also for interactive mesh inspection. By visualizing element quality via contour plots, users can quickly and intuitively assess mesh quality and decide whether to use the current mesh for subsequent calculations.

Although this article does not discuss triangular prism elements or wedge elements in detail, their quality metrics are calculated similarly to those of tetrahedral and hexahedral elements and can be determined using the same methods. Other quality metrics - such as parallel deviation, orthogonal quality, and warping factor - are not addressed here.



