---
lang: en
layout: post
title:  "Elastoplastic Models in Structural Finite Element Analysis"
date:   2022-11-22
author: "[SimLet](https://twitter.com/getwelsim)"
---



Plastic forming is one of the most important processing methods in modern industry. As small as spring winding, as large as automobile body forging, it is a plastic forming process. The basic forming production methods include free forging, die forging, sheet metal forming, extrusion, rolling, drawing, etc. In addition, most materials will undergo a process of plastic deformation before damage and failure. Understanding plastic deformation is of great significance for production and life safety.
<p align="center">
  <img src="\assets\blog\20221122\plastic_factory.jpg" alt="plastic_factory" />
</p>


Plastic deformation means that the material deforms beyond the elastic limit (also known as yield stress), showing a complex strain-stress relationship. At this time, even if the external force is unloaded, it cannot return to its original shape. After the material enters the plastic stage, if the strain continues to increase, the stress begins to decrease (also called strain softening) until the material fails and fractures. There are many factors affecting plastic deformation, such as strain, strain rate, temperature, loading history, and some material factors such as damage. To better understand and describe plasticity, various plasticity models have been proposed.
<p align="center">
  <img src="\assets\blog\20221122\plastic_manufacture.png" alt="plastic_manufacture" />
</p>


## Yield Criteria
The yield criterion is the entrance point in the theory of plasticity. It describes the transition from elasticity to plasticity. The yield stress or yield function is often used to represent this stage of structural deformation. The elastoplastic analysis is based on the yield criterion to determine whether the material is in the elastic range or has entered the plastic flow state. The initial yield condition gives the stress state at which the material has just entered plastic deformation. The commonly used yield criteria for engineering materials are von Mises, Drucker–Prager, Tresca, Mohr-Coulomb, and Barlat. In anisotropic materials, the yield equation is often expressed in terms of equivalent stress. In an isotropic system, however, the yield stress is a constant variable.
<p align="center">
  <img src="\assets\blog\20221122\plastic_deform_chart.png" alt="plastic_deform_chart" />
</p>


## Plastic Flow Rule
The flow rule is used to describe the relationship between the plastic strain increment and the stress increment, and on this basis, the elastoplastic constitutive relation is established. When the material is experiencing plastic deformation, the flow rule defines the direction of the strain. After the material has yielded, the flow rule describes how each component of plastic strains develops for every load increment. From the mathematical perspective, according to whether it is normal to the yield surface, the flow rule can be classified into associated and non-associated criteria. Most metal materials follow the associated flow rule, while rock and soil materials mostly satisfy the non-associated flow rule. Besides, the flow rule plays a more important role in the process of viscoplastic deformation.

## Hardening Criteria
The hardening criterion specifies the form in which the material is during plastic deformation. When the material undergoes plastic deformation in the yield stage, it is unloaded and then loaded to yield, and the new yield point is higher than the original yield point. The first yield point corresponds to the “initial yield stress”, and each yield is a little higher than the previous one, and this development process is hardening. For ideal elastoplastic materials without hardening effects, the subsequent yield function is identical to the initial yield function.
<p align="center">
  <img src="\assets\blog\20221122\plastic_fea.png" alt="plastic_fea" />
</p>


According to the directionality of deformation, if the hardening in each direction is the same after loading-unloading in one direction, it is called “isotropic hardening”; if the hardening in each direction is different after loading-unloading in one direction, it is called “Kinematic Hardening”. For example, isotropic hardening usually adopts the Von Mises (isotropic) yield criterion, which has a good approximation for metals, polymers, and saturated geological materials. The kinematic hardening model can adopt the Hill (orthotropic) yield criterion, and the yield process needs to consider the relative relationship between the stress direction and the axial direction, which can be used in the forging process of microstructure or metal.

For each hardening process, there are bilinear, multilinear, and nonlinear models. All three are used to describe the strain-stress relations, which give important mechanical information such as yield stress and elastic modulus. The bilinear model is described by two lines, and the multi-linear model is described by multiple lines, which are generally expressed by strain-stress experimental data. The nonlinear modulus uses a segment of nonlinear functions and parameters to determine the plastic properties.
<p align="center">
  <img src="\assets\blog\20221122\plastic_forming4.gif" alt="plastic_forming4" />
</p>


## Temperature effect and loading and unloading criteria
For the impact and shock, most of the plastic strain energy is converted into thermal energy, which leads to an increase in material temperature, and the elevated temperature will affect the physical properties of the materials. Therefore, in many plastic analyses, plastic heat is taken into account in the calculation. At the same time, due to the hardening of the material, the loading and unloading processes sometimes need to be treated differently. This is why many plastic calculations need to consider loading and unloading processes separately.

