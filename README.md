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
> The eigenvalue distribution of the convection–diffusion operator depends on both the **discretization scheme** and the **Péclet number (Pe)**:
>
> - Using **first-order upwind** for convection:
>   - **Low Pe** → eigenvalues are distributed **horizontally** (near the real axis, \( y = 0 \))
>   - **High Pe** → eigenvalues stretch **vertically** (down the negative x-axis)

<p align="center">
  <img src="./primerorden.png" alt="Eigenvalue distribution for first-order upwind scheme" width="45%" />
</p>

<p align="center">
  <em>Eigenvalue spectrum for first-order upwind scheme</em>
</p>

> - Using **centered differences**:
>   - Eigenvalues tend to remain **horizontal**, but the distribution width depends on the mesh size \( h \) and Péclet number

<p align="center">
  <img src="./difcentradas.png" alt="Eigenvalue distribution for centered difference scheme" width="45%" />
</p>

<p align="center">
  <em>Eigenvalue spectrum for centered differences</em>
</p>

> - For **BDF (Backward Differentiation Formula)**:
>   - Eigenvalues form either a **vertical line** or a **circular arc** centered on the negative real axis, depending on mesh size \( h \) and Péclet number



> **IMPRKC** was chosen for its **enhanced vertical stability**, which is critical for stiff problems where eigenvalues align along the imaginary axis—typical in **high-Pe regimes** or with **fine spatial meshes**.
>
> In standard **RKC** methods, the **number of stages** `nst` determines the extent of the stability region. The **improved variant**, **IMPRKC**, introduces a modified stage structure (`nst_g`) that significantly **widens the stability region along the vertical axis** of the complex plane. This allows the method to integrate more stiff systems efficiently without sacrificing stability.

<p align="center">
  <img src="./imprkc.png" alt="Stability region comparison for RKC and IMPRKC methods" width="45%" />
</p>

<p align="center">
  <em>Stability regions of RKC and IMPRKC methods. IMPRKC extends vertical stability via generalized staging (nst_g).</em>
</p>



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
- **Physical parameters** of the equation:
  \[
\frac{\partial u}{\partial t} + \beta \frac{\partial u}{\partial x} - \alpha \frac{\partial^2 u}{\partial x^2} + c u = q
\]

Where:
- `c` is the reaction coefficient  
- `β` is the convection coefficient  
- `q` is the source term  
- `α` is the diffusion coefficient (assumed constant and incorporated implicitly in spatial discretization)
 
 
The method identifies the **maximum stable time step (`Δt`)** that ensures convergence for each setup.

### ⚙️ Time Integration Methods Compared (for a Particular Case)
  - Reaction coefficient: `c = 1`  
  - Convection coefficient: `β = 10`  
  - Source term: `q = 5`

> With these parameters, the eigenvalue spectrum is **horizontally spread**, dominated by convection and reaction terms.


### 1. RK2 (Second-Order Runge-Kutta)
Second-order explicit method with a **strict stability limit**. `Δt` decreases rapidly with mesh refinement.

| Mesh Size (`h`) | Max `Δt` |
|------------------|-----------|
| 0.1              | 0.004562  |
| 0.05             | 0.0012159 |
| 0.025            | 0.000317  |



### 2. Explicit Euler
Same behavior as RK2 due to its explicit nature.

| Mesh Size (`h`) | Max `Δt` |
|------------------|-----------|
| 0.1              | 0.004562  |
| 0.05             | 0.0012159 |
| 0.025            | 0.000317  |



### 3. IMPRKC (Improved Explicit Runge-Kutta-Chebyshev)
Specialized for **stiff systems**. Allows **significantly larger time steps**, scalable with the number of stages. In this case, the results are **independent of `nst_g`**, meaning that even with the improved stage structure, the **maximum stable time step (`Δt`)** remains the same as in the standard RKC method.

| nStages | `h = 0.1` | `h = 0.05` | `h = 0.025` | 
|---------|-----------|------------|-------------|
| 5       | 0.03649   | 0.0097273  | 0.00248     |      
| 10      | 0.14598   | 0.0389     | 0.0099255   | 
| 20      | 0.593     | 0.15807    | 0.0403224   | 
| 50      | 3.695     | 0.984888   | 0.251239    | 


### 🧠 Insight Summary

- For **explicit methods** (Euler, RK2), the stability limit scales as `Δt ∝ h²`, which is typical for **diffusion-dominated** problems.
- **IMPRKC** greatly increases allowable time steps in **stiff** scenarios, especially when using higher `nStages`, making it ideal for convection-reaction dominated cases.
- The developed method supports **pre-simulation stability analysis**, allowing unstable combinations to be filtered out early—boosting **robustness and computational efficiency**.


---

## 🔄 Next Steps

- Extend models to **2D geometries** with complex boundary conditions  
- Perform **experimental validation** using lab-scale flame setups  
- Apply findings to **real-world ignition systems** and flame control applications  

---

📎 *This repository is part of a collaboration project on reactive transport modeling in combustion, with emphasis on numerically stable solvers for convection–diffusion–reaction systems in stiff regimes.*
