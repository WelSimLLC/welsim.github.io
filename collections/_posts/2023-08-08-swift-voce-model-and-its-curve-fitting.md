---
lang: en
layout: post
title:  "Swift-Voce model and its curve fitting"
date:   2023-08-08
author: "[SimLet](https://twitter.com/getwelsim)"
---

The process of deformation to ultimate failure in a structural material involves several stages: Elasticity -> Initial Necking -> Cold deformation during necking -> Continued hardening and failure. Commonly used mathematical models for deformation beyond the necking point, are the Johnson-Cook model and the Swift-Voce model. The Swift-Voce model is a combination of the Swift and Voce models using linear interpolation, which provides a wider range of applicability and better fitting accuracy with test data.

<p align="center">
  <img src="\assets\blog\20230808\welsim_necking.png" alt="welsim_necking" />
</p>

With the development of electric vehicles and electric battery technology in recent years, engineers have applied the Swift-Voce model to the plastic deformation of lithium alloys after necking, achieving excellent results. Similar to Johnson-Cook, the Swift-Voce model can also account for the effects of strain rate and temperature on plastic material deformation. Additionally, Swift-Voce can be applied to orthotropic materials and allows for quadratic non-associated plastic flow rules. This article will introduce the Swift-Voce model and its curve fitting.


## Swift and Voce Models
The mathematical representation of the Swift plasticity model is as follows:
<p align="center">
  <img src="\assets\blog\20230808\welsim_eqn_swift.png" alt="welsim_eqn_swift" />
</p>

Where the material constants A, yield strain epsilon0, and strain hardening exponent n are all positive values. Similar to the Johnson-Cook model, the Swift model has no stress limit, but it lacks an initial value.

The Voce plasticity model considers the initial yield point, and its mathematical equation is as follows:
<p align="center">
  <img src="\assets\blog\20230808\welsim_eqn_voce.png" alt="welsim_eqn_voce" />
</p>

Here, yield stress K0, coefficients Q, and B are all positive values. The model has a stress limit, and as strain increases, the fitted stress approaches a constant value.

The mathematical expression of the Swift-Voce plasticity model is as follows:
<p align="center">
  <img src="\assets\blog\20230808\welsim_eqn_swift_voce.png" alt="welsim_eqn_swift_voce" />
</p>

Essentially, Swift-Voce is a linear combination of the two models above. The parameter alpha represents the weight coefficients of the Swift and Voce hardening models, using values within the range of [0, 1].

In practical applications, the Swift hardening model fits the flow stress to increase rapidly with the increasing strain, eventually exceeding the actual stress. While, the Voce hardening model fits the flow stress to approach the tensile strength but remains lower than the actual stress as strain increases. Combining the advantages of both models, Swift-Voce achieves better fitting accuracy, but the number of fitting parameters increases from 3 to 7.

When dealing with the effects of strain rate and temperature, the strain rate and temperature components of the Johnson-Cook model can be directly introduced into the above models. For the effects of strain rate strengthening and temperature softening, you can refer to the article "[Johnson-Cook model and its curve fitting](https://welsim.com/2023/07/28/johnson-cook-model-and-its-curve-fitting.html)".


## Fitting Swift-Voce Parameters 
In practical applications, Swift-Voce parameters need to be obtained through parameter fitting based on material test data. CurveFitter provides curve-fitting formulas for the Swift-Voce plasticity model, requiring only input of true plastic strain and true stress values to obtain the fitted parameter values. For details about CurveFitter, refer to the articles "[An easy-to-use and free curve fitting tool - CurveFitter](https://welsim.com/2021/07/09/an-easy-to-use-and-free-curve-fitting-tool-curvefitter.html)" and "[The numerical methods applied in curve fitting and the updates of CurveFitter](https://welsim.com/2022/08/11/the-numerical-methods-applied-in-curve-fitting-and-the-updates-of-CurveFitter.html)".

The procedure is as follows:

(1) Choose the Swift, Voce, or Swift-Voce curve equation from the left-side list. In this example, the Voce model is chosen.
<p align="center">
  <img src="\assets\blog\20230808\welsim_curvefitter_nonlinear.png" alt="welsim_curvefitter_nonlinear" />
</p>

(2) Import the curve data into the table window on the right. After importing, the stress-strain curve is displayed in the chart window.
<p align="center">
  <img src="\assets\blog\20230808\welsim_curvefitter_voce_chart.png" alt="welsim_curvefitter_voce_chart" />
</p>

(3) Click the "Solve" button in the main window. This will provide the fitted parameters. For the given data, parameters K0=499.9, Q=1474.63, and B=0.7148 are obtained, with an almost negligible fitting error (R2=0.9988). The chart window simultaneously displays both the curve and test data, with the two curves closely aligned, indicating high fitting accuracy. The output window shows the solver's computational details for the curve fitting.
<p align="center">
  <img src="\assets\blog\20230808\welsim_curvefitter_voce_result.png" alt="welsim_curvefitter_voce_result" />
</p>

(4) The curve fitting steps for Swift and Swift-Voce models are the same as those for the Voce model example.

It's important to note that the test data uses true plastic strain - true stress pairs. Curve fitting requires consistency in units. When applying these parameters, ensure that the stress unit in the finite element software matches the stress unit in the test data. Here, the test data is in MPa.


## Conclusion

The Swift, Voce, and Swift-Voce models are plasticity models used to represent metal structures with a broader range of applicability. When other models fail to meet fitting accuracy, Swift-Voce can be considered, achieving higher precision. For materials without given parameters in manuals, CurveFitter can rapidly and accurately calculate the vital parameters for subsequent finite element analyses.

---

<small>
WELSIM is the #1 engineering simulation software for the open-source community.
</small>
