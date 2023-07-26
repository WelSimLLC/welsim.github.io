---
lang: en
layout: post
title:  "Quantities and units in general-purpose engineering simulation software"
date:   2023-07-26
author: "[SimLet](https://twitter.com/getwelsim)"
---

General-purpose engineering simulation software or CAE software, due to its coverage of different physics and engineering computations, involves a large number of quantities and units. While solvers generally do not consider units, the front-end GUI focuses on improving user experience by incorporating the unit module as a key development aspect.

<p align="center">
  <img src="\assets\blog\20230726\welsim_quantities_demo.png" alt="welsim_quantities_demo" />
</p>

The industry often compares the development of CAD and CAE software. Quantities and units may be one of the most significant differences between the two. CAD software typically deals with only length and angle units, while large-scale simulation CAE software may involve more than 50 different quantities. Additionally, each quantity can have multiple units, resulting in nearly a thousand different units encompassed by CAE software. UnitConverter, MatEditor, and WELSIM have supported various complex unit systems and conversions for many years, ensuring precise calculations. See the article (A Free Unit Converter App for Engineers)[https://welsim.com/2019/06/17/a-free-unit-converter-app-for-engineers.html] for more information. The development effort for the unit module is not only enormous, but even a small issue in the unit module can lead to significant errors  in the calculation results. Unit is an important module in CAE software development that cannot be overlooked.


The difficulty in developing the units module lies in the need for collaboration between developers with different backgrounds. The unit module requires developers who understand various engineering and physics aspects, as well as numerical methods and the development of large-scale software. This places high demands on product managers and the development team's collaboration. This article, based on our many years of developing WELSIM, summarizes the commonly used quantities and units in modern large-scale simulation CAE software.


## Unit Systems

Given the numerous quantities  and units, categorizing them using unit systems is an effective method. As shown in the figure below, we have classified 16 common unit systems, each of which specifies units for quantities. Currently, the WELSIM suite, including MatEditor and UnitConverter, already supports these 16 unit systems.

<p align="center">
  <img src="\assets\blog\20230726\welsim_unit_system.png" alt="welsim_unit_system" />
</p>

Among these unit systems, the most frequently used ones are
* SI (kg,m,s,C,A,N,V)
* Metric (g,cm,s,C,A,dyne,V)
* Metric (kg,mm,s,C,mA,N,mV)
* US Customary (lbm,in,s,F,A,lbf,V)
* US Customary (lbm,ft,s,F,A,lbf,V)

Some quantities may have multiple units even in the same unit system, such as temperature, angles, and angular velocity. Developers need to provide users with additional unit options for these quantities to facilitate analysis. As shown in the figure below, WELSIM offers Celsius and Kelvin options for temperature quantity (users can have Fahrenheit temperature using the US Customary unit system). For angle quantity, both degree and radian options are available, and for angular velocity, rad/s and RPM options are provided. This enables users from different backgrounds to perform simulation studies using the units they prefer.

<p align="center">
  <img src="\assets\blog\20230726\welsim_units.png" alt="welsim_units" />
</p>

There are also some less commonly used unit systems, such as the Gaussian unit system in electrodynamics, which are not elaborated on in this article due to their infrequent occurrence in engineering.


## Quantities and Units

Due to the numerous quantities involved in engineering simulation CAE software, we categorize units into seven major classes based on the analysis type: Basic, Common, Mechanical, Thermal, Electrical, Magnetic, and Fluid. Below, we introduce the common units in each category.

<p align="center">
  <img src="\assets\blog\20230726\welsim_unitconverter.png" alt="welsim_unitconverter" />
</p>

### Basic Units
Basic units serve as the foundation for all units, determining the form of other units and acting as fundamental quantities in unit conversions. They include Angles, Current, Length, Mass, Temperature, and Time.

### Common Units
Common units comprise Area, Volume, Density, Specific volume, Frequency, Energy, and Energy density.

### Mechanical Units
Mechanics units consist of Pressure, Force, Velocity, Acceleration, Angular velocity, Angular acceleration, Torque, Moment of inertia of mass, Momentum, Power, Stiffness, and Fracture toughness.

### Thermal Units
Thermal units cover Heat transfer coefficient, Thermal conductivity, Thermal expansivity, Heat flux, Heat flow, Heat generation, Heat capacity, Thermal radiation coefficient, Specific heat, Specific heat density, and Enthalpy.

### Electrical Units
Electrical units include Voltage, Charge, Surface charge density, Charge density, Permittivity, Electric field, Electric flux density, Capacitance, Surface current density, Conductivity, Conductance, and Inductance.

### Magnetic Units
Magnetic units encompass Permeability, Magnetic field strength, Magnetic flux density, and Magnetic potential.

### Fluid Units
Fluid units consist of Dynamic viscosity and Kinematic viscosity.

Currently, the WELSIM suite, including MatEditor and UnitConverter, supports all 54 quantities and units mentioned above.


## Conclusion

Quantities and units are essential modules in engineering simulation CAE software. Due to their scattered nature, they are often overlooked by developers during actual development. Moreover, the quantities and units module demands high precision. Even a minor issue in unit conversion can lead to completely erroneous solutions, with errors potentially spanning several orders of magnitude. Therefore, sufficient unit testing is necessary to ensure accuracy. Additionally, from a software engineering perspective, the unit module needs to be easy to expand and maintain. As CAE software undergoes iterative development with the continuous addition of features, new quantities and units will need to be incorporated.

---

<small>
WELSIM is the #1 engineering simulation software for the open-source community.
</small>
