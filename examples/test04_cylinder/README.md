# Test 4 — Unsteady incompressible flow around a circular cylinder

## Problem definition

Consider two-dimensional time-dependent incompressible Navier–Stokes flow in the channel-with-cylinder domain $\Omega$:

$$
\begin{aligned}
\frac{\partial\mathbf{u}}{\partial t}
+(\mathbf{u}\cdot\nabla)\mathbf{u}
-\nu\Delta\mathbf{u}+\nabla p &= \mathbf{0},\\
\nabla\cdot\mathbf{u} &= 0.
\end{aligned}
$$

The geometry consists of a channel of length $L=2.2$ and height $H=0.41$, excluding a circular cylinder of diameter $D=0.1$, centered at $(x_{1c},x_{2c})=(0.2,0.2)$.

## Initial and boundary conditions

The flow is initially at rest:

$$
\mathbf{u}(0,\mathbf{x})=\mathbf{0}\qquad\text{in }\Omega.
$$

At **both inlet and outlet**, the following time-dependent parabolic velocity is prescribed:

$$
\mathbf{u}(t,x_1,x_2)=
\frac{6\sin(\pi t/8)}{0.41^2}
\begin{bmatrix}
x_2(0.41-x_2)\\0
\end{bmatrix},
\qquad 0<t\leq8.
$$

No-slip velocity conditions are applied at the top and bottom channel walls and on the cylinder boundary. The pressure is normalized by

$$
\int_{\Omega}p\,\mathrm{d}\Omega=0.
$$

## Physical and numerical configuration in the manuscript

- Density: $\rho=1$; kinematic viscosity: $\nu=10^{-3}$; final time: $T=8$.
- Time-dependent mean velocity: $U(t)=\sin(\pi t/8)$; hence $U_{\max}=1$ and $0\leq Re(t)\leq100$ based on cylinder diameter.
- Initial mesh: straight-sided Gmsh triangular mesh with target element size $h=0.006$; **29,782 vertices** and **58,636 triangles**.
- Time integration: Crank–Nicolson, $\Delta t=5\times10^{-3}$ (**1,600 time steps**).
- Spatial discretization: equal-order $\mathbb{P}_1/\mathbb{P}_1$ velocity–pressure elements with SUPG/PSPG/LSIC stabilization.
- Adaptation monitor: hybrid recovered velocity-curvature and LSIC-activity indicator, with $\theta=0.25$, $\alpha=2$, $\widetilde{p}=0.30$.
- Adaptation strategies described in the manuscript: a one-time movement based on an indicator aggregated from $t=1,2,\ldots,8$, and an online approach that updates after every 100 time steps.
- Benchmark diagnostics: drag, lift, and the cylinder front-to-rear pressure difference $\Delta p(t)=p(t,0.15,0.2)-p(t,0.25,0.2)$.

## Solver implementation

**Work in progress.** The solver code, setup instructions, and reproducibility workflow for this benchmark are being prepared and will be added later. No implementation files or numerical figures are included in this folder yet.
