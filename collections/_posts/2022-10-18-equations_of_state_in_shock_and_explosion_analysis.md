---
lang: en
layout: post
title:  "Equations of State (EOS) in Shock and Explosion Analysis"
date:   2022-10-18
author: "[SimLet](https://twitter.com/getwelsim)"
---

Shock and explosion are common subjects in modern engineering simulation. There have been many successful applications ranging from cell phone dropping analysis, to car crashes, to complex underwater explosion. Compared with traditional structural or fluid simulation, the calculation method of shock and explosion is slightly difference due to the diversity of working conditions. The main characteristics of impact and explosion are high speed and high energy. Under this condition, even a material with very high strength will undergo a huge change in physical properties in an instant. For example, the change of substances from solid to liquid, or even gaseous state, material failure, fracture or pulverization due to high strain rate or high temperature. These characteristics make us need to add relevant theories to the traditional continuum mechanics to meet the needs of practical engineering.

<p align="center">
  <img src="\assets\blog\20221018\car_crash.jpg" alt="car_crash" />
</p>

Due to the characteristics of hydrodynamic pressure in shock and explosion, it is necessary to calculate these pressures caused by volumetric strains, so as to obtain all stresses accurately. The Equations of State (EOS) is a model for calculating the hydrodynamic pressure. The development of EOS began in the 1950s and has experienced more than 70 years of development. With the development of simulation technologies such as finite element method, the application of EOS has become more and more extensive. Some theories of EOS come from empirical formulas, and some from theoretical deductions at the atomic and molecular level. Thermodynamics also plays an important role in the EOS model due to the huge thermodynamic energy transfer in the shock and explosion. Some EOS models may also contain ideal gas equations to describe explosive products or air. These differ from traditional continuum mechanics, involving interactions between particles and chemical reactions. It can be said that EOS involves multi-scale and multi-disciplinary, and expresses complex physical conditions into a mathematical model for calculating hydrodynamic pressure.

<p align="center">
  <img src="\assets\blog\20221018\water_explosion3.jpg" alt="water_explosion" />
</p>

## Types of EOS Models

The main purpose of EOS is to calculate the hydrodynamic pressure, and the independent variables often use the volumetric change of the object, such as the compressibility and the internal energy density by volume. The choose of independent variables is not unique, that explains that we see the various equations for the same EOS model. In this article, we use the compressibility as the main independent variable to keep the consistence of the content.

In addition, the free software MatEditor has supported a large number of EOS models, users can quickly and easily create EOS material properties for successive analysis or computation.
<p align="center">
  <img src="\assets\blog\20221018\mateditor_eos_list.PNG" alt="mateditor_eos_list" />
</p>

### Compaction EOS
The pressure governing equation is
<p align="center">
  <img src="\assets\blog\20221018\welsim_eos_compaction.png" alt="welsim_eos_compaction" />
</p>

The definition of the input parameters is shown in the following figure.
<p align="center">
  <img src="\assets\blog\20221018\mateditor_eos_compaction.png" alt="welsim_eos_compaction" />
</p>

The description of the unloading state can be expressed by the parameter Unloading Bulk Modulus. Compaction EOS is commonly used for gas materials, and also be used for porous media such as soil, foam, etc.

### Gruneisen EOS
Gruneisen EOS gives the respective pressure calculation methods according to the two different states of compression and expansion. At compression u>=0, the governing equation of pressure:
<p align="center">
  <img src="\assets\blog\20221018\welsim_eos_gruneisen.png" alt="welsim_eos_gruneisen" />
</p>

At expansion u<0, the pressure is :
<p align="center">
  <img src="\assets\blog\20221018\welsim_eos_gruneisen2.png" alt="welsim_eos_gruneisen2" />
</p>

The definition of the input parameters is shown in the following figure.
<p align="center">
  <img src="\assets\blog\20221018\mateditor_eos_gruneisen.png" alt="mateditor_eos_gruneisen" />
</p>

Gruneisen is often used in metal materials, such as the metal shell of TNT explosives. The commonly used metals are copper, stainless steel, aluminum, manganese, titanium, nickel, barium, etc.

### Ideal Gas EOS
The pressure governing equation is
<p align="center">
  <img src="\assets\blog\20221018\welsim_eos_idealgas.png" alt="welsim_eos_idealgas" />
</p>

The definition of the input parameters is shown in the following figure.
<p align="center">
  <img src="\assets\blog\20221018\mateditor_eos_idealgas.png" alt="mateditor_eos_idealgas" />
</p>

As the name suggests, Ideal Gas is often used for gases such as air at atmospheric pressure.

### Linear EOS
The pressure governing equation is
<p align="center">
  <img src="\assets\blog\20221018\welsim_eos_linear.png" alt="welsim_eos_linear" />
</p>

The definition of the input parameters is shown in the following figure.
<p align="center">
  <img src="\assets\blog\20221018\mateditor_eos_linear.png" alt="mateditor_eos_linear" />
</p>

Linear model is a simplified form of polynomial model. Wide range of uses. Often used for gases.

### LSZK EOS (Landau-Stanyukovich-Zeldovich-Kompaneets)
The pressure governing equation is
<p align="center">
  <img src="\assets\blog\20221018\welsim_eos_lszk.png" alt="welsim_eos_lszk" />
</p>

The definition of the input parameters is shown in the following figure.
<p align="center">
  <img src="\assets\blog\20221018\mateditor_eos_lszk.png" alt="mateditor_eos_lszk" />
</p>

LSZK is a model commonly used for gases in explosions.

