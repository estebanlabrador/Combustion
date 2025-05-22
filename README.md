# Reactive Transport Modeling in Combustion Systems

- **Institution**: Polytechnic University of Madrid  
- **Duration**: January 2024 – June 2024  
- **Advisor**: Jaime Carpio  
- **Tools Used**: MATLAB, Custom 1D Solvers, Eigenvalue Analysis, RK Schemes

---

## 🌍 Project Objective

Simulate and analyze the **stability and propagation** of reactive flows using time integration methods tailored to **stiff PDE systems**. The project focused on understanding how numerical methods perform under varying eigenvalue distributions—especially in **convection–diffusion–reaction** problems where time integration stability is a bottleneck.

---

## ⚙️ Technical Highlights

### 🔬 Models Solved:
- Adiabatic flame temperature of **H₂ combustion**
- Nonlinear chemical oscillators: **Brusselator**, **Van der Pol**
- Flame propagation and detonation wave modeling
- **Primary Focus**: Stability of **convection–diffusion–reaction** PDEs under stiff regimes

### ⏱️ Time Integration Schemes:
- Explicit Euler
- Implicit Euler
- Runge-Kutta-Chebyshev (**RKC**)
- **Improved RKC (IMPRKC)** – implemented for its enhanced **vertical stability**, critical for handling vertically distributed eigenvalue spectra in high Péclet number regimes.

> 💡 **Eigenvalue-aware method selection**: Depending on the **Péclet number**, the convection–diffusion system's eigenvalues shift in orientation:
> - **Low Pe** → eigenvalues distributed horizontally
> - **High Pe** → eigenvalues shift vertically
> IMPRKC was chosen to ensure robust stability across both regimes.

### 📊 Metrics Studied:
- L² Error Analysis
- Spectral Radius and Stability Regions
- Flame Front Speed (via y = 0.5 interpolation)
- Eigenvalue Distributions for varying β and c parameters

---

## 📈 Key Results

| Focus Area                 | Insight                                                                 |
|---------------------------|-------------------------------------------------------------------------|
| **Adiabatic Flame Temp**  | Accurate predictions using Newton solver with variable Cp and air vs. O₂ |
| **Van der Pol Oscillator**| Implicit schemes allowed for larger time steps without loss of stability |
| **Conv-Diff-Reaction**    | IMPRKC enabled stable steps ~10× larger than Euler with similar accuracy |
| **Flame Front Speed**     | Interpolated at y = 0.5 for propagation tracking                        |
| **Detonation Modeling**   | Captured shock-like behavior and validated through spectral analysis     |

---

## 🔄 Next Steps

- Extend models to **2D geometries** with complex boundary conditions  
- Perform **experimental validation** using lab-scale flame setups  
- Apply findings to **real-world ignition systems** and flame control applications  

---

📎 *This repository is part of a collaboration project on reactive transport modeling in combustion, with emphasis on numerically stable solvers for convection–diffusion–reaction systems in stiff regimes.*
