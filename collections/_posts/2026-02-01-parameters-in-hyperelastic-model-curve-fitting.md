---
lang: en
layout: post
title:  "Parameters in hyperelastic model curve fitting"
date:   2026-01-31
author: "[SimLet](https://twitter.com/getwelsim)"
---


Many tasks in finite element analysis require curve fitting. Especially in materials engineering, when only experimental test data is available, engineers must perform curve fitting to determine the parameters in a given numerical model. Common types of material curve fitting include hyperelastic, plastic, viscous, core loss materials, and more.
<p align="center">
  <img src="\assets\blog\20260201\welsim_curvefitter_demo_ogden3.png" alt="welsim_curvefitter_demo_ogden3" />
</p>

Unlike other types of curve fitting, curve fitting for finite element material models requires both a small error and physically valid fitted parameters; furthermore, these parameters must be conducive to convergence in subsequent nonlinear finite element computation. As a result, there are high standards placed on the algorithms and details of parameter fitting.

Rarely do articles discuss the parameters, initial values, and reasonable bounds for hyperelastic model parameters despite their importance when implementing hyperelastic model curve fitting and verifying the rationality of fitted parameters. From a development perspective, this article discusses how to better perform curve fitting for hyperelastic material models, with a particular focus on setting parameter bounds and initial values, as well as identifying the characteristics of reasonable parameters.

Due to the large number of hyperelastic models and order-dependent variation, this article describes the computational details of each hyperelastic model in separate sections to avoid confusion.

## 1. neo-Hookean
The neo-Hookean model is first because it is one of the most simple and classic hyperelastic models. Many other models can be simplified to the neo-Hookean model under specific parameter conditions. Its strain energy density function W is expressed as:
<p align="center">
  <img src="\assets\blog\20260201\welsim_mateditor_eqn_neo_hookean.png" alt="welsim_mateditor_eqn_neo_hookean" />
</p>

where μ is the shear modulus. During curve fitting computation, the shear modulus must be greater than zero, i.e., μ>0. The initial value is set to μ0​=E/3, where Young's modulus E can be obtained from the slope of the stress-strain curve near the origin (strain < 5%).
<p align="center">
  <img src="\assets\blog\20260201\welsim_mateditor_curvefit_neohookean.png" alt="welsim_mateditor_curvefit_neohookean" />
</p>


To check for physical validity after parameter fitting, you can refer below for the approximate correspondence between common hyperelastic materials and μ:

| --- | --- |
| **Material Type**      | **Shear Modulus μ (MPa)** |
| Extra-soft Rubber      | 0.3 ~ 0.5 |
| Medium-hardness Rubber | 1.0 ~ 1.5 |
| Hard Rubber            | 3.0 ~ 5.0 |
| Biological Soft Tissue | 0.01 ~ 0.1 |

A fitted parameter μ that differs significantly from the uniaxial tension data indicates that the material may exhibit a strong second strain invariant effect, in which the Mooney-Rivlin or other suitable models should be used instead.

## 2. Mooney-Rivlin
The Mooney-Rivlin model is another one of the most commonly used hyperelastic models in engineering analysis. It is a direct extension of the neo-Hookean model and is characterized by its simple and flexible form. If the neo-Hookean is considered the entry-level model in hyperelasticity, then the Mooney-Rivlin would be the standard model for handling small-to-moderate deformations (100%-200% strain). Its simple mathematical form and linear dependence on material constants allows it to converge easily in Finite Element Analysis (FEA) calculations.

Depending on the order, the Mooney-Rivlin model has several different forms with varying amounts of parameters, the most complex being the 9-parameter model. This section uses the 9-parameter Mooney-Rivlin model as an example to discuss parameter ranges and initial value settings. Its strain energy density function W includes all combinations from linear to cubic terms:
<p align="center">
  <img src="\assets\blog\20260201\welsim_mateditor_eqn_mooney_rivlin9.png" alt="welsim_mateditor_eqn_mooney_rivlin9" />
