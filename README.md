# Cat Qubit Stabilization with Online Optimization

## Overview
This project demonstrates a real-time optimization system for stabilizing a cat qubit under hardware drift. The system continuously adjusts control parameters to maintain performance, maximize lifetime, and preserve bias.

Rather than performing a full quantum simulation, this implementation uses a **physics-informed model** to focus on adaptive control and optimization behavior in realistic noisy environments.

---

## Objective
The goal is to design and benchmark an online optimization algorithm that:

- Maintains qubit performance under hardware drift  
- Maximizes lifetimes:
  - \(T_X\) (X-error resistance)
  - \(T_Z\) (Z-error resistance)  
- Preserves target bias:
  \[
  \eta = \frac{T_Z}{T_X}
  \]

---

## Key Idea
The system tunes two complex control parameters:

- \( g_2 \): two-photon interaction strength (stabilization mechanism)  
- \( \epsilon_d \): drive amplitude (system control input)  

These are represented as four real control knobs:
- Re(\(g_2\)), Im(\(g_2\))
- Re(\(\epsilon_d\)), Im(\(\epsilon_d\))

The optimizer continuously updates these parameters to counteract drift and maintain stability.

---

## Optimization Algorithm
This project uses a **gradient-free, online optimization algorithm**:

1. Propose new parameters by adding noise (simulating drift)  
2. Evaluate system performance using:
   - \(T_X\), \(T_Z\), and bias \( \eta \)  
3. Compute reward:
   \[
   R = 0.7(T_X + T_Z) - 0.3|\eta - \eta_{target}|
   \]
4. Convert to loss:
   \[
   L = -R
   \]
5. Accept new parameters if they reduce loss  

---

## Optimization Strategies
Two strategies are implemented:

- **Greedy Optimization**
  - Only accepts improvements  
  - Stable but can get stuck  

- **Exploratory Optimization**
  - Occasionally accepts worse steps  
  - More adaptive under drift  

---

## Drift Modeling
Hardware drift is simulated using noise injected into control parameters at each time step.

The optimizer must continuously adapt to:
- parameter fluctuations  
- performance degradation  
- shifting system behavior  

---

## Features
- Real-time Streamlit dashboard  
- Adjustable hardware drift level  
- Adaptive stabilization system  
- Control parameter evolution tracking  
- Bias (\(\eta\)) monitoring  
- Two optimization strategies  
- Physics test mode (more realistic system behavior)  

---

## Metrics Explained

- **TX (Lifetime / Usage Time)**  
  Measures how long the qubit resists X-type errors  

- **TZ (Lifetime / Usage Time)**  
  Measures resistance to Z-type errors  

- **η (Bias Ratio)**  
  \[
  \eta = \frac{T_Z}{T_X}
  \]

Higher TX and TZ → longer usable quantum lifetime  
η near target → correct bias behavior  

---

## True Physics Test Mode
This mode uses a more realistic, physics-inspired model based on the system Hamiltonian.

- Slower than proxy mode  
- Better represents real system behavior  
- Useful for testing robustness of optimization  

---

## Algorithm Summary

We use a gradient-free, online optimization algorithm to stabilize the system:

1. Apply drift by perturbing control parameters  
2. Propose a new parameter set  
3. Compute performance metrics:
   - TX (lifetime)
   - TZ (lifetime)
   - η (bias ratio)  
4. Compute reward:
   R = 0.7(TX + TZ) - 0.3|η - η_target|  
5. Convert to loss:
   L = -R  
6. Update rule:
   - Greedy: accept only improvements  
   - Exploratory: occasionally accept worse steps  

This allows the system to adapt in real time under hardware drift.

---

## What This Demonstrates
This project shows that:

- Online optimization can stabilize a quantum system under drift  
- Control parameters can be tuned in real time  
- Lifetime and bias can be preserved simultaneously  
- Adaptive control is critical for quantum hardware  

---

## Tech Stack
- Python  
- Streamlit  
- NumPy  
- Matplotlib  

---
