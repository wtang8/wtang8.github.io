---
layout: page
title: Ensemble Reweighting
description: A Bayesian Inference Framework for Recovering Biomolecular Populations from Cryo-EM Images
img: assets/img/ensemble_reweighting.jpg
importance: 3
category: work
related_publications: true
---

### Overview

Biomolecules are dynamic entities that exist in a Boltzmann-weighted ensemble of conformations. While cryo-electron microscopy (cryo-EM) has revolutionized structural biology by capturing high-resolution snapshots of macromolecules, traditional reconstruction methods are heavily biased toward low conformational heterogeneity. In a typical cryo-EM workflow, only a small fraction of the collected particle images (often <25%) representing the most stable state is utilized to generate a consensus 3D density map, while the remaining images—which contain vital information about transition states or rare conformations—are discarded.

This project implements a general **Bayesian Ensemble Reweighting** framework. Instead of discarding heterogeneous single-particle images or relying on pre-defined low-dimensional paths, the framework estimates the equilibrium probability density of the biomolecule directly in its high-dimensional conformational space. By combining prior structural ensembles (generated from molecular dynamics simulations or structure prediction tools) with individual cryo-EM particle images, it reconstructs the system's true thermodynamic population and free-energy landscape.

---

### The Problem

Standard ensemble refinement techniques typically use experimental observables that represent an ensemble average (such as NMR chemical shifts or SAXS intensities). Cryo-EM, conversely, yields independent and identically distributed (i.i.d.) single-molecule measurements. 

Traditional map-fitting or 3D classification methods fail to recover the full probability distribution because they average out spatial variations. Although single-particle reweighting algorithms have been proposed (e.g., cryoBIFE), they require a predetermined 1D conformational path, which limits their applicability to complex, multi-state transitions. The goal of this framework is to compute the posterior distribution of ensemble weights directly in the high-dimensional coordinate space ($\mathbb{R}^{3N_{\text{atom}}}$) using individual, noisy 2D projections.

---

### Methodology and Workflow

The framework corrects an initial guess of the Boltzmann distribution by applying a parameterized, multiplicative correction factor inferred from single-particle observations.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/ensemble_reweighting.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
*Figure 1: Conceptual overview of the Ensemble Reweighting framework. An initial, approximate conformational probability density (left) from simulations is refined using a Bayesian framework (middle) that compares candidate structures against individual cryo-EM particle images. The correction factor $\eta(x; \alpha)$ scales the weights $\alpha$ to produce an optimized probability density in the molecular coordinate space (right).*

#### 1. Bayesian Formulation for i.i.d. Measurements
We define a family of candidate probability densities $p(x \mid \alpha) = \eta(x; \alpha) p_0(x)$, where $p_0(x)$ is the prior Boltzmann density (e.g., from MD) and $\eta(x; \alpha)$ is the nonnegative correction factor parameterized by $\alpha$. 
Using Bayes' theorem for i.i.d. measurements $Y = \{y_i\}$, the posterior distribution of the weights $\alpha$ is:
$$p(\alpha \mid Y) \propto p(\alpha) \prod_{i} \left( \int p(y_i \mid x) \eta(x; \alpha) p_0(x) dx \right)$$
where $p(y_i \mid x)$ is the likelihood of observing the $i$-th noisy projection image given the 3D configuration $x$.

#### 2. Simple Ensemble Reweighting
For a small, discrete set of conformations $\{x_t\}_{t=1}^T$, we assume a uniform prior distribution:
$$p(x \mid \alpha) = \sum_{t=1}^T \delta(x - x_t) \alpha_t$$
where the weights are constrained such that $\alpha_t \ge 0$ and $\sum_t \alpha_t = 1$. The posterior simplifies to:
$$p(\alpha \mid Y) \propto p(\alpha) \prod_{i} \left( \sum_{t=1}^T p(y_i \mid x_t) \alpha_t \right)$$

#### 3. Piecewise Clustering on Conformational Samples
For large ensembles (e.g., $>10^5$ structures from MD), evaluating the likelihood for every image-structure pair is computationally prohibitive. To scale the algorithm, we partition the configuration space into $M$ disjoint, spatially compact clusters using $k$-medoids clustering based on $C_\alpha$ RMSD distance. 
The correction factor is represented piecewise across clusters:
$$\eta(x; \alpha) = \sum_{m=1}^M \alpha_m \mathbb{1}_m(x)$$
Approximating the likelihood of each cluster by its medoid $\chi_m$ simplifies the posterior to:
$$p(\alpha \mid Y) \propto p(\alpha) \prod_{i} \left( \frac{1}{T} \sum_{m=1}^M p(y_i \mid \chi_m) \alpha_m N_m \right)$$
where $N_m$ is the number of conformations belonging to cluster $m$.

#### 4. Posterior Sampling
Posterior inference of the weights is performed using Markov chain Monte Carlo (MCMC) sampling. Specifically, we employ Hamiltonian Monte Carlo (HMC) with the No-U-Turn Sampler (NUTS) implemented via Stan to draw samples of $\alpha$ and estimate credible intervals.

#### 5. Post-Processing Free-Energy Reconstruction
Once the optimal weights $\alpha$ are obtained, the refined ensemble density can be projected onto any chosen set of collective variables $s$ to reconstruct a 2D or 1D free-energy surface:
$$e^{-\beta G(s)} = \frac{1}{Z_0} \int \delta(S(x) - s) p(x \mid \alpha) dx$$

---

### Key Validation Results

The methodology was validated across a hierarchy of test cases:

#### 1. Normal Mixture Toy Model
*   **Design:** Evaluated on a 3D normally distributed mixture representing three metastable states (target populations: 0.5, 0.3, 0.2) contaminated with Gaussian noise.
*   **Result:** The algorithm robustly recovered the true populations. When non-representative conformations (points in low-density regions) were included, the model assigned them near-zero weights, demonstrating that a "perfect" prior ensemble is not required.

#### 2. Decapeptide Chignolin Benchmark
*   **Simulation Setup:** Prior configurations were sampled from a $12\text{ }\mu\text{s}$ MD trajectory (120,000 frames) using the Amber ff99SB-ILDN force field. Synthetic cryo-EM images (106,949 projections) were generated using a different force field (CHARMM22*) to serve as the ground truth.
*   **Conformational States:** Chignolin folds into three distinct states: folded (anti-parallel $\beta$-hairpin), misfolded (anti-parallel $\beta$-hairpin shifted by one residue), and a highly heterogeneous unfolded state.
*   **Performance:** CryoLike image-structure likelihoods were integrated into the reweighting pipeline. The framework successfully recovered the populations of all three states (folded $\approx 77\%$, misfolded $\approx 0.4\%$, unfolded $\approx 23\%$) under extreme noise levels down to an SNR of $10^{-3}$.
*   **Free-Energy Refinement:** The initial prior ensemble overpopulated the misfolded state. Applying the reweighting framework successfully down-weighted the misfolded state in the 2D free-energy landscape (plotted against folded and misfolded $C_\alpha$ RMSD), matching the ground-truth landscape.

---

### Code Availability

*   **Academic Paper:** "Ensemble reweighting using Cryo-EM particles" — Published in *The Journal of Physical Chemistry B* (2023). [DOI: 10.1021/acs.jpcb.3c01072](https://doi.org/10.1021/acs.jpcb.3c01072)
*   **Ensemble Reweighting Code:** [flatironinstitute/Ensemble-reweighting-using-Cryo-EM-particles](https://github.com/flatironinstitute/Ensemble-reweighting-using-Cryo-EM-particles)
*   **Technical Stack:** Python, Stan, PyTorch, GROMACS.