</p>


Physically, the shear modulus μ>0. Therefore, μ=2(C10​+C01​)>0. The most robust constraint for practical calculations is C10​>0 and C01​≥0. In many rubber materials, C10​ is the dominant term, and C01​ is relatively small; C11​ is also usually positive. The third-order parameter C30​≥0. C03​, C21​, C12​ can capture the sharp stiffening at extremely large deformations (strain > 400%) and are generally 3–4 orders of magnitude smaller than the first-order parameters.
<p align="center">
  <img src="\assets\blog\20260201\welsim_mateditor_curvefit_mr9.png" alt="welsim_mateditor_curvefit_mr9" />
</p>


Regarding initial conditions, C10​=0.9×(μ0​/2), C01​=0.1×(μ0​/2), with the initial shear modulus μ0​=E/3. The initial values for C11​, C20​, C02​, C30​, C21​ are often chosen to be small, typically 0.1% of C10​. The initial values for C12​ and C03​ can be set to zero. For most synthetic rubbers (e.g., NBR, EPDM, Neoprene), the parameters generally follow the order-of-magnitude rules below:

| --- | --- | --- |
| **Order Classification** | **Parameter Symbol** | **Typical Value Range (MPa)** |
| 1st-order (Linear)     | C10​,C01          | ​0.1 ~ 2.0 | 
| 2nd-order (Transition) | C20​,C11​,C02      | ​-0.2 ~ 0.2 | 
| 3rd-order (Stiffening) | C30​,C21​,C12​,C03  | ​-0.05 ~ 0.1 |

The Mooney-Rivlin model has its limitations. When rubber is stretched to its limit (molecular chains fully extended), the stress rises sharply (the "upturn" phenomenon). The Mooney-Rivlin model cannot account for this stiffening at high strains; the Ogden or Gent model is recommended when simulating extremely large deformations (strain > 300%). If the experimental data is not comprehensive, a more robust model with fewer parameters is advised, such as the Yeoh model or the 5-parameter Mooney-Rivlin model.


## 3. Yeoh
The Yeoh hyperelastic model is known for its simplicity and stability. It discards the second invariant I2​ (terms like C01​), which is highly susceptible to experimental error, retaining only the first invariant I1​. Therefore, it is more robust than the Mooney-Rivlin model when fitting large-deformation data. The strain energy density function W is as follows:
<p align="center">
  <img src="\assets\blog\20260201\welsim_mateditor_eqn_yeoh.png" alt="welsim_mateditor_eqn_yeoh" />
</p>

Common Yeoh models are 1st to 3rd-order, with 1 to 3 parameters respectively. During fitting, C10​>0 is required since the material loses shear resistance and crashes the simulation immediately if C10​≤0. C20​ is usually negative; its magnitude is not too large and can be constrained to be greater than 1% of C10​. C30​ is positive and is used to capture the stiffening at large strain.
<p align="center">
  <img src="\assets\blog\20260201\welsim_mateditor_curvefit_yeoh3.png" alt="welsim_mateditor_curvefit_yeoh3" />
</p>


The initial value settings are relatively simple: the initial value of C10​ is E/6, where Young's modulus E is the slope of the test data at small deformations. C20​=−0.1×C10​, C30​=0.01×C10​.

The parameters of the Yeoh model for common materials are as follows:

| --- | --- | --- | --- | --- | 
| **Material Type/Hardness** | **C10​ (MPa)**  | **C20​ (MPa)** | **C30​ (MPa)** | **Description** | 
| Ultra-soft Silicone/Gel | 0.01 ~ 0.1 | –0.001 ~ -0.01 | 0.0001 ~ 0.01 | Very low initial modulus, stiffening occurs late. |
| Natural Rubber (40A-50A) | 0.2 ~ 0.5 | –0.02 ~ -0.1 | 0.01 ~ 0.05 | Good ductility, obvious plateau in the mid-curve. |
| Industrial-grade Rubber (60A-70A) | 0.6 ~ 1.2  | –0.1 ~ -0.5    | 0.1 ~ 0.5     | Medium stiffness, commonly used for tire sidewalls or seals. |
| High-hardness Elastomer (80A+) | 1.5 ~ 5.0  | –0.5 ~ -2.0    | 0.5 ~ 2.0     | Stiffening occurs very early, curve is steep. | 


