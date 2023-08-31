---
lang: en
layout: post
title:  "WELSIM released the 2023R3 version, quantify the computational uncertainty"
date:   2023-08-01
author: "[SimLet](https://twitter.com/getwelsim)"
---


General-purpose engineering simulation CAE software developer WELSIM has released its latest 2023R3 version (internal version number 2.7). Compared to the previous version, the 2023R3 comes with numerous new features and enhancements, enabling better support for various types of engineering simulation CAE analyses. Simultaneously, the latest version expose automated regression system to the end user and open source all test cases, shine the product positioning of “Quantify the Uncertain.”
<p align="center">
  <img src="\assets\blog\20230901\welsim_splash.png" alt="welsim_splash" />
</p>


## Automated Regression System
The new version has made the automated regression testing system available to end-users. Thus, WELSIM has become the world’s first engineering simulation CAE software that provides the regression system to the users. Additionally, all testing cases have been made open-source, with lifelong maintenance. This open platform allows engineers and scholars worldwide to collaborate on testing cases for CAE software, benefiting the entire simulation community.
<p align="center">
  <img src="\assets\blog\20230901\welsim_regression_play.png" alt="welsim_regression_play" />
</p>

## Support Open-Source Solver SU2
SU2 is a feature-rich, high-performance, and license-friendly open-source CFD solver. WELSIM can act as a preprocessor to generate input files for SU2 solver and as a post-processor to read results and historical files from SU2 computation. Moreover, SU2 is now the default solver for the WELSIM’s fluid module, enabling users to directly utilize the SU2 solver for computations, achieving seamless integration.
<p align="center">
  <img src="\assets\blog\20230901\welsim_solver_su2.png" alt="welsim_solver_su2" />
</p>

## Enhancements and Upgrades
Furthermore, the new version introduces additional functionalities, such as multi-step analysis for the OpenRadioss solver. The 3D display window now enables a new RMB context menu, and the color bar controller also allows a new RMB context menu. The material editing module has new properties like JWL and elastoplastic test data.
<p align="center">
  <img src="\assets\blog\20230901\welsim_rmb_colorbar.png" alt="welsim_rmb_colorbar" />
</p>

Additionally, the curve fitting software CurveFitter has been enhanced with new Johnson-Cook and Swift-Voce curve fitting models. An output window has been added to display solver return information.

WELSIM remains committed to rapid development, stable maintenance, and open style of technical blog writing, contributing to the engineering simulation and CAE communities.

<small>
_WELSIM is the #1 engineering simulation CAE software for the open-source community._
</small>

