# Test 3 — Steady Kovasznay flow

## Problem definition

Consider the steady incompressible Navier–Stokes equations in nondimensional, unit-density form:

$$
\begin{aligned}
-\nu\Delta\mathbf{u}+(\mathbf{u}\cdot\nabla)\mathbf{u}+\nabla p &= \mathbf{0},\\
\nabla\cdot\mathbf{u} &= 0,
\end{aligned}
$$

where $\mathbf{u}=(u,v)^T$, $\rho=1$, $\nu=1/Re$, and there is no body force. The computational domain and Reynolds number are

$$
\Omega=(-0.5,1)\times(-0.5,1.5),\qquad Re=2400.
$$

## Analytical solution and boundary conditions

The Kovasznay analytical fields are

$$
\begin{aligned}
u(x_1,x_2)&=1-e^{\lambda x_1}\cos(2\pi x_2),\\
v(x_1,x_2)&=\frac{\lambda}{2\pi}e^{\lambda x_1}\sin(2\pi x_2),\\
p(x_1,x_2)&=\frac12\left(1-e^{2\lambda x_1}\right),
\end{aligned}
$$

where

$$
\lambda=\frac{Re}{2}-\sqrt{\frac{Re^2}{4}+4\pi^2}.
$$

The analytical velocity is imposed as the Dirichlet boundary data over the domain boundary. The analytical velocity and pressure fields are used for error assessment.

## Numerical configuration in the manuscript

- Initial mesh: structured crossed triangular mesh with $N_x=120$ and $N_y=150$ subdivisions.
- Spatial interpolation: equal-order continuous $\mathbb{P}_1/\mathbb{P}_1$ velocity–pressure elements.
- Finite element formulations considered: standard Galerkin and SUPG/PSPG/LSIC stabilized finite elements.
- Adaptation monitor: recovered Hessians of both velocity components and the LSIC activity $I_{\mathrm{LSIC}}=\tau_{\mathrm{LSIC}}\lvert\nabla\cdot\mathbf{u}^h\rvert$ extracted from the stabilized solution.
- Monitor parameters: $\theta=0.9$, $\alpha=2$, $\widetilde{p}=0.30$.
- UM2N adaptation: a single mesh movement followed by recomputation of the stabilized flow solution.

## Solver implementation

**Work in progress.** The solver code, setup instructions, and reproducibility workflow for this benchmark are being prepared and will be added later. No implementation files or numerical figures are included in this folder yet.
