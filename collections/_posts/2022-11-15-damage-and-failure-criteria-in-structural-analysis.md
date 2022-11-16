---
lang: en
layout: post
title:  "Damage and Failure Criteria in Structural Analysis"
date:   2022-11-15
author: "[SimLet](https://twitter.com/getwelsim)"
---

With the development of simulation technology, engineers and scientists are more and more interested in the damage, fracture, failure, destruction and other phenomena on the top of conventional analysis. For example, in shock and dynamics, the ideal failure model can predict the elements that should be deleted or propagate cracks, and show the results of the analysis objects under extraordinary loads. Combined with post-processing tools, the simulation results can be not only accurate, but also vivid. We have often seen the application of failure models in the crash analysis of automobiles and aircraft.

<p align="center">
  <img src="\assets\blog\20221115\demo_failure2.jpg" alt="car_crash" />
</p>

In actual engineering, mechanical failure can occur in various conditions. Such as large deformation, buckling, bending, brittle fracture, ductile fracture, creep, wear, fatigue crack propagation, delamination, etc. In addition, there are also various thermal failures, chemical failures, electrical failures, etc. These failures have permanent effects on objects and will also bring certain safety hazards to people’s production and life. The failure and damage models can effectively avoid disasters through pre-analysis. At the same time, with the rise of the metaverse in recent years, various failure models will also have a large number of applications in the metaverse.

<p align="center">
  <img src="\assets\blog\20221115\demo_failure3.jpg" alt="car_crash" />
</p>


## Quantities in Failure Models
There are many damage models, including general-purpose models and fine models for specific materials or working conditions. In general, these models are represented by calculating the damage quantity, which is usually represented by the letter D in the math formula. When D is greater than a certain value, it is considered that the material damage reaches a certain level and begins to fail. Most models define D to be a value between 0 and 1. When D is less than 1, the structure is free. When D is greater than or equal to 1, it is determined that the material fails.

The calculation of D value is the key to distinguish different failure models, and it is generally obtained through the results on the elemental integration points such as strain, stress, and strain energy density. The most common basic quantity of failure model is strain, such as plastic strain, total strain, etc., because the strain quantity is easy to obtain and is less influenced by other physical quantities, it is widely used in failure models. There are also some failure models based on stress, such as some brittle materials. Failure models based on strain energy density are often used in metal forming process. Some failure models also take fatigue as the basic quantity, and this kind of model often has an integral form to measure the accumulated damage. In addition, some models take thermal effects into account, allowing the models to be used in scenarios where there are temperature variations.

## Numerical Processing after Failure
In modern engineering simulation software, when the algorithm determines that the element is failed, it will make corresponding numerical processing. Common processing methods are:

1. Delete the element. Since the part has failed, the local element is deleted for subsequent computation.

2. Crack propagation. If it is a small local failure, XFEM and other methods can be used to expand the crack and convey influence of the failed element on the surrounding elements.

<p align="center">
  <img src="\assets\blog\20221115\demo_xfem.png" alt="xfem" />
</p>

3. Stress elimilation and softening. Make the stress of the current element to zero or reduce it artificially. Comparing to element deletion and crack propagation, it consumes less computational resources and is easy to implement in development. Among them, stress softening is a method often used in the failure of hyperelastic materials.

For solid elements, you can decide whether to process the element according to a single integration point or multiple integration points. For shell elements, the element can be processed based on a single layeror multiple layers.


## Failure Models
Now introduce some commonly used failure models, the current version of material editing software MatEditor has supported these models.

### Glass Failure Model
A special stress-based failure model for glass materials in structural simulations. The input parameters are

<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_alter.png" alt="welsim_mateditor_failure_alter" />
</p>

### Bi-Quadratic Failure
The failure model is determined by the user entering the effective plastic strain. Commonly used in ductile metals. The input parameters are

<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_biquad.png" alt="welsim_mateditor_failure_biquad" />
</p>


### Cockcroft Failure
A simplified failure model for calculating ductile materials. The damage calculation is

<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_cockcroft_d.png" alt="welsim_mateditor_failure_cockcroft_d" />
</p>

The input parameters are
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_cockcroft.png" alt="welsim_mateditor_failure_cockcroft" />
</p>


### Connect Failure
A failure model for connecting materials in structural simulation, based on displacement and strain energy quantities. The input parameters are

<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_connect.png" alt="welsim_mateditor_failure_connect" />
</p>



### Extended Mohr-Coulumb Failure
A failure criterion based on effective plastic strain. The damage calculation is
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_emc_d.png" alt="welsim_mateditor_failure_emc_d" />
</p>

The input parameters are
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_emc.png" alt="welsim_mateditor_failure_emc" />
</p>


### Energy Failure
A criterion based on strain energy density. The damage calculation formula is
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_energy_d.png" alt="welsim_mateditor_failure_energy_d" />
</p>


The input parameters are
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_energy.png" alt="welsim_mateditor_failure_energy" />
</p>



### Fabric Failure
The damage calculation formula is
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_fabric_d.png" alt="welsim_mateditor_failure_fabric_d" />
</p>

The input parameters are
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_fabric.png" alt="welsim_mateditor_failure_fabric" />
</p>



### Forming Limit Diagram Failure
Enter the maximum and minimum strain curves to control the failure model. Commonly used to simulate metal forming. The input parameters are
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_fld.png" alt="welsim_mateditor_failure_fld" />
</p>


