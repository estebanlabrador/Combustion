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
>   - Eigenvalues tend to remain **horizontal**, but distribution width depend on mesh size \( h \) and Péclet number
>
> - For **BDF (Backward Differentiation Formula)**:
>   - Eigenvalues form either a **vertical line** or a **circular arc** centered in the negative real axis, depending on the mesh size \( h \) and Péclet number
>
> **IMPRKC** was chosen for its **robust vertical stability**, which ensured stable integration even when eigenvalues were vertically aligned—particularly relevant in high-Pe regimes or fine spatial meshes.

---

### 📊 Metrics Studied:
The focus of the analysis was to **evaluate when each time integration scheme performs well**, by studying **how the eigenvalues of the discretized PDE system align with the method's stability region**.
-**Spectral Radius and Stability Regions** – Analyzed to determine **whether the eigenvalues lie inside the method's stability domain**, ensuring numerical stability
- Flame Front Speed (via y = 0.5 interpolation)
- **Eigenvalue Distributions for varying β and c parameters** – Explored how **reaction rate (β)** and **convection strength (c)** affect the eigenvalue spread

---

## 📈 Key Results

### 🔍 Focus Area: Simulation Stability Assessment

I developed a **systematic method** to evaluate the **numerical stability** of convection-diffusion-reaction (CDR) simulations based on:
- **Discretization scheme** (spatial mesh size `h`)
- **Time integration method** (`RK2`, `Explicit Euler`, `IMPRKC`)
- **Physical parameters** of the equation ADD EQUATION
   - Reaction coefficient: `c`  
  - Convection coefficient: `β`  
  - Source term: `q`
 
The method identifies the **maximum stable time step (`Δt`)** that ensures convergence for each setup.

### ⚙️ Time Integration Methods Compared fpr a particular case
  - Reaction coefficient: `c = 1`  
  - Convection coefficient: `β = 10`  
  - Source term: `q = 5`
With this parameters the eigenvalue spread is horizontal.

### 1. RK2 (Second-Order Runge-Kutta)
Second-order explicit method with a **strict stability limit**. `Δt` decreases rapidly with mesh refinement.

| Mesh Size (`h`) | Max `Δt` |
|------------------|-----------|
| 0.1              | 0.004562  |
| 0.05             | 0.0012159 |
| 0.025            | 0.000317  |

---

### 2. Explicit Euler
Same behavior as RK2 due to its explicit nature.

| Mesh Size (`h`) | Max `Δt` |
|------------------|-----------|
| 0.1              | 0.004562  |
| 0.05             | 0.0012159 |
| 0.025            | 0.000317  |

---

### 3. IMPRKC (Improved Explicit Runge-Kutta-Chebyshev)
Specialized for **stiff systems**. Allows **significantly larger time steps**, scalable with the number of stages.

| nStages | `h = 0.1` | `h = 0.05` | `h = 0.025` | Notes                        |
|---------|-----------|------------|-------------|------------------------------|
| 5       | 0.03649   | 0.0097273  | 0.00248     | Cuts off at ~1e-16           |
| 10      | 0.14598   | 0.0389     | 0.0099255   | Cuts off at ~1e-64           |
| 20      | 0.593     | 0.15807    | 0.0403224   | Cuts off at ~1e-260          |
| 50      | 3.695     | 0.984888   | 0.251239    | Cuts off at ~1e-1620         |

####🧠 Insight Summary

- For **explicit methods (Euler, RK2)**, stability limit scales with `h²` — expected for diffusion-dominated problems.
- **IMPRKC** dramatically improves stability for stiff PDEs and fine meshes by increasing `nStages`.
- This approach enables **pre-simulation filtering** of unstable configurations, boosting simulation efficiency and robustness.


---

## 🔄 Next Steps

- Extend models to **2D geometries** with complex boundary conditions  
- Perform **experimental validation** using lab-scale flame setups  
- Apply findings to **real-world ignition systems** and flame control applications  

---

📎 *This repository is part of a collaboration project on reactive transport modeling in combustion, with emphasis on numerically stable solvers for convection–diffusion–reaction systems in stiff regimes.*
