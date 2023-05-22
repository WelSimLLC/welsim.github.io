---
lang: en
layout: post
title:  "Use MatEditor to generate OpenRadioss material data files"
date:   2022-11-26
author: "[SimLet](https://twitter.com/getwelsim)"
---

OpenRadioss is an open-source enterprise-grade explicit dynamics analysis software. Due to its powerful features and long history, OpenRadioss gained a lot of attention from
the simulation community when this open-source project was announced in September 2022. However, as a console solver, OpenRadioss does not have an easy-to-use dedicated GUI front-end program yet. For new users, this causes OpenRadioss to have a relatively large learning curve. That's why an easy-to-use OpenRadioss GUI software is vital for the OpenRadioss, users with simulation needs, and even the entire simulation community.
<p align="center">
  <img src="\assets\blog\20221126\welsim_openradioss_github.png" alt="welsim_openradioss_github" />
</p>


MatEditor is a free material editing software released by WelSim in September 2019 (see “[A Free Material Editing Tool MatEditor](/2019/09/25/a-free-material-editing-tool-mateditor.html)”). Because of its rich features and easy-to-use interface, it has been recognized by many users. In addition to conventional material property editing, MatEditor added the test data curve fitting features (see “[Hyperelastic Material Model and Its Curve Fitting](/2020/07/23/hyperelastic-material-models-and-curve-fitting.html)”). Recently, MatEditor supports OpenRadioss’ material format text file generation. Undoubtedly, MatEditor is the best free material editing software that supports the OpenRadioss format, and the related features are introduced in the following.
<p align="center">
  <img src="\assets\blog\20221126\welsim_mateditor_gui.png" alt="welsim_mateditor_gui" />
</p>



## Supported Unit Systems
Currently, MatEditor supports eight types of commonly used unit systems in simulation engineering.

* Metric kg-m-s
* Metric g-cm-s
* Metrickg-mm-s
* Metric tonne-mm-s
* Metric decatonne-mm-s
* Metric kg-um-s
* US Customary lbm-ft-s
* US Customary lbm-in-s
* Metric g-cm-us

The user can change MatEditor's unit system at any time, and the generated OpenRadioss material file will also be based on the current unit system. The unit conversion will be performed automatically during exporting.

<p align="center">
  <img src="\assets\blog\20221126\welsim_mateditor_units_menu.png" alt="welsim_mateditor_units_menu" />
</p>

In engineering analysis, many diverse units are involved. Currently, MatEditor already supports 81 different quantities. The figure below shows the commonly used pressure unit in structural analysis.
<p align="center">
  <img src="\assets\blog\20221126\welsim_mateditor_units_pressure.png" alt="welsim_mateditor_units_pressure" />
</p>


## Save and Resume
MatEditor supports data persistence. Users can save all newly created material nodes as wsmat files. Files can be used on other machines for data sharing. The wsmat file is an ASCII file in XML format. This format not only effciently performs data reading and loading, but also supports human reading.
<p align="center">
  <img src="\assets\blog\20221126\welsim_mateditor_db_save.png" alt="welsim_mateditor_db_save" />
</p>

An example wsmat file is shown in the figure. This supports reading and writing of multiple materials.
<p align="center">
  <img src="\assets\blog\20221126\welsim_mateditor_db_wsmat.png" alt="welsim_mateditor_db_wsmat" />
</p>


## Tabular Data Input
In addition to the usual constants, large amounts of experimental data such as strain-stress curves, needs to be inputed to material property tables. MatEditor not only supports conventional table input, but also approves multi-dimensional tables based on strain rate, temperature, and frequency. While inputting table data, you can observe the shape of the input curve on the chart window. Data input not only supports manual input for each individual cell, but also supports copy and paste, and reading from external files.
<p align="center">
  <img src="\assets\blog\20221126\welsim_mateditor_plas_rate_dep.png" alt="welsim_mateditor_plas_rate_dep" />
</p>


## Export OpenRadioss Material Files
It is straightforward and easy to export the OpenRadioss file (.rad) file using MatEditor. The toolbar and menu bar of MatEditor provide important buttons. When the material editing is completed, click them to proceed with the output.
<p align="center">
  <img src="\assets\blog\20221126\welsim_openradioss_actions.png" alt="welsim_openradioss_actions" />
