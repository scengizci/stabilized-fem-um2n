# Third-party software and attribution

This repository accompanies the research project **Curvature- and stabilization-informed neural mesh adaptation for stabilized finite element computations of convection-dominated transport** by Süleyman Cengizci and Bilen Emek Abali.

Our research integrates stabilized finite element computations with an existing pretrained neural mesh-movement method. **We do not claim authorship of the Universal Mesh Movement Network (UM2N), its original architecture, or its pretrained weights.**

## Universal Mesh Movement Network (UM2N)

- **Upstream project:** [mesh-adaptation/UM2N](https://github.com/mesh-adaptation/UM2N)
- **Original research:** *Towards Universal Mesh Movement Networks*, NeurIPS 2024, by Mingrui Zhang and collaborators.
- **Upstream license:** MIT (as stated by the official GitHub repository).
- **Role here:** A pretrained, zero-shot mesh-movement component used with monitors obtained from stabilized finite element solutions.

If original UM2N source files or model weights are added to this repository, preserve all applicable upstream copyright, license, and attribution information. Check the licensing or distribution terms for any model weight files before redistribution. Cite the original UM2N publication in research outputs that use it.

## Computational dependencies

The numerical workflow described in the accompanying manuscript uses **Firedrake**, **PETSc**, **PyTorch**, **PyTorch Geometric**, and **Gmsh**, with additional libraries as documented in the paper. These tools are independently developed, have their own maintainers and licensing terms, and are not automatically covered by this repository's MIT license.

See each dependency's official repository or project website for the applicable license and citation instructions. Add any third-party source code, data, model, or asset redistributed in this repository to this notice with its precise provenance and license.

## Scope of the repository license

The top-level `LICENSE` covers original source code and documentation authored for this project to the extent the named copyright holders are authorized to license those materials. It does not relicense independently copyrighted third-party code, models, data, or images.

The repository may initially contain documentation without executable benchmark code. Update this file and the project README when the actual source files and pretrained-model dependencies have been added and verified.
