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
- **Improved RKC (IMPRKC)** – implemented for its enhanced **vertical stability** in the complex plane.

> 💡 **Eigenvalue-aware method selection**:  
> The eigenvalue distribution of the convection–diffusion operator depends both on the **discretization scheme** and the **Péclet number (Pe)**:
>
> - Using **first-order upwind** for convection:
>   - **Low Pe** → eigenvalues distributed **horizontally** (near the real axis, \( y = 0 \))
>   - **High Pe** → eigenvalues stretch **vertically** (down the negative x-axis)
>
> - Using **centered differences**:
>   - Eigenvalues tend to remain **horizontal**, but distribution width increases with \( h \) and Pe
>
> - For **BDF (Backward Differentiation Formula)**:
>   - Eigenvalues form either a **vertical line** or a **circular arc** centered in the negative real axis, depending on the mesh size \( h \) and Péclet number
>
> **IMPRKC** was chosen for its **robust vertical stability**, which ensured stable integration even when eigenvalues were vertically aligned—particularly relevant in high-Pe regimes or fine spatial meshes.

---

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