## Selected Plasticity Models
### Johnson-Cook model
The Johnson-Cook model is widely used for isotropic elastoplastic materials. The Johnson-Cook constitutive is mainly suitable for deformations with strain rates less than 1e4 s-1. True stress is expressed as
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_plas_johnson_d.png" alt="welsim_mateditor_plas_johnson_d" />
</p>

Among them, the yield stress a should be greater than 0, and the plastic hardening exponent n should be less than or equal to 1. Johnson-Cook has the characteristics of simple form and easy calculation and can reflect the effects of plastic strain, strain rate, and temperature at the same time. It is the most commonly used plastic model in structural analysis. The input parameters are shown in the figure below
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_plas_johnson.png" alt="welsim_mateditor_plas_johnson" />
</p>

### Zerilli-Armstrong model
Similar to Johnson-Cook, it is a simple nonlinear theory used to model isotropic elastoplastic materials. The expression of true stress is
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_plas_zeril_d.png" alt="welsim_mateditor_plas_zeril_d" />
</p>

Among them, the yield stress C0 should be greater than 0, and the plastic hardening exponent m should be less than or equal to 1. The input parameters are shown in the figure below
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_plas_zeril.png" alt="welsim_mateditor_plas_zeril" />
</p>

### Hill model
Hill is used to describe orthotropic plastic materials. Yield stress is defined as
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_hill_d.png" alt="welsim_mateditor_hill_d" />
</p>

The Hill model is the most widely used orthotropic elastoplastic model. The input parameters are shown in the figure below
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_hill.png" alt="welsim_mateditor_hill" />
</p>


### Rate-dependent multilinear hardening model
Define isotropic elastoplastic deformation via tabular data. The input data is the strain-stress relationship at different strain rates. Enter the data as shown in the figure.
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_plas_rate_dep2.png" alt="welsim_mateditor_plas_rate_dep2" />
</p>

<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_plas_rate_dep.png" alt="welsim_mateditor_plas_rate_dep2" />
</p>


### Orthotropic Hill model
Orthotropic elastoplastic model. For solid elements, the equivalent stress is defined as:
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_plas_orthotropic_hill_d.png" alt="welsim_mateditor_plas_orthotropic_hill_d" />
</p>

The input parameters are shown in the figure below.
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_plas_orthotropic_hill.png" alt="welsim_mateditor_plas_orthotropic_hill" />
</p>

### Cowper-Symonds model
Similar to the Johnson-Cook model, the Cowper-Symonds model is used for isotropic plasticity. Stresses can be expressed by three stress coefficients, tabular data, or a combination of both. Among them, the three-parameter expression is:
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_plas_cowper_d.png" alt="welsim_mateditor_plas_cowper_d" />
</p>

where the yield stress a should be greater than 0, and the plastic hardening exponent n should be less than or equal to 1. The input parameters are shown in the figure below:
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_plas_cowper.png" alt="welsim_mateditor_plas_cowper" />
</p>

### Zhao model
This model can describe elastoplastic materials that deform based on plastic strain rates. The stress calculation formula is:
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_plas_zhao_d2.png" alt="welsim_mateditor_plas_zhao_d2" />
</p>

where the yield stress A should be greater than 0, and the plastic hardening index n should be less than or equal to 1. When the strain rate is less than the reference strain rate, the stress simplifies to:
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_plas_zhao_d.png" alt="welsim_mateditor_plas_zhao_d" />
</p>

The input parameters are shown in the figure below.
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_plas_zhao.png" alt="welsim_mateditor_plas_zhao" />
</p>

### Steinberg-Guinan model
This model adds an elastoplastic model of the thermal softening effect. The expression for the yield stress is as follows:
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_plas_steinberg_d.png" alt="welsim_mateditor_plas_steinberg_d" />
</p>

The input parameters are shown in the figure below.
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_plas_steinberg.png" alt="welsim_mateditor_plas_steinberg" />
</p>

### Gurson model
The Gurson model can be used for the calculation of viscoelastic plastic materials, especially porous materials. Yield stress can be obtained from experimental data or calculated by the Cowper-Symond model. For the von Mises criterion under viscoplastic flow, it can be calculated by the following formula:
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_plas_gurson_d2.png" alt="welsim_mateditor_plas_gurson_d2" />
</p>
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_plas_gurson_d.png" alt="welsim_mateditor_plas_gurson_d" />
</p>

