---
lang: en
layout: post
title:  "Modal Finite Element Analysis of Rotating Machine Blades"
date:   2019-06-07
author: "[SimLet](https://twitter.com/getwelsim)"
---

The blade design plays an essential role in the operation of the rotating machine. For example, the centrifugal force will increase as the turbine rotating speed increases, and sometimes the operating environment temperature is high. Under such high pressure and high-temperature conditions, the design of the turbine blades is particularly important.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*ss9A6DgTOBL3KW2PfQUjwg.png"/>
</p>

For rotating equipment, in addition to the fundamental dynamic and static balance requirements, the finite element simulation method can analyze the vibration and strength of the blade, and understand the vibration and dynamic characteristics of the blade through modal analysis.

The general-purpose finite element software WELSIM provides modal analysis features. With simple setup, the user can easily, quickly and accurately obtain the natural frequency and mode shape of the structures. Let’s take a turbine blade as an example to see how to perform the modal analysis.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*sD3N3KzcCxfTeZkm1Jgs1w.png"/>
</p>

Start the WELSIM software application. First set the material properties. Add a material object and name it myMat, set Young’s modulus to 9.7e7 kg/(mm s2), Poisson’s ratio of 0.3, the mass density of 4.72e-6 kg/mm3. This is a titanium alloy material.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*ezaKes-OE00l_cEkWksnnw.png"/>
</p>

Set the analysis type. In the FEM project object, set the Analysis Type property to Modal.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*pTgvu8UYf3DAVvs9WHf7MQ.png"/>
</p>

Create a rotor model by importing a STEP file. And assign the “myMat” to the Material property, as the picture shows:

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*eTdZRAB7ka1yFXihHwsdTw.png"/>
</p>

In the Mesh Settings, use a high-order (Quadratic) element. A total of 483,163 nodes and 281,050 Tet10 elements were generated.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*wWVO_UYIRQ4P-ASsEldvug.png"/>
</p>

For a three-dimensional structure without constraints, the natural frequencies of the first six orders are zero. To understand the natural frequency and mode shape of the blade under actual conditions, we impose constraint boundary conditions to blade surfaces that are connected to the rotor. As the picture shows,

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/600/1*V1ivX0kam5rGFHSqDySETQ.png"/>
</p>

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/600/1*KHrvp_WH9sN1W6kuiLxzZQ.png"/>
</p>

Click the Compute button. The system defaults to calculate the first six modes, so we add six result objects to view the resonant shape separately.

The first-order mode has a natural frequency of 2286.3 Hz.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*vfyOvB_2G5flVqDkN9NG9g.png"/>
</p>

The second-order mode has a natural frequency of 3201 Hz.

<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*WBwxj5VLW9bB_f6CUlnahg.png"/>
</p>

The third-order mode has a natural frequency of 5206.1 Hz.
<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*KDOTP7eYRB97NMZeLQxxlg.png"/>
</p>

The fourth-order mode has a natural frequency of 5744 Hz.
<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*5QCO1DZKGqI0-LNgQ7Up6g.png"/>
</p>

The fifth-order mode has a natural frequency of 6784.4 Hz.
<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*2hJFVGFefq0ba4ta3FAUEg.png"/>
</p>

The sixth-order mode has a natural frequency of 8213.2 Hz.
<p align="center">
  <img src="https://cdn-images-1.medium.com/max/800/1*YAUoRtIpqpaCkPxXKK9H0w.png"/>
</p>

Note that the value of the deformation result here is not a real deformation, but a relative reference value. The table window on the right and the curve window at the bottom also list the specific natural frequency values.

This example is saved in examples/v18/modal/modal_turbine_blade.wsdb in the installation directory. If you have any suggestions or comments about WELSIM’s modal analysis, please leave us a message or visit [https://welsim.com](https://welsim.com).