## 4. Polynomial
The Polynomial hyperelastic model is also based on the power series expansion of the strain energy density function W with respect to the invariants I1​ and I2​. It is one of the most widely used frameworks in hyperelasticity theory, and many models (Mooney-Rivlin, Yeoh, Neo-Hookean) are essentially its special cases. The general strain energy density function W is expressed as:
<p align="center">
  <img src="\assets\blog\20260201\welsim_mateditor_eqn_polynominal.png" alt="welsim_mateditor_eqn_polynominal" />
</p>

where N is the order of the model. Common polynomial models are 1st to 3rd-order, corresponding to 2, 5, and 9 parameters. Like the Mooney-Rivlin model, during fitting, it is necessary for C10​>0 and C10​>∣C01​∣. C30​ is also usually required to be positive. Generally, the higher the order, the smaller the magnitude of the values. The reasonable parameter ranges for hyperelastic materials are shown below.

| --- | --- | --- | --- |
| **Parameter Category**           | **Parameter Item** | **Typical Range (MPa)** | **Physical Behavior Description** | 
| Base Modulus                 | C10            | ​0.1 ~ 0.6           | Dominates small-to-medium deformation stiffness, usually positive. |
| Shear Correction             | C01​            | 0.01 ~ 0.1          | Corrects shear behavior, usually positive.
| Mid-range Adjustment         | C20            | ​-0.05 ~ 0.05        | Controls slope change in the mid-curve, often negative. |
| Large-deformation Stiffening | C30            | ​0.001 ~ 0.01        | Controls the upturn stiffening at very high strains, must be positive. |
| Coupling Terms               | C11​,C02        | ​-0.01 ~ 0.01        | Cross-effects between I1​ and I2​, usually close to zero. | 

For initial value settings, set C10​=E/6. C20​=−0.1×C10​, C30​=0.01×C10​ or smaller. Although the value of C30​ is small, its high power amplifies its impact on the end of the curve.


## 5. Arruda-Boyce
The Arruda-Boyce model is unique in hyperelastic material simulation, and it is constructed based on statistical mechanics (molecular chain network theory). The strain energy density function W is expressed as:
<p align="center">
  <img src="\assets\blog\20260201\welsim_mateditor_eqn_arruda_boyce.png" alt="welsim_mateditor_eqn_arruda_boyce" />
</p>

A key feature of this model is its low requirement for test data, and uniaxial data alone is sufficient to start. Unlike polynomial models that require multi-axial data to determine parameters, the Arruda-Boyce model's parameters have clear physical definitions, in which relatively accurate μ and λm​ can usually be obtained from the high-quality uniaxial tension data.


The value range for the initial shear modulus μ is straightforward; it must be greater than 0 and lie between 0.1~5 MPa, with common values for rubber materials ranging from 0.5~1.5 MPa. λm​ must be greater than and typically limited to [1.1, 20]. The model becomes extremely stiff when λm​ is too close to 1, leading to highly unstable numerical calculations. For most industrial rubbers, setting λm​ between 3.0 and 7.0 usually covers most working conditions.
<p align="center">
  <img src="\assets\blog\20260201\welsim_mateditor_curvefit_arruda_boyce.png" alt="welsim_mateditor_curvefit_arruda_boyce" />
</p>

Initial value determination is also straightforward: set μ=E/3. λm​=5 is a robust starting point.

Typically, the Arruda-Boyce parameters correspond to rubber materials as follows:

