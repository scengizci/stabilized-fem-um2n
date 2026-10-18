# Test 2 — Two-dimensional transient viscous Burgers' equations

## Problem definition

On $\Omega=(0,1)^2$ and for $0<t\leq T$, solve the coupled nonlinear viscous Burgers' system

$$
\begin{aligned}
\frac{\partial u}{\partial t}
+u\frac{\partial u}{\partial x_1}
+v\frac{\partial u}{\partial x_2}
-\frac{1}{Re}\Delta u &= 0,\\
\frac{\partial v}{\partial t}
+u\frac{\partial v}{\partial x_1}
+v\frac{\partial v}{\partial x_2}
-\frac{1}{Re}\Delta v &= 0.
\end{aligned}
$$

Here $Re=10^4$, and the diffusion coefficient is $\nu=1/Re$.

## Analytical solution and boundary/initial conditions

The analytical solution, following the benchmark formulation used in the manuscript, is

$$
\begin{aligned}
u(x_1,x_2,t)
&=\frac34-\frac{1}{4\left[1+\exp\left(\frac{Re}{32}(4x_2-4x_1-t)\right)\right]},\\
v(x_1,x_2,t)
&=\frac34+\frac{1}{4\left[1+\exp\left(\frac{Re}{32}(4x_2-4x_1-t)\right)\right]}.
\end{aligned}
$$

- **Initial conditions:** the analytical solution evaluated at $t=0$.
- **Boundary conditions:** time-dependent Dirichlet data obtained by restricting the analytical solution to $\partial\Omega$.

## Numerical configuration in the manuscript

- Final time: $T=2$.
- Time integration: BDF1 with $\Delta t=5\times10^{-3}$ (**400 time steps**).
- Initial mesh: structured crossed triangular mesh with $N=64$ subdivisions per direction; **8,321 vertices** and **16,384 triangles**.
- Spatial interpolation: continuous piecewise-linear elements for both velocity components.
- Finite element formulations considered: GFEM, SUPG, and SUPG-YZ$\beta$; shock-capturing reference scales $Y_u=Y_v=0.1$.
- Adaptation monitor: recovered curvature of both solution components and a residual-based YZ$\beta$ sensor, evaluated using the final-time SUPG solution (including the last two time levels for the BDF1 residual).
- Monitor parameters: $\theta=0.25$, $\alpha=2$, $\widetilde{p}=0.30$.
- UM2N adaptation: one mesh movement after the original transient run, followed by a full recomputation from $t=0$ to $t=T$ on the moved mesh.

## Solver implementation

**Work in progress.** The solver code, setup instructions, and reproducibility workflow for this benchmark are being prepared and will be added later. No implementation files or numerical figures are included in this folder yet.
