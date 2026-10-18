# Test 1 — Two-dimensional stationary convection–diffusion

## Problem definition

Find the scalar field $u$ such that

$$
-\varepsilon\Delta u+\mathbf{b}\cdot\nabla u=0
\qquad \text{in }\Omega=(0,1)^2,
$$

where

$$
\varepsilon=10^{-4},\qquad
\mathbf{b}=\begin{bmatrix}\cos(-\pi/3)\\\sin(-\pi/3)\end{bmatrix}
=\begin{bmatrix}\tfrac12\\-\tfrac{\sqrt3}{2}\end{bmatrix}.
$$

## Boundary conditions

Dirichlet conditions are prescribed on the entire boundary:

$$
u=g_D\qquad\text{on }\partial\Omega,
$$

with

$$
g_D(x_1,x_2)=
\begin{cases}
0, & x_1=1\ \text{or}\ x_2\leq0.7,\\
1, & \text{otherwise}.
\end{cases}
$$

The discontinuous boundary data generate a characteristic interior layer beginning at $(0,0.7)$, as well as outflow boundary layers.

## Numerical configuration in the manuscript

- Initial mesh: structured triangular mesh, with $N=128$ subdivisions in each coordinate direction; **33,025 vertices** and **65,536 triangles**.
- Numerical reference solution: SUPG-YZ$\beta$ with $N_{\mathrm{ref}}=500$.
- Finite element formulations considered: GFEM, SUPG, and SUPG-YZ$\beta$.
- Adaptation monitor: hybrid recovered-Hessian and residual-based YZ$\beta$ sensor, constructed from the original-mesh SUPG solution.
- Monitor parameters: $\theta=0.25$, $\alpha=2$, $\widetilde{p}=0.30$.
- UM2N adaptation: a single mesh movement; the same moved mesh is used for the subsequent finite element comparisons.

## Solver implementation

**Work in progress.** The solver code, setup instructions, and reproducibility workflow for this benchmark are being prepared and will be added later. No implementation files or numerical figures are included in this folder yet.