|---|---|---|
| **Material** | **μ (MPa)** | **λm** |
| Soft Rubber (Shore 30A - 40A) | 0.3 ~ 0.6 | 5.0 ~ 8.0 |
| Medium-hardness (Shore 50A - 60A) | 1.0 ~ 2.5 | 3.0 ~ 5.0 |
| Hard Rubber (Shore 70A - 80A)  | 3.0 ~ 8.0 | 1.5 ~ 2.5 |


## 6. Blatz-Ko
The Blatz-Ko model is a simple model used to simulate foams and porous materials. The most commonly used form contains only one parameter, the shear modulus μ.
<p align="center">
  <img src="\assets\blog\20260201\welsim_mateditor_eqn_blatz_ko.png" alt="welsim_mateditor_eqn_blatz_ko" />
</p>

Like other hyperelastic models, the shear modulus must be greater than zero. Poisson's ratio ν is fixed as a theoretical property of this model is that its effective Poisson's ratio is locked at approximately 0.25. This means the material is assumed to shrink significantly in volume when compressed, rather than expanding sideways like ordinary rubber. Do not use the Blatz-Ko model for solid rubber (Poisson's ratio near 0.5, incompressible).

As long as the Blatz-Ko model ensures that the shear modulus μ is positive (μ>0) and the material is indeed a compressible foam, fitting is usually straightforward.

Since Poisson's ratio ν is often fixed at 0.25, according to the linear elastic conversion relationship: μ = E/[2(1+ν)] = E/2.5 = 0.4E. The initial value can be set to 0.4E.

Typically, the shear modulus corresponds to the materials as follows:

|---|---|---|
| **Material Type**  | **μ Value Range (MPa)** | **Description** | 
| Ultra-light Polyurethane Foam  | 0.05 ~ 0.5          | Extremely low density, highly compressible. | 
| Medium-density Foamed Rubber   | 0.5 ~ 2.0           | Common for shock pads and packaging. | 
| High-hardness Closed-cell Foam | 2.0 ~ 10.0          | Structural support foam, high stiffness. | 
| Solid Compressible Rubber      | 10.0+               | Special synthetic rubbers with voids. | 


## 7. Gent
The Gent model is a physically based hyperelastic model, similar in behavior to the Arruda-Boyce model. Its greatest advantage is its simple form, which can effectively capture the nonlinear behavior of polymer chains reaching their limiting extension length using only two constants. The mathematical form of the Gent model is a logarithmic function, and the computational cost for curve fitting is lower than that of the Arruda-Boyce model.

The Gent model has only two core parameters: μ (initial shear modulus) and Jm​ (limiting invariant). Its strain energy density function is defined as:
<p align="center">
  <img src="\assets\blog\20260201\welsim_mateditor_eqn_gent.png" alt="welsim_mateditor_eqn_gent" />
</p>

The parameter μ must be greater than 0; Jm​ must be greater than the maximum measured value of I1​−3. If Jm​ is too small, causing (I1​−3)/Jm ​≥ 1, the logarithm becomes undefined, so the calculation will fail.

The initial value of the shear modulus μ is simply determined by μ=E/3. Mathematically, Jm​ defines the upper limit for I1​−3, so its initial value must be slightly larger than the invariant value corresponding to the maximum deformation observed in the experiment. To determine this, find the maximum elongation ratio λmax​ in the experimental data and calculate the corresponding I1​. Note that the formula for I1​ varies slightly depending on the type of experiment. The initial value of Jm​ is set to 1.2×(I1_max​−3).

The empirical parameters for materials of different hardness are as follows:

| --- | --- | --- | --- | 
| **Material Hardness/Type** | **Shear Modulus μ (MPa)** | **Limiting Constant Jm** | **Description** | 
| Ultra-soft Gel/Soft Tissue    | 0.01 ~ 0.15           | 0 ~ 150              | Extremely stretchable, stiffens very late.| 
| Natural Rubber (40A)          | 0.3 ~ 0.6             | 30 ~ 80              | Excellent ductility, high stiffening point.| 
| Industrial Rubber (60A)       | 1.0 ~ 2.0             | 10 ~ 25              | Medium stiffness, stiffens rapidly after 3–4x stretch.| 
| High-hardness Elastomer (80A) | 3.0 ~ 7.0             | 2 ~ 8                | Stiffens within a very short distance, increased brittleness.| 

## 8. Ogden
The Ogden hyperelastic model is one of the most powerful and flexible hyperelastic models available today. It is constructed directly based on the principal stretches λi​. The strain energy density function of the Ogden model adopts a series superposition form expanded by order n, where n represents the model order.
<p align="center">
  <img src="\assets\blog\20260201\welsim_mateditor_eqn_ogden.png" alt="welsim_mateditor_eqn_ogden" />
</p>

* 1st-order Ogden: 2 parameters, suitable for small deformations and simple rubber materials, highest computational efficiency.
* 2nd-order Ogden: 4 parameters, balances accuracy and efficiency, mainstream for general industrial simulations.
* 3rd-order Ogden: 6 parameters, suitable for large-deformation, highly nonlinear complex elastomers, highest fitting accuracy. The Ogden model maintains solid predictive capability even when strains reach 700% or higher.

The Ogden model has relatively more parameters, and higher-order versions require combined fitting of multiple sets of test data, such as uniaxial, pure shear, and equibiaxial, to prevent non-physical solutions and overfitting. Parameters must satisfy thermodynamic stability constraints, and reasonable bounds must be set during fitting. For example, set μ1​>∣μ2​∣>∣μ3​∣, 1<α1​<10, −10<α2​<10, −15<α3​<15.
<p align="center">
  <img src="\assets\blog\20260201\welsim_mateditor_curvefit_ogden3.png" alt="welsim_mateditor_curvefit_ogden3" />
</p>


Initial values for curve fitting are often set as follows: α1​=2, α2​=2, α3​=6, μ1​=0.6μ0​, μ2​=0.1μ0​, μ3​=0.05μ0​, where the initial shear modulus μ0​=E/3. Young's modulus E is obtained from the slope of the test data at low strains.

The empirical data fitted by common Ogden hyperelastic models is as follows:

| --- | --- | --- | --- |
| **Material Type**         | **Parameter** | **Typical Value Range** | **Description** |
| Soft Rubber / Silicone | μ         | 0.01 ~ 0.5 MPa      | Low modulus, gentle curve. |
|                        | α         | -10 ~ 10            | Usually includes positive and negative exponents to fit tension/compression symmetry. |
| Industrial Hard Rubber | μ         | 1.0 ~ 10.0 MPa      | High stiffness, large initial slope from combined μ. |
|                       | α         | 1.5 ~ 20            | Large positive exponents to simulate severe stiffening at large deformations. |
| Biological Soft Tissue | μ         | 0.001 ~ 0.1 MPa     | Extremely soft, highly sensitive to small deformations. |
|                       | α         | 10 ~ 50             | Exponents are usually very large to simulate the "lock-up" effect of fibrous connective tissue. |

## Conclusion
Although curve fitting has relatively mature numerical methods, fitting material parameters for finite element computation requires the consideration of many physical constraints, ensuring that the parameters are conducive to convergence in subsequent finite element calculations. Oftentimes due to the lack of test data, curve fitting for hyperelastic materials becomes complex which places high demand on both developers and users.

The main test data required for hyperelastic material model fitting includes uniaxial tension, equibiaxial tension, and pure shear deformation data. The author discusses this in detail in the article "[Hyperelastic Material Models and Curve Fitting](https://welsim.com/2020/07/23/hyperelastic-material-models-and-curve-fitting.html)".

Currently, WELSIM can accurately fit hyperelastic model curves. The independent and free engineering software MatEditor and CurveFitter also feature the aforementioned curve fitting capabilities. Users can download and use this software directly.


---
