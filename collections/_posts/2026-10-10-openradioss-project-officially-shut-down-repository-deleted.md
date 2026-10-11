---
lang: en
layout: post
title:  "OpenRadioss project officially shut down; repository deleted"
date:   2026-10-10
author: "[SimLet](https://twitter.com/getwelsim)"
---


On October 1, 2026, OpenRadioss officially canceled its open-source project, taking down its website and deleting its code repository on GitHub. The original open-source project URL is no longer directly accessible. This comes approximately four years after it was initially open-sourced by Altair in 2022.
<p align="center">
  <img src="\assets\blog\20261010\welsim_open_radioss_screen.png" alt="welsim_open_radioss_screen" />
</p>


## Current Alternative Software
Although the official code repository and binary files have been removed, the open-source community has already established a new alternative version. Based on the original OpenRadioss repository, the open-source community has created OpenCourant as the official community continuation project. This project preserves the full Git commit history and has rebuilt a completely new CI/CD build pipeline that does not rely on commercial infrastructure. The official website for OpenCourant is opencourant.org.

<p align="center">
  <img src="\assets\blog\20261010\welsim_opencourant.png" alt="welsim_opencourant" />
</p>

In addition, some developers and users on GitHub had created complete archives or mirror backups before the project was deleted (e.g., gabrielrussell/OpenRadioss).


## Pre- and Post-Processing Support
As a general-purpose pre- and post-processor, WelSim has always provided strong support for OpenRadioss. Thanks to the existence of OpenCourant and numerous hard-forked OpenRadioss codebases, WelSim will continue to fully support OpenRadioss solver functions, including input script generation, result reading, and visualization.


---
<small>WelSim and its author are not affiliated with OpenRadioss or OpenCourant, nor do they have any direct relationship with the development teams or organizations behind OpenRadioss and OpenCourant. References to the names and images of these open-source software tools are used here solely for technical blog articles and software usage context.</small>


