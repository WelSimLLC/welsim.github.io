---
lang: en
layout: post
title:  "Rigid body and dynamics in structural finite element analysis"
date:   2023-04-03
author: "[SimLet](https://twitter.com/getwelsim)"
---


Modern finite element analysis often involves multiple bodies. When the structure has strong stiffness and is not the main concern, we may regard these structures as rigid bodies. At solving, there is no need to consider its internal stress and strain distribution, which saves a lot of computing resources. In this type of analysis, these rigid bodies can be static or moving, and generate contact force on the deformable bodies. This configuration is similar to real physical conditions and has a large number of applications in large-scale engineering simulations. Meanwhile, with the rise of Metaverse, rigid body dynamics will have more applications.
<p align="center">
  <img src="\assets\blog\20230403\welsim_metaverse.png" alt="welsim_metaverse" />
</p>

There are many types of structures that can be defined as rigid bodies in simulation. For example, obstacles in automobile collision simulation, molds in die-casting of metal forming, incoming objects in high-speed impact, metal fixtures in sealing systems, solid ground in drop analysis, etc. In engineering simulation, especially in transient structural analysis, rigid bodies are widely used. Currently, WELSIM already supports the definition of rigid bodies and performs explicit dynamic simulations.
<p align="center">
  <img src="\assets\blog\20230403\car_crash_test.jpg" alt="car_crash_test" />
</p>


There are many advantages to defining rigid bodies in structural simulations:

1. Reduce computing efforts.
The rigid body no longer needs to solve its internal stress and strain, but only needs to consider the movement or rotation of the surface mesh, thus saving a lot of computing resources.

2. Simplify the pre-processing process.
A rigid body does not need to consider properties such as materials and integration points through the thickness of plate or shell elements, which can reduce the physical factors that need to be considered in pre-processing.

3. Lighten the post-processing load.
In post-processing, simplification can be done for rigid bodies. It only needs to show the displacement and rotation of the rigid body, without showing mechanical properties such as stress and strain.

Combining these advantages, in the modern structural finite element analysis, there are a large number of analysis cases of combining rigid bodies and deformable bodies. While obtaining results that conform to the physical reality, it can also simplify processing, reduce computing work, and quickly obtain solutions.

## Contact analysis with rigid bodies
Rigid bodies often involve extensive contact analysis. Although the computing methods of rigid body and deformable body are different, the contact algorithms are nearly the same. In WELSIM, the method of defining a contact pair with a rigid body is the same as a contact pair without a rigid body. It is worth noting that, depending on the algorithms, some solvers may tend to define the rigid body as a target contact surface, represented by nodes, and define the deformable body as a master contact surface, represented by element surfaces.

## Setting rigid body in WELSIM
WELSIM provides a quick way to define a rigid body. The user only needs to set the Rigid Body property from the default False to True in the property window of the geometry. In subsequent computation and processing, this geometry will be regarded as a rigid body.
<p align="center">
  <img src="\assets\blog\20230403\welsim_define_rigid_body.png" alt="welsim_define_rigid_body" />
</p>

When the structure is defined as a rigid body, WELSIM will add an extra node based on the finite element mesh to express the centroid of the body. The boundary conditions will be applied to this centroid node in the solver script. The original mesh element will be ignored in the solving for the rigid body. The surface mesh of a rigid body is considered only if contact occurs.

WELSIM has exposed the rigid body settings in version 2023R2, and at the same time supports the definition of rigid bodies for the OpenRadioss solver. The support for the rigid body will be continuously improved in future versions.

---

<small>
WelSim and the author are not affiliated with OpenRadioss. OpenRadioss is used only as a nominative reference to the open-source project and software developed and released by these teams.
</small>

<small>
WelSim is an independent engineering simulation software provider, located in Greater Pittsburgh, PA. Its flagship product WESLIM is a general-purpose engineering simulation software with an all-in-one graphical user interface and self-integrated features.
</small>


