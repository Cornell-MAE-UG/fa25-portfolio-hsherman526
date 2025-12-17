---
layout: project
title: 2025 Wind Turbine Blade Design Project
description: Wind Turbine Blade Design & Wind Tunnel Testing 
technologies: [MATLAB, Autodesk Fusion]
image: /assets/images/blade.png


---



## Overview 
The goal of this project was to design a three-blade wind turbine to optimize power output at a specified design RPM based on a Weibull probability distribution for the free-stream wind velocity:

$$
p(U) = \frac{U^5}{4}\,\exp\!\left(-\frac{U^5}{5}\right)
$$


Design Constraints/Requirements: 
- Maximum blade length: **6 inches** (root to tip)
- Design RPM must not exceed **2000 RPM**
- Maximum allowable bending stress: **55 MPa**
- Blade geometry must be compatible with the provided hub attachment

---

## Design Process 

### Selection of Design Wind Speed

Power is proportional to the cube of velocity:

$$
P \propto U^3 = bU^3
$$

Using a change of variables on the Weibull velocity distribution:

$$
U = \left(\frac{P}{b}\right)^{1/3}, \quad
\frac{dU}{dP} = \frac{1}{3} b^{-1/3} P^{-2/3}
$$

The resulting power probability distribution function is:

$$
p(P) = \frac{P^{2/3}}{1875b}
\exp\left(-\frac{P^{5/3}}{3125b^{5/3}}\right)
$$

Maximizing the power PDF yields:

$$
P = 84.7b
$$

The corresponding wind speed producing the most probable power output is:

$$
U_{P_{\text{max}}} = \left(\frac{P}{b}\right)^{1/3} = 4.4 \text{ m/s}
$$


---

### Airfoil Selection

The NACA 7412 airfoil was selected because:

- It avoids ultra-thin sections that could fail during manufacturing (3d printing) 
- Increased camber compared to NACA 4412 improves resistance to operating conditions 
- It allowed exploration of a different airfoil than used in prior laboratory work


---

### Aerodynamic Forces 

Using a design wind speed of 4.4 m/s, an axial induction factor of 1/3, and an initial design RPM of 1800, aerodynamic forces were calculated to maximize useful torque: 

<div style="text-align: center;">
  <img src="{{ '/assets/images/flowchart.jpg' | relative_url }}"
       alt="Design Process Flowchart"
       style="max-width: 100%; height: auto;">
</div>


#### Velocity Relationships

$$
\phi(r) = \tan^{-1}\!\left(\frac{V}{\Omega r}\right)
$$

$$
\alpha(r) = \phi(r) - \theta(r)
$$

#### Aerodynamic Forces

$$
F_L = \frac{1}{2}\,\rho\,C_L\,V_{\text{eff}}^{2}\,A(r)
$$

$$
F_D = \frac{1}{2}\,\rho\,C_D\,V_{\text{eff}}^{2}\,A(r)
$$

Differential forces:

$$
dF_L = \frac{1}{2}\,\rho\,C_L\,V_{\text{eff}}^{2}\,c(r)\,dr
$$

$$
dF_D = \frac{1}{2}\,\rho\,C_D\,V_{\text{eff}}^{2}\,c(r)\,dr
$$

#### Force Projections

$$
dF_{\text{axial}} = dF_L \cos\phi + dF_D \sin\phi
$$

$$
dF_{\text{tangential}} = dF_L \sin\phi - dF_D \cos\phi
$$

#### Torque Calculations

$$
M_{\text{tangential}}
= \sum_{i=1}^{N} dF_{\text{tangential}}\, r_i
$$

$$
M_{\text{axial}}
= \sum_{i=1}^{N} dF_{\text{axial}}\, r_i
$$

#### Bending Stress

$$
\sigma(r) = \frac{M_{\text{axial}}(r)\, y(r)}{I(r)}
$$

Rectangular section approximations:

$$
I(r) = \frac{1}{12}\,t(r)\,c(r)^{3},
\qquad
y(r) = \frac{c(r)}{2}
$$


---

### Design Assumptions

- Incompressible flow (wind speeds < 15 m/s)
- Rectangular blade cross-sections for stress calculations
- Axial bending stress is the dominant failure mode
- No viscous boundary-layer losses
- No blade tip losses

---

### Blade Geometry and CAD Modeling

Discrete chord and pitch values were calculated at 29 spanwise locations. These were used to generate individual sketches in CAD, connected by 3D spline curves along the leading and trailing edges.

<div style="text-align: center;">
  <img src="{{ '/assets/images/blade.png' | relative_url }}"
       alt="Design Process Flowchart"
       style="max-width: 70%; height: auto;">
</div>

---

### Predicted Performance

Using the torque equations, predicted power curves were calculated for wind speeds from 4.2 m/s to 10.2 m/s. Maximum predicted power of 12 Watts occurred at 5.7 m/s, slightly above the design wind speed.

<div style="text-align: center;">
  <img src="{{ '/assets/images/predicted_power.jpg' | relative_url }}"
       alt="Design Process Flowchart"
       style="max-width: 70%; height: auto;">
</div>


---

## Testing Summary

Performance testing was conducted in the Big Blue Wind Tunnel. Torque, RPM, and power were recorded while varying wind speed and brake voltage.

$$
P = \tau\,\omega
$$


### Experimental Protocol

1. Increase wind tunnel speed until blades begin rotating
2. Adjust torque brake voltage to collect power data
3. Increment wind speed and repeat step 2
4. Ensure RPM remains below 3000 RPM
5. Collect at least five power curves across wind speeds

---

### Results and Reflections

<div style="text-align: center;">
  <img src="{{ '/assets/images/exp_data_1.png' | relative_url }}"
       alt="Design Process Flowchart"
       style="max-width: 90%; height: auto;">
</div>

<div style="text-align: center;">
  <img src="{{ '/assets/images/all_p_curves.png' | relative_url }}"
       alt="Design Process Flowchart"
       style="max-width: 90%; height: auto;">
</div>


The true operating RPM was determined to be 590 RPM, producing a maximum power output of 0.04 W with an efficiency of approximately 3%.

#### Performance Comparison

<table style="width: 50%; border-collapse: collapse; margin: 1em auto;">
  <thead>
    <tr style="background-color: #f2f2f2;">
      <th style="text-align: left; padding: 8px;">Metric</th>
      <th style="text-align: right; padding: 8px;">Predicted</th>
      <th style="text-align: right; padding: 8px;">Actual</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="padding: 8px;">Optimal RPM</td>
      <td style="text-align: right; padding: 8px;">1800</td>
      <td style="text-align: right; padding: 8px;">590</td>
    </tr>
    <tr>
      <td style="padding: 8px;">Max Power</td>
      <td style="text-align: right; padding: 8px;">12 W</td>
      <td style="text-align: right; padding: 8px;">0.04 W</td>
    </tr>
  </tbody>
</table>



The low performance was primarily due to incorrect blade twist orientation, causing the flow to impact the trailing edge first. Additionally, real-world losses such as viscous and tip losses were neglected in the model. Despite producing low power, the blade satisfied all design constraints and survived testing at 12.2 m/s, indicating structural robustness.

---

## My Contribution 
I developed the MATLAB model to iteratively choose the chord and pitch functions for the blade design. I also developed the MATLAB model to predict the operating performance of our blade and also post-processed our experimental data to produce the resulting experimental power curves.  