</p>

An example of the output rad file is below. Units and all material properties are defined in the file. Notably, MatEditor supports exporting multiple materials in one single rad file.
<p align="center">
  <img src="\assets\blog\20221126\welsim_mateditor_plas_or_output.png" alt="welsim_mateditor_plas_or_output" />
</p>


## Suppress Specified Materials
When editing materials, some material properties will not be used after being added. During this, you can simply suppress the material properties by selecting the boolean dropdown. The suppressed material properties will not be exported to the rad file. As shown in the figure, suppressing and activating operations is simple. Additionally, the suppressed material properties can clearly be distinguished through the crossed-out font.
<p align="center">
  <img src="\assets\blog\20221126\welsim_mateditor_suppress.png" alt="welsim_mateditor_suppress" />
</p>


## Supported OpenRadioss Materials
At present, MatEditor has supported a large number of OpenRadioss material properties, it's still increasing. The corresponding list of the supported properties is below.

### Hyperelasticity and Viscoelasticity

- LAW34 — Boltzmann
- LAW35 — Maxwell-Kelvin-Voigt
- LAW40 — Maxwell-Kelvin
- LAW42 — Odgen 1/2/3
- LAW92 — Arruda-Boyce
- LAW94 — Yeoh 1/2/3
- LAW100 — Polynomial, Neo-Hookean, Mooney-Rivlin2

### Plasticity

- LAW2 — Johnson-Cook 
- PLAS_ZERIL — Zerilli-Armstrng
- LAW32 — Hill
- LAW36 — Rate-Dependent Multilinear Hardening
- LAW44 — Cowper-Symonds
- LAW93 — Orthotropic Hill
- LAW48 — Zhao
- LAW49 — Steinberg-Guinan
- LAW52 — Gurson
- LAW57 — Barlet3
- LAW78 — Yoshida-Uemori
- LAW79 — Johnson-Holmquist
- LAW84 — Swift-Voce
- LAW103 — Hensel-Spittel
- LAW110 — Vegter

### Failure Models

- ALTER — Glass Failure
- BIQUD — BiQuadratic
- COCKCROFT — Cockcroft
- CONNECT-Connect
- EMC — ExtendedMohr-Coulomb
- ENERGY-Energy
- FABRIC — Fabric
- FLD — Forming Limit Diagram
- GURSON — Gurson
- HASHIN — Hashin
- HC_DSSE — Ladeveze Delamination
- JOHNSON-Johnson-Cook
- MULLINS_OR — Mullins Effect
- NXT — NXT
- ORTHBIQUAD — Orthotropic Biquad
- ORTHSTRAIN — Orthotropic Strain
- PUCK — Puck
- TBUTCHER — Tuler-Butcher
- TENSSTRAIN — Tensile Strain
- WILKINS — Wilkins
- WIERZBICKI — Wierzbicki

### Equation of State (EOS)

- Compaction EOS
- Gruneisen EOS
- Ideal Gas EOS
- Linear EOS
- LSZK EOS
- Murnaghan EOS
- NASG EOS
- Nobel-Abel EOS
- Osborne EOS
- Polynomial EOS
- Puff EOS
- Stiff-Gas EOS

Additionally on MatEditor, some basic material properties are supported for OpenRadioss. Such as density, linear elasticity, ALE, etc.

## Conclusion
At the moment, MatEditor has implemented most of the material types required for OpenRadioss analysis. MatEditor is still actively developing and maintaining the package, more unit systems and materials will be added as needed, and more output formats and open-source software will be supported. MatEditor is free for life and can be used for academic research or commercial applications. If you use MatEditor in your thesis or product, you are welcome to cite the [WelSim User Manual](https://docs.welsim.com). If you are would like any new features for MatEditor, please submit them on WelSim’s [GitHub](https://github.com/WelSimLLC) page.

******

<small>
WelSim is not affiliated with the Altair or OpenRadioss team. OpenRadioss is used only as nominative references to the open-source project and software developed and released by the Altair and OpenRadioss teams.
</small>

<small>
WelSimulation LLC is an independent engineering simulation technology provider, located in Greater Pittsburgh, PA. Its flagship product WESLIM is a general-purpose engineering simulation software with an all-in-one graphical user interface and self-integrated features.
</small>

