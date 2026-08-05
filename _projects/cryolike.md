---
layout: page
title: CryoLike
description: A GPU-Accelerated Python Package for Cryo-EM Image-to-Structure Likelihood Calculations
img: assets/img/cryolike.png
importance: 1
category: work
related_publications: true
---

### Overview

Characterizing conformational heterogeneity in single-particle cryo-electron microscopy (cryo-EM) is a significant challenge in structural biology, especially for highly flexible biomolecules. Standard 3D reconstruction and classification approaches often rely on consensus maps and extensively filter or discard particle images, losing critical information about rarely occupied conformations or transition states. 

**CryoLike** is a computationally efficient, GPU-accelerated Python package developed for evaluating image-to-structure (and image-to-volume) likelihoods across large-scale cryo-EM datasets. Based on Fourier-Bessel representations of images, CryoLike enables high-throughput likelihood computations, serving as a key driver for downstream Bayesian inference, ensemble reweighting, and structural discrimination tasks.

---

### The Problem

Bayesian methods offer physically interpretable frameworks to recover the conformational probability distributions and free-energy landscapes of biomolecules from cryo-EM images. However, calculating image-to-structure likelihoods is extremely computationally demanding because the pose parameters of each individual particle—specifically the 3D viewing direction, 2D translation offset, and in-plane rotation—are unknown and must be marginalized or resolved over a massive search space. When scaling to thousands of candidate structures from molecular dynamics (MD) simulations and millions of experimental single-particle images, conventional algorithms become prohibitively expensive.

---

### Methodology and Workflow

CryoLike optimizes the likelihood calculation pipeline through a combination of fast Fourier transformations and polar coordinate algebra.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/cryolike_workflow.png" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
*Figure 1: Schematic workflow of the CryoLike package. (a) Image processing pipeline: Ingesting STAR/CryoSparc metadata, MRC particle stacks, and atomic coordinates (PDB) or density volumes (MRC). Conversion to Fourier space via NUFFT, applying the CTF, evaluating cross-correlations over pose parameters $\tau$, and outputting optimal poses and likelihoods. (b) Mathematical transformation: Converting physical coordinates to Fourier space, projecting onto polar grids, transforming to a Fourier-Bessel basis via 1D FFT along the angular axis, and computing cross-correlations.*

#### 1. Input Specifications
CryoLike ingests:
*   **Particle Stacks:** 2D experimental images in MRC format.
*   **CTF Parameters:** Microscope optics metadata in STAR or CryoSparc formats.
*   **3D Models:** Atomic coordinates in PDB format or 3D density maps/volumes in MRC format.

#### 2. Template Generation & Fourier Projection
According to the Fourier-slice theorem, the 2D projection of a 3D structure corresponds to a slice through the origin of 3D Fourier space.
*   **For PDB Structures:** CryoLike represents atomic densities using either a 3D Gaussian or a hard-sphere model (with Van der Waals radii on $C_\alpha$ atoms).
*   **For 3D Volumes:** Slices are extracted using a 3D Non-Uniform Fast Fourier Transform (NUFFT) via `cuFINUFFT`/`finufft`. Slices are resolved on a polar grid $\{k_{\text{polar}}\} := (k, \psi)$ where radial frequencies are determined by Gauss-Jacobi quadrature.
*   **CTF Application:** Slices are corrected with the image-specific contrast transfer function (CTF) to generate target templates $\hat{S}_\tau(k_{\text{polar}})$.

#### 3. Rotational Alignment in Fourier-Bessel Space
To avoid the $O(N^2)$ expense of spatial image alignment, CryoLike transforms the polar Fourier representations of the experimental images and templates into a **Fourier-Bessel basis** by applying a 1D FFT along the angular coordinate $\psi$. In this basis, in-plane rotations correspond to simple phase shifts. By multiplying the Fourier-Bessel coefficients and integrating over radial frequencies, the cross-correlation profile across all rotational angles and translation offsets is evaluated rapidly:
$$X_{\text{freq}}(\tau; \hat{A}, \text{CTF}, \hat{F}) = \mathcal{F}^{-1} \left[ \int_{0}^{k_{\text{max}}} \check{S}^\dagger(k, \cdot) \odot \check{A}(k, \cdot) k dk \right]$$
The optimal pose parameters $\tau^{\text{opt}} = \{\gamma, \beta, \alpha, \delta\}$ are resolved by maximizing this cross-correlation.

#### 4. Likelihood Calculation and Parameter Marginalization
Assuming a Gaussian white-noise model with variance $\lambda^2$, CryoLike analytically marginalizes the likelihood over image-specific intensity factors $\nu$, offset variables $\mu$, and pixel variance $\lambda^2$. Users can compute the final marginalized likelihood using three approaches:
1.  **Optimal Physical:** Evaluates the likelihood in physical space for only the optimal pose $\tau^{\text{opt}}$.
2.  **Optimal Fourier:** Evaluates the likelihood in Fourier space for only the optimal pose $\tau^{\text{opt}}$.
3.  **Integrated Fourier:** Integrates/marginalizes the likelihood in Fourier space over all possible pose parameters $\tau$ assuming a flat prior.

---

### Computational Performance

By leveraging custom PyTorch cores and GPU acceleration, CryoLike processes millions of image-template pairs efficiently. 

*   **Benchmarking (NVIDIA H100 GPU):**
    *   Evaluating $1,024$ images of box size $256 \times 256$ pixels against a 3D volume using $1,024$ translation samples completes in **under 45 seconds**.
    *   For box size $128 \times 128$ pixels with $256$ translation samples, processing finishes in **under 3 seconds**.
*   The processing time scales with the number of frequency shells (resolution), displacement search space, and GPU memory batch size.

---

### Efficacy and Model Discrimination

CryoLike’s performance was validated through Log-Likelihood Ratio (LLR) tests on experimental datasets, calculating the probability of a "true" model versus a deformed "false" model:

1.  **Apoferritin (EMPIAR-10026):** Evaluated against PDB structures (`4v1w` as true; deformed normal mode structure as false; RMSD $7.6\text{ Å}$). CryoLike achieved a low False Negative Rate (FNR) and outpaced the benchmark framework BioEM.
2.  **Hemagglutinin (EMPIAR-10532):** Evaluated using PDB structures (`6wxb` as true; deformed structure as false; RMSD $14.4\text{ Å}$). CryoLike reliably discriminated the conformations with high accuracy.
3.  **SARS-CoV-2 Spike Protein (EMPIAR-12098):** Directly evaluated using 3D density maps of two conformations: EMD-50421 (three RBD up, "3U") and EMD-50422 (two RBD up, one down, "2U"). CryoLike successfully identified the true conformation for both particle sets. Importantly, the ability to perform direct volume-to-image likelihood evaluations is a unique capability not present in coordinate-only tools like BioEM.

Furthermore, CryoLike's outputs were successfully integrated into ensemble reweighting frameworks, demonstrating its utility in mapping complex conformational probability distributions for highly flexible biomolecular assemblies.

---

### Code and Availability

*   **Academic Preprint:** "CryoLike: A Python package for Cryo-Electron Microscopy image-to-structure likelihood calculations" — deposited on *bioRxiv* (2024). [DOI: 10.1101/2024.10.18.619077](https://doi.org/10.1101/2024.10.18.619077)
*   **GitHub Repository:** [flatironinstitute/CryoLike](https://github.com/flatironinstitute/CryoLike)
*   **Technical Stack:** Python, PyTorch, cuFINUFFT / finufft.
