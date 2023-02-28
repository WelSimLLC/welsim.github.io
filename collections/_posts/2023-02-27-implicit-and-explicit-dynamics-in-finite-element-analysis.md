---
lang: en
layout: post
title:  "Implicit and explicit dynamics in finite element analysis"
date:   2023-02-27
author: "[SimLet](https://twitter.com/getwelsim)"
---

There are a large number of transient problems in the fields of engineering simulation and scientific computing, which requires appropriate time solvers to obtain solutions effectively and efficiently. Nowadays, we often classify numerical time solvers  into two categories: implicit method and explicit method. Both methods have been supported in the structural simulation module of WELSIM. This article will discuss the basics and respective advantages of these two numerical methods.

<p align="center">
  <img src="\assets\blog\20230227\implicit_vs_explicit.jpeg" alt="implicit_vs_explicit" />
</p>


## Implicit dynamics method
The implicit method is a commonly used method in transient problem simulation. Thanks to the advantages in computational speed and numerical accuracy, implicit has been widely used in general simulations. The most notable feature of the implicit method is to construct and solve the ax=b linear algebra equations in each time step. If the governing equation contains nonlinear factors, a nonlinear solver such as a Newton iterative solver will also be applied. Therefore the implicit method is relatively complicated, it requires more computer memory and more complex software programming. Especially the parallel implementation is more complicated. The implicit method is the default transient solver in WELSIM. For highly nonlinear models, the Newton solver may experience solving difficulties and fail to converge. The advantage of implicit is that there is no need to consider numerical stability, and the time step can be set to a larger value, since the implicit time solvers are unconditionally stable. Besides, various residual convergence criteria ensure computational precision. The common implicit time solvers include Newmark, Hilber-Hughes-Taylor (HHT), Crank-Nicolson, etc.
<p align="center">
  <img src="\assets\blog\20230227\welsim_ball_rebounce.jpeg" alt="welsim_ball_rebounce" />
</p>

## Explicit dynamics method
The explicit method is simpler in terms of algorithm, and there is no need to construct linear algebra matrix equations, so there is no need to solve a large ax=b linear algebra equation system. For nonlinear problems, there is no need to use a nonlinear solver, and everything is calculated by a time solver. The explicit method is relatively simple to calculate, relatively easy to program and implement, and requires less hardware memory space. Moreover, it has natural advantages for parallel computing. It can achieve a good speed-up for parallel frameworks such as OpenMP, MPI, or GPU. It has a great convergence advantage for high-speed and high-rate-varying problems. However, the disadvantage is that a small time step must be used to meet the requirement of numerical stability. Common explicit solvers include: Runge-Kutta, central difference method, etc. Using the explicit method in WELSIM is straightforward, you only need to set the Explicit property to true and configure the OpenRadioss.
<p align="center">
  <img src="\assets\blog\20230227\explicit_welsim.png" alt="explicit_welsim" />
</p>


## Conclusion
Implicit and explicit are two completely different computational methods that determine different advantages in terms of applications. In general, for large rate change problems, such as large strain-rate problems in structural analysis, high-speed impact, and explosion problems, the explicit method has better solving capabilities. For strongly nonlinear problems, explicit methods can also be applied when the implicit solver fails to converge. However, due to the small time step, the overall computation of the explicit solver takes a long physical time. It is hoped that with the popularization of GPU clusters, the computational time can be significantly reduced through parallel computing. In addition, the accuracy of the explicit method is relatively low, compared with the implicit method.
Currently, the best open-source explicit dynamics solver is OpenRadioss, which is fully functional and supports a large number of material models. WELSIM also uses OpenRadioss as the default explicit dynamics solver. For details, see the article "Run OpenRadioss solver for explicit dynamics analysis using WELSIM". At the same time, the free software MatEditor also supports the generation of OpenRadioss material texts. For details, see the article "Using MatEditor to generate OpenRadioss material data files".


---
<small>
WelSim and the author are not affiliated with the Altair or OpenRadioss team. OpenRadioss is used only as nominative references to the open-source project and software developed and released by the OpenRadioss team.
</small>

<small>
WelSimulation LLC is an independent engineering simulation technology provider, located in Greater Pittsburgh, PA. Its flagship product WESLIM is a general-purpose engineering simulation software with an all-in-one graphical user interface and self-integrated features.
</small>

