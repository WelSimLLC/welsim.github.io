---
lang: en
layout: post
title:  "The numerical methods applied in curve fitting and the updates of CurveFitter"
date:   2022-08-11
author: "[SimLet](https://twitter.com/getwelsim)"
---


With the development of big data and computational science, data mining and analysis tools play an increasingly important role. For general two-dimensional curve and three-dimensional surface data, through the given curve/surface equations and parameters, complex data can be expressed with simplified and abstract functions, and relevant important information can be extracted quickly. At present, curve fitting has been widely used in engineering and scientific research, involving sociology, medicine, engineering, biology, and many other fields.

<p align="center">
  <img src="\assets\blog\bigdata_01.jpg" alt="welsim_big_data" />
</p>

WELSIM released the free tool CurveFitter two years ago, which has received a lot of praise and popularity. The earliest version of CurveFitter was developed to compute test data-curve fits for hyperelastic materials in structural mechanics, and data-curve fits for energy losses in magnetic materials. After that, many general curves are added per users’ requirements, such as polynomial, power function, exponential function, and so on. Most of these curves are nonlinear, and the corresponding parameters can be obtained quickly and accurately only by computing.


## Least Squares

The least squares method is the most commonly used method in solving curve fitting and optimization. The core of the algorithm is to find the global minimum of the function within a given set of data. By linearizing at each step size and constructing a Jacobian matrix, a linear equation system with parameters as independent variables is obtained, and the parameter values ​​we need are obtained when the solution converges.

<p align="center">
  <img src="\assets\blog\curvefitter_gui.png" alt="welsim_curvefitter_gui" />
</p>

The general approach when solving non-linear optimization and curve fitting problems is to solve a sequence of approximations to the original problem. At each iteration, the approximation is solved to determine a correction step size vector. In order to converge faster and more accurately, the control of the step size is particularly important. Line search methods are in some sense dual to trust region methods: trust region methods first choose a step size and then a step direction while line search methods first choose a step direction and then a step size. Usually, for curve fitting problems that are not computationally expensive, the trust region method is a better choice.


## Levenberg-Marquardt algorithm

The Levenberg-Marquardt algorithm (LMA) is the most commonly used method for solving the nonlinear least squares method. The LMA was developed in the early 1960s as a trust region method for solving nonlinear least squares problems. The LMA combines two numerical minimization algorithms: Gradient Descent method and Gauss-Newton method. In the Gauss-Newton method, the sum of the squared errors is reduced by assuming the least squares function is locally quadratic in the parameters and finding the minimum of this quadratic. The LMA acts more like a gradient-descent method when the parameters are far from their optimal value, and acts more like the Gauss-Newton method when the parameters are close to their optimal value[1].

In addition to the LM method, the Dogleg method is also a commonly used method for computing trust region optimization problems. Unlike LMA, the dogleg method computes two vectors about the step size. The advantage of the dogleg method is that it does not need to be calculated from scratch, and the radius of the trust region is small. The dogleg method can generally only use the direct method (factorization) to solve the linear equation system Ax=b.

## Updates from CurveFitter

Recently, CurveFitter, a free software tool developed by WELSIM, has undergone many upgrades. These include:

1. Support multi-core parallel computing. For a large amount of test data, curve fitting is processed quickly.
2. Support user input of solver options, such as the maximum number of iterations, function tolerance value, etc. Currently, the solver control options supported are:
**Maximum number of iterations**: the maximum number of iterations of the solver. If this value is exceeded, it will not be determined to converge. The default value is 100.
**Function tolerance**: The critical value used to judge the change of the objective function value. Convergence is judged when it is less than this value. Defaults to 1e-9.
**Gradient tolerance**: The critical value used to judge the maximum norm. Defaults to 1e-10.
**Parameter tolerance**: the critical value used to judge the step size parameter. Defaults to 1e-8.

<p align="center">
  <img src="\assets\blog\curvefitter_solver_options.png" alt="welsim_curvefitter_solver_options" />
</p>

3. Added 1st-6th Schulz-Flory functions.
The Schulz-Flory function has been widely applied to describe the polymerization of various complex materials. The governing equation is as follows:

<p align="center">
  <img src="\assets\blog\eq_schulz_flozy.png" alt="welsim_eq_schulz_flozy" />
</p>

It can be seen that this equation is highly nonlinear and has high requirements for curve fitting algorithms.

<p align="center">
  <img src="\assets\blog\schulz_flozy_list.png" alt="welsim_curvefitter_schulz_flozy_list" />
</p>

4. A lot of software optimizations and enhancements.

At present, CurveFitter already supports a variety of nonlinear curve fittings, and more curves will be added in the future to fulfill the needs of users. Curvefitter can be downloaded from WELSIM’s official website and used for free.

## Reference
[1] Henri P. Gavin, 2020, The Levenberg-Marquardt algorithm for nonlinear least squares curve-fitting problems.


******

<small>
[WelSimulation LLC](https://welsim.com) is an independent engineering simulation technology provider, located in Greater Pittsburgh, PA. Its flagship product WESLIM is a general-purpose engineering simulation software with an all-in-one graphical user interface and self-integrated features.
</small>