The relevant parameters are defined as follows.
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_plas_gurson.png" alt="welsim_mateditor_plas_gurson" />
</p>


### Barlat3 model
The Barlat3 model is an orthotropic elastoplastic model. Commonly used in metal forming processing, such as aluminum alloy processing. Therefore a large number of applications are relevant to shell elements. The plastic hardening function can be expressed by parameters or tabular data, where the anisotropic yield criterion for plane stress can be expressed by the following formula
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_plas_barlet3_d2.png" alt="welsim_mateditor_plas_barlet3_d2" />
</p>


The evolution of Young’s modulus during plastic deformation can be expressed by the following formula.
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_plas_barlet3_d.png" alt="welsim_mateditor_plas_barlet3_d" />
</p>


The input parameters are shown in the figure below:
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_plas_barlet3.png" alt="welsim_mateditor_plas_barlet3" />
</p>


### Yoshida-Uemori model
The Yoshida-Uemori model can be used in the case of large-strain cyclic plastic deformation. This model is based on yield surface and bound surface theories. For solid elements, the von Mises yield criterion is commonly used. For plate and shell elements, Hill or Barlat3 yield criteria can be applied. The corresponding yield criterion expression is as follows:
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_plas_yoshida_d.png" alt="welsim_mateditor_plas_yoshida_d" />
</p>
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_plas_yoshida_d2.png" alt="welsim_mateditor_plas_yoshida_d2" />
</p>


The input parameters are shown in the figure below:
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_plas_yoshida.png" alt="welsim_mateditor_plas_yoshida" />
</p>


### Johnson-Holmquist model
The Johnson-Holmquist model is often used for elastoplastic processes of brittle materials, such as ceramics, glass, etc. This model can also be combined with failure models. The equivalent stress expression is
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_plas_holmquist_d.png" alt="welsim_mateditor_plas_holmquist_d" />
</p>


The input parameters are shown in the figure below:
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_plas_holmquist.png" alt="welsim_mateditor_plas_holmquist" />
</p>


### Swift-Voce model
The Swift-Voce elastoplastic model combines Johnson-Cook strain rate hardening and temperature softening effects. Can be used for orthotropic materials while allowing quadratic non-associative flow laws. Yield stress can be expressed comprehensively by Swift and Voce models.
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_plas_swift_d.png" alt="welsim_mateditor_plas_swift_d" />
</p>

The input parameters are shown in the figure below:
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_plas_swift.png" alt="welsim_mateditor_plas_swift" />
</p>

### Hensel-Spittel model
The Hensel-Spittel model takes into account the effects of strain, strain rate, and temperature. Commonly used in the hot forging process of metals. The expression for the yield stress is
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_plas_hensel_d.png" alt="welsim_mateditor_plas_hensel_d" />
</p>


The input parameters are shown in the figure below:
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_plas_hensel.png" alt="welsim_mateditor_plas_hensel" />
</p>


### Vegter model
The yield function is expressed as follows.
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_plas_vegter_d.png" alt="welsim_mateditor_plas_vegter_d" />
</p>

The input parameters are shown in the figure below:
<p align="center">
  <img src="\assets\blog\20221122\welsim_mateditor_plas_vegter.png" alt="welsim_mateditor_plas_vegter" />
</p>


The plastic models mentioned above all support the generation of material files in the OpenRadioss format.
<p align="center">
  <img src="\assets\blog\20221122\welsim_eos_export_openradioss.png" alt="welsim_eos_export_openradioss" />
</p>

## Postprocessing for Plasticity Analysis
In postprocessing, elastoplastic analysis often requires the evaluation of additional results. Such as

**Equivalent Stress**: under the hardening circumstance, the current value of the yield stress.

**Accumulated Plastic Strain**: it refers to the sum of the plastic strain rate along a certain path in the deformation history.

**Stress Ratio**: The ratio of the elastic stress to the current yield stress is an indicator of plastic deformation under load increments. When >1, the current is plastic deformation; when <1, the current is elastic deformation; when =1, the current has just reached yield.

## Conclusion
This article introduces plastic models commonly used in finite element analysis, which can meet most engineering application scenarios. Due to limited space, not all the formulas are listed here, and the specific details of the relevant plastic models can be found in the theory manuals in MatEditor or other software.


******

<small>
WelSimulation LLC is an independent engineering simulation technology provider, located in Greater Pittsburgh, PA. Its flagship product WESLIM is a general-purpose engineering simulation software with an all-in-one graphical user interface and self-integrated features.
</small>