### Hashin Failure
The damage calculation formula is
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_hashin_d.png" alt="welsim_mateditor_failure_hashin_d" />
</p>


The input parameters are
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_hashin.png" alt="welsim_mateditor_failure_hashin" />
</p>



### Hosford-Coulomb Failure
For ductile metals. The damage calculation formula is
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_hc_dsse_d.png" alt="welsim_mateditor_failure_hc_dsse_d" />
</p>


The damage strain is calculated as
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_hc_dsse_d2.png" alt="welsim_mateditor_failure_hc_dsse_d2" />
</p>


The input parameters are
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_hc_dsse.png" alt="welsim_mateditor_failure_hc_dsse" />
</p>




### Johnson-Cook Failure
The damage calculation formula is
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_joshnson_cook_d.png" alt="welsim_mateditor_failure_joshnson_cook_d" />
</p>


where the damage strain is defined as
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_joshnson_cook_d2.png" alt="welsim_mateditor_failure_joshnson_cook_d2" />
</p>


The input parameters are
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_joshnson_cook.png" alt="welsim_mateditor_failure_joshnson_cook" />
</p>


### Ladeveze Delamination Failure
Used to describe the delamination of composite . Commonly used for composite materials. The damage calculation formula is
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_lad_dama_d.png" alt="welsim_mateditor_failure_lad_dama_d" />
</p>

The input parameters are
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_lad_dama.png" alt="welsim_mateditor_failure_lad_dama" />
</p>



### Mullins Effect
Stress softening methods for hyperelastic materials. The failure algorithm is not invoked. During unloading or reloading, the stress takes into account the softening and is defined as
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_mullins_d.png" alt="welsim_mateditor_failure_mullins_d" />
</p>
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_mullins_d2.png" alt="welsim_mateditor_failure_mullins_d2" />
</p>

The input parameters are
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_mullins.png" alt="welsim_mateditor_failure_mullins" />
</p>

Among them, the larger the R value, the smaller the damage. The smaller the value of m, the larger the damage under small strain. When the value of m is large, the damage is smaller at small strains. The smaller the beta value, the greater the damage.

### NXT Failure
Similar to Forming Limit Diagram, this is a stress-based model. Commonly used in metal forming processes. The damage calculation formula is
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_nxt_d.png" alt="welsim_mateditor_failure_nxt_d" />
</p>

The input parameters are
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_nxt.png" alt="welsim_mateditor_failure_nxt" />
</p>


### Orthotropic Bi-Quadratic Failure
This failure model is available for orthotropic materials. Commonly used in ductile metals. The input parameters are
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_orthbiquad.png" alt="welsim_mateditor_failure_orthbiquad" />
</p>

### Orthotropic Strain Failure
This failure model is available for orthotropic materials. Commonly used in composite materials. The damage calculation formula is
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_orthstrain_d.png" alt="welsim_mateditor_failure_orthstrain_d" />
</p>

The input parameters are
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_orthstrain.png" alt="welsim_mateditor_failure_orthstrain" />
</p>


### Puck Failure
This model is available for solid and shell elements. Commonly used in composite materials. The damage calculation formula is
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_puck_d.png" alt="welsim_mateditor_failure_puck_d" />
</p>

The input parameters are
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_puck.png" alt="welsim_mateditor_failure_puck" />
</p>


### Tuler-Butcher Failure
This model supports the fatigue condition. It can be applied for both ductile and brittle metals. The damage calculation formula is

<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_tbutcher_d1.png" alt="welsim_mateditor_failure_tbutcher_d1" />
</p>

or
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_tbutcher_d2.png" alt="welsim_mateditor_failure_tbutcher_d2" />
</p>

The input parameters are
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_tbutcher.png" alt="welsim_mateditor_failure_tbutcher" />
</p>


### Tensile Strain Failure
This is a strain-based failure criterion. Strain can be equivalent strain or maximum principal tensile strain. This failure criterion gives the solutions close to the real fracture behavior. It commonly used for failure after plastic deformation of metals. The damage calculation formula is
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_tensstrain_d.png" alt="welsim_mateditor_failure_tensstrain_d" />
</p>

The input parameters are
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_tensstrain.png" alt="welsim_mateditor_failure_tensstrain" />
</p>

### Wierzbicki Failure
This is a model based on effective plastic strain, commonly used for ductile metals. The damage calculation formula is
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_wierzbicki_d.png" alt="welsim_mateditor_failure_wierzbicki_d" />
</p>

The input parameters are shown in the figure below
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_wierzbicki.png" alt="welsim_mateditor_failure_wierzbicki" />
</p>


### Wilkins Failure
is a model based on effective plastic strain, commonly used for ductile metals. The damage calculation formula is
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_wilkins_d.png" alt="welsim_mateditor_failure_wilkins_d" />
</p>

The input parameters are shown below
<p align="center">
  <img src="\assets\blog\20221115\welsim_mateditor_failure_wilkins.png" alt="welsim_mateditor_failure_wilkins" />
</p>

## Conclusion
There are many types of failure models that are still under development. Various failure models bring the icing on the cake to the engineering simulation analysis. This article focuses on mechanical failure only. Other types of failures such as electrical failures, radiation failures, chemical failures, etc. will be discussed in future articles.



******

<small>
WelSimulation LLC is an independent engineering simulation technology provider, located in Greater Pittsburgh, PA. Its flagship product WESLIM is a general-purpose engineering simulation software with an all-in-one graphical user interface and self-integrated features.
</small>