### Murnaghan EOS
The pressure governing equation is
<p align="center">
  <img src="\assets\blog\20221018\welsim_eos_murnaghan.png" alt="welsim_eos_murnaghan" />
</p>

The definition of the input parameters is shown in the following figure.
<p align="center">
  <img src="\assets\blog\20221018\mateditor_eos_murnaghan.png" alt="mateditor_eos_murnaghan" />
</p>

The Murnaghan EOS is independent of the energy density quantity and is often used for gases.

### NASG EOS (Noble-Abel Stiffened Gas)
The pressure governing equation is
<p align="center">
  <img src="\assets\blog\20221018\welsim_eos_nasg.png" alt="welsim_eos_nasg" />
</p>

The definition of the input parameters is shown in the following figure.
<p align="center">
  <img src="\assets\blog\20221018\mateditor_eos_nasg.png" alt="mateditor_eos_nasg" />
</p>

NASG can be used for gases and liquids.

### Noble-Abel EOS
The pressure governing equation is
<p align="center">
  <img src="\assets\blog\20221018\welsim_eos_nobleabel.png" alt="welsim_eos_nobleabel" />
</p>

The definition of the input parameters is shown in the following figure.
<p align="center">
  <img src="\assets\blog\20221018\mateditor_eos_nobleabel.png" alt="mateditor_eos_nobleabel" />
</p>

The Noble-Abel model can be used for high-density gases at high pressures.

### Osborne EOS
Osborne EOS is also known as Quadratic EOS. The pressure governing equation is
<p align="center">
  <img src="\assets\blog\20221018\welsim_eos_osborne.png" alt="welsim_eos_osborne" />
</p>

The definition of the input parameters is shown in the following figure.
<p align="center">
  <img src="\assets\blog\20221018\mateditor_eos_osborne.png" alt="mateditor_eos_osborne" />
</p>

The Osborne model is widely used in various metals, and can also be used in materials such as water, explosives, graphite, plexiglass, and plastics. Parameters for various materials can be found in the manual.

### Polynomial EOS
The pressure governing equation is
<p align="center">
  <img src="\assets\blog\20221018\welsim_eos_polynomial.png" alt="welsim_eos_polynomial" />
</p>

The definition of the input parameters is shown in the following figure.
<p align="center">
  <img src="\assets\blog\20221018\mateditor_eos_polynomial.png" alt="mateditor_eos_polynomial" />
</p>

Polynomial EOS is a general empirical model. It commonly used for metals such as steel, tungsten.

### Puff EOS
According to different states, Puff’s pressure governing equation is given below. In the compressed state u>=0,
<p align="center">
  <img src="\assets\blog\20221018\welsim_eos_puff1.png" alt="welsim_eos_puff1" />
</p>

Expansion state u<0, and energy density E>=Es,
<p align="center">
  <img src="\assets\blog\20221018\welsim_eos_puff2.png" alt="welsim_eos_puff2" />
</p>

Expansion state u<0, and strain energy density E<Es,
<p align="center">
  <img src="\assets\blog\20221018\welsim_eos_puff3.png" alt="welsim_eos_puff3" />
</p>

The definition of the input parameters is shown in the following figure.
<p align="center">
  <img src="\assets\blog\20221018\mateditor_eos_puff.png" alt="mateditor_eos_puff" />
</p>

Puff is often used for metal materials.

### Stiffened Gas EOS
The pressure governing equation is
<p align="center">
  <img src="\assets\blog\20221018\welsim_eos_stiffenedgas.png" alt="welsim_eos_stiffenedgas" />
</p>

The definition of the input parameters is shown in the following figure.
<p align="center">
  <img src="\assets\blog\20221018\mateditor_eos_stiffgas.png" alt="mateditor_eos_stiffgas" />
</p>

Stiffened Gas can be used for water in underwater explosions.

### Tillotson EOS
According to different states, Tillotson’s pressure governing equation is given below. In the compressed state (u>=0),
<p align="center">
  <img src="\assets\blog\20221018\welsim_eos_tillotson1.png" alt="welsim_eos_tillotson1" />
</p>

In the expanded state (u<0), and the volume V/V0<Vs, when the energy density E<Es,
<p align="center">
  <img src="\assets\blog\20221018\welsim_eos_tillotson2.png" alt="welsim_eos_tillotson2" />
</p>

Expansion state (u<0), and volume V/V0>=Vs, or volume V/V0<Vs and energy density E>=Es,
<p align="center">
  <img src="\assets\blog\20221018\welsim_eos_tillotson3.png" alt="welsim_eos_tillotson3" />
</p>

The definition of the input parameters is shown in the following figure.
<p align="center">
  <img src="\assets\blog\20221018\mateditor_eos_tillotson.png" alt="mateditor_eos_tillotson" />
</p>

Tillotson is often used in metallic materials. Parameters can be obtained from the relevant manuals.

## Conclusion
MatEditor provides a simple and easy-to-use graphical user interface for creating well-known EOS material properties, and supports conversion of different units. Data can be exported in different formats, such as OpenRadioss format, more data format will be supported in the future.
<p align="center">
  <img src="\assets\blog\20221018\welsim_eos_export_openradioss.png" alt="welsim_eos_export_openradioss" />
</p>

There are a considerable number of EOS models and EOS models are still evolving. It is necessary to have a good understanding of the application scope of each EOS model. In order to achieve accurate calculation or simulation results, the material parameters of each EOS need to be determined by referring to the relevant manuals.


******

<small>
WelSimulation LLC is an independent engineering simulation technology provider, located in Greater Pittsburgh, PA. Its flagship product WESLIM is a general-purpose engineering simulation software with an all-in-one graphical user interface and self-integrated features.
</small>

