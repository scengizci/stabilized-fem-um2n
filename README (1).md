# Curvature- and Stabilization-Informed Neural Mesh Adaptation

**A zero-shot neural r-adaptation framework for stabilized finite element computations of convection-dominated transport and incompressible flows.**

**Authors:** Süleyman Cengizci¹ and Bilen Emek Abali²  
¹ Department of Computer Technologies, Antalya Bilim University, Antalya, Türkiye  
² Division of Applied Mechanics, Uppsala University, Uppsala, Sweden

**Manuscript:** *Curvature- and stabilization-informed neural mesh adaptation for stabilized finite element computations of convection-dominated transport*  
**Repository status:** Research materials are being organized. Reproducible scripts, configuration files, and figures will be added after verification.

## Overview

This research combines stabilized finite element methods (FEM) with a **pretrained Universal Mesh Movement Network (UM2N)** to redistribute mesh vertices without changing mesh connectivity or the number of degrees of freedom. Instead of training a neural network to solve the governing partial differential equations, the method uses the numerical FEM solution to construct a mesh-adaptation monitor and then applies the same pretrained UM2N model in a **zero-shot** setting.

The main methodological contribution is a **hybrid curvature- and stabilization-informed monitor**:

- A **Hessian-informed indicator** derived from recovered solution curvature.
- A **stabilization-informed indicator** based on a residual-derived YZβ shock-capturing sensor for transport problems or local LSIC activity for incompressible flows.
- A normalized combination of these indicators used to guide neural mesh movement.

The physical problem is solved by FEM both before and after mesh movement; UM2N does **not** replace the PDE solver.

## Method at a glance

1. Solve the governing PDE on the original mesh using the appropriate stabilized FEM formulation.
2. Recover curvature and/or stabilization-related indicators from the computed solution.
3. Normalize the indicators and construct the hybrid monitor.
4. Pass the monitor, mesh coordinates, connectivity, and boundary information to the **fixed pretrained UM2N** model.
5. Restore prescribed boundary vertices, check mesh validity, and accept a valid moved mesh.
6. Re-solve the PDE on the moved mesh using the same FEM discretization and compare accuracy and mesh quality.

The hybrid indicator and monitor are defined as

$$
I_\theta(\mathbf{x}) = \theta \widehat I_H(\mathbf{x})
+ (1-\theta)\widehat I_S(\mathbf{x}), \qquad 0\leq\theta\leq1,
$$

$$
m_\theta(\mathbf{x}) = 1+\alpha\bigl[I_\theta(\mathbf{x})\bigr]^{\widetilde p},
\qquad \alpha>0,\quad \widetilde p>0.
$$

Here, $\widehat I_H$ and $\widehat I_S$ are percentile-normalized curvature and stabilization indicators, respectively. The mesh movement is **r-adaptive**: the mesh topology and discrete problem size are preserved.

## Numerical benchmarks

The manuscript investigates four two-dimensional benchmark problems.

| Test | Governing problem | Reported observation |
| --- | --- | --- |
| **1** | Stationary convection–diffusion | **62.1%** reduction in global SUPG RMSE after UM2N redistribution, at the same number of degrees of freedom. |
| **2** | Transient coupled viscous Burgers equations | **57.8%** reduction in final-time global SUPG RMSE after UM2N redistribution. |
| **3** | Stationary incompressible Kovasznay flow | Approximately **5.7%** reduction in pressure RMSE; some velocity errors increase slightly. |
| **4** | Unsteady incompressible flow around a circular cylinder | With a time-aggregated monitor, the relative error in peak lift decreases from **1.32% to 0.51%** using the volume functional, and from **6.49% to 3.35%** using surface traction. Other quantities show mixed changes. |

**Interpretation:** These are benchmark-specific accuracy results, not guarantees of improvement for all physical quantities or geometries. Preserving degrees of freedom does not, on its own, establish a reduction in total computational time.

### Transient adaptation strategies

For the cylinder benchmark, the manuscript also compares a **single time-aggregated mesh redistribution** with an **online strategy that updates the mesh every 100 time steps**. More frequent adaptation is not uniformly beneficial, highlighting the roles of adaptation frequency and solution transfer.

## Software and dependencies

The computational workflow uses:

- **Firedrake** for finite element discretization and solution.
- **PETSc** for linear and nonlinear algebraic solves.
- **PyTorch / PyTorch Geometric** for inference with the pretrained UM2N model.
- **Gmsh** for benchmark geometries and mesh generation where required.
- **Python** for indicators, mesh processing, post-processing, and analysis.

Exact environment specifications and reproducible execution instructions will accompany the code release. The published UM2N architecture and its training procedure are not modified in this work.

## Reproducibility and availability

This repository is being prepared to host the numerical experiments, monitor construction, mesh-quality checks, plotting scripts, and documentation associated with the manuscript. **At present, the repository is not yet a complete executable reproduction package.** Do not assume that missing scripts, checkpoints, or configurations are available.

The pretrained UM2N implementation and checkpoints originate from the original UM2N project. Their use and redistribution are subject to the upstream project's applicable license and attribution requirements.

## Related work and acknowledgment

This study builds on the **Universal Mesh Movement Network (UM2N)** introduced by Zhang et al. and the earlier **Mesh Movement Network (M2N)** work by Song et al. The neural architecture and pretrained weights are credited to their original developers; the hybrid stabilization-informed monitor and its FEM coupling are investigated in the present manuscript.

- Zhang et al., *Towards Universal Mesh Movement Networks* (2024): https://arxiv.org/abs/2407.00382
- Song et al., *Mesh Movement Networks for PDE Solvers* (2022): https://arxiv.org/abs/2204.11188

The first author acknowledges partial financial support from **TÜBİTAK**, Grant No. **225M468**, as stated in the manuscript.

## Citation

The manuscript's definitive bibliographic details and a `CITATION.cff` file will be provided when available. In the meantime, please cite the underlying UM2N work when using its model or implementation.

## License

**A license has not yet been selected for this repository.** Public visibility does not itself grant permission to reuse or redistribute its contents. A license will be added before a general code release, subject to the rights and licenses of third-party software and model weights.
