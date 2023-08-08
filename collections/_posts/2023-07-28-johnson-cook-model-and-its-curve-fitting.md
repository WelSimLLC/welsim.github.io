---
lang: en
layout: post
title:  "Johnson-Cook model and its curve fitting"
date:   2023-07-28
author: "[SimLet](https://twitter.com/getwelsim)"
---


The Johnson-Cook constitutive and failure models were proposed by Johnson and Cook in the 1980s. Since then, they have been widely applied in the fields of impact and structural analysis. The most significant feature of the Johnson-Cook model is its simple form, which simultaneously evaluates the effects of strain hardening, strain rate strengthening, and temperature softening.
<p align="center">
  <img src="\assets\blog\20230728\deformation_chart.png" alt="deformation_chart" />
</p>

The mathematical expression of the Johnson-Cook plasticity model is as follows:
<p align="center">
  <img src="\assets\blog\20230728\johnson_cook_eqn.png" alt="johnson_cook_eqn" />
</p>



Here, **a** is the initial yield stress, measured in pressure units. The hardening constant, **b**, is also measured in pressure units. **n** is a dimensionless hardening exponent. The value of **n** determines the material's plastic flow direction and material model: (1) when n=1, the material is an ideal linear elastic material; (2) when n=0, the material is nonlinear elastic; (3) when 0 < n < 1, the material is elastoplastic. **c** and **m** are dimensionless model parameters related to strain rate and thermal softening effects, respectively. T* = (T-Tr)/(Tm-Tr) is the dimensionless temperature, where **Tr** and **Tm** are the reference temperature and the material's melting point, respectively, and **T** is the current temperature.

Parameters **a**, **b**, and **n** can be obtained from smooth round bar tensile tests (or thin-walled cylindrical tube torsion tests) conducted at a reference strain rate and reference temperature. These parameters are obtained by fitting true stress-strain data.


## Parameter fitting for the Johnson-Cook model
In practical applications, the Johnson-Cook parameters need to be obtained through parameter fitting based on the material test data. CurveFitter provides a curve-fitting formula for the Johnson-Cook plasticity model, where users simply input the plastic strain and stress values to obtain the fitted parameter values. For more details about CurveFitter, refer to the articles [An easy-to-use and free curve fitting tool — CurveFitter](https://welsim.com/2021/07/09/an-easy-to-use-and-free-curve-fitting-tool-curvefitter.html) and [The numerical methods applied in curve fitting and the updates of CurveFitter](https://welsim.com/2022/08/11/the-numerical-methods-applied-in-curve-fitting-and-the-updates-of-CurveFitter.html).
The operation is as follows:

1. Select the Johnson-Cook equation from the list on the left.
<p align="center">
  <img src="\assets\blog\20230728\curvefitter_johnson_cook.png" alt="curvefitter_johnson_cook" />
</p>

2. Import the plastic strain-stress test data in the table window on the right. After importing, the corresponding curve will be displayed in the Chart window.
<p align="center">
  <img src="\assets\blog\20230728\curvefitter_chart_johnson_cook.png" alt="curvefitter_chart_johnson_cook" />
</p>

3. Click the "Solve" button in the main window to obtain the fitted parameters. For the given data in this case, the obtained parameters are a=475.1, b=787.2, and n=0.763, with an almost perfect fit (R<sup>2</sup>=1). The Chart window shows the curve along with the test data. The two curves match well, indicating high accuracy in parameter fitting. The Output window shows the details of the curve-fitting solver's computation.
<p align="center">
  <img src="\assets\blog\20230728\welsim_curvefitter_johnson_cook_fitted.png" alt="welsim_curvefitter_johnson_cook_fitted" />
</p>


It's worth noting that curve fitting does not consider units. When using these parameters, it's vital to ensure that the stress units in the finite element software match those of the test data. Here, the test data uses MPa as the stress unit. Strain rate and temperature data are not considered in this fitting, so totally only three parameters are calculated (a, b, and n).


## Johnson-Cook failure model
In addition to the plasticity model, Johnson-Cook also has a corresponding failure model which evaluates the influence of stress, strain rate, and temperature. It is commonly used for ductile metals. The failure strain expression is as follows:
<p align="center">
  <img src="\assets\blog\20230728\failure_johnson_cook_eqn.png" alt="failure_johnson_cook_eqn" />
</p>

Here, D1-D5 are material constants. Firstly, D1-D3 can be obtained through different stress triaxiality experiments at a reference strain rate and reference temperature. The strain rate parameter D4 can be derived through different strain rate tensile tests at the reference temperature. Similarly, the temperature parameter D5 can be acquired through different temperature tensile tests at the reference strain rate. With D1~D3 known, the fitting fracture strain-temperature experimental data can yield the temperature parameter D5.


## Conclusion
The Johnson-Cook model is a plasticity and failure model applied to metal structures. Due to its simple form and a small number of unknown parameters, it is widely used in engineering. For materials without given parameters in the handbook, core parameters need to be obtained through parameter fitting of test data. CurveFitter can quickly and accurately calculate these parameters for subsequent finite element analysis.


---

<small>
WELSIM is the #1 engineering simulation software for the open-source community.
</small>
