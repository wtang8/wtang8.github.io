---
layout: page
title: SINATRA Pro
description: A Topological Data Analytic Pipeline for Biophysical Signature Discovery in Protein Dynamics
img: assets/img/sinatra_pro.jpg
importance: 2
category: work
related_publications: true
---

### Overview

Comparing ensembles of protein structures obtained from molecular dynamics (MD) simulations is a key challenge in computational biology. Biologically relevant structural changes are frequently overshadowed by thermal fluctuations and spurious statistical noise. Traditional metrics—such as root-mean-square fluctuation (RMSF) or principal component analysis (PCA)—either suffer from reduced power in noisy trajectories or require explicit atom-by-atom correspondences (diffeomorphisms) between structures. 

**SINATRA Pro** is a robust computational pipeline designed to identify topological and geometric differences between two protein structural ensembles (e.g., wild-type versus mutant, or active versus inactive states) without requiring predefined coordinate grids or sequence correspondences. By utilizing tools from integral geometry and differential topology, SINATRA Pro extracts spatial locations and biophysical signatures that define the variance between phenotypic classes.

---

### The Problem

Analyzing MD trajectories to locate critical structural variations is often hindered by two primary issues:
1. **Thermal Noise:** Thermal fluctuations naturally arising in simulations can easily mask minor, yet functionally critical, conformational shifts.
2. **Correspondence Constraints:** Conventional structural mapping methods rely on a strict one-to-one mapping between atomic coordinates. When mutations, insertions, deletions, or phylogenetic changes occur, sequence heterogeneity makes establishing these differentiable mappings (diffeomorphisms) impossible. 

SINATRA Pro addresses these constraints by leveraging topological summaries that capture shape information globally and locally, preserving the geometric properties of the protein without depending on rigid atom-by-atom alignments.

---

### Methodology and Pipeline

The SINATRA Pro framework processes all-atom MD simulation trajectories through a unified five-step pipeline:

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/sinatra_pro.jpg" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
*Figure 1: Schematic overview of the SINATRA Pro pipeline. (A) Input parameters and coordinate extraction. (B) Simplicial construction of 3D meshes. (C) Extraction of Differential Euler Characteristic (DEC) curves. (D) Gaussian Process Classification (GPC) and relative centrality computation. (E) Projection of evidence potentials onto the 3D protein structure.*

#### 1. Simplicial Construction (3D Mesh Representation)
The pipeline begins by taking the 3D Cartesian coordinates of the atoms in each aligned protein frame as vertices. An edge is drawn between any two atoms if their Euclidean distance is smaller than a specified cutoff radius $r$ (typically $r \approx 6.0\text{ Å}$ for flexible proteins, or $r \approx 1.0\text{–}2.0\text{ Å}$ for rigid systems). The triangles (faces) enclosed by these connected edges are filled to construct a triangulated 3D mesh, representing the protein structure as a simplicial complex.

#### 2. Topological Summary Statistics (DEC Transform)
The 3D mesh is converted into topological summaries using the **Differential Euler Characteristic (DEC)** transform. While the classical Euler Characteristic ($\chi = V - E + F$) computes global properties, the DEC tracks local topological changes (the appearance and disappearance of vertices, edges, and faces) across $l$ filtration steps (sublevel sets) along $m = c \times d$ directions (where $c$ is the number of cones and $d$ is the number of directions per cone, parameterized by a cap radius $\theta$):
$$\Delta \chi = \Delta V - \Delta E + \Delta F$$
The DEC curves along all directions are concatenated to form a topological feature vector of length $J = l \times m$.

#### 3. Probabilistic Classification (Gaussian Process Probit Regression)
A weight-space Gaussian Process Classification (GPC) model with a probit link function and a Radial Basis Function (RBF) kernel is used to classify the protein structures based on the topological summaries. The model is represented as:
$$y \sim \text{Bernoulli}(\pi); \quad \Phi^{-1}(\pi) = f; \quad f \sim \mathcal{N}(0, K)$$
where $y$ indicates the phenotypic label (e.g., wild-type $y=0$ or mutant $y=1$), and $K$ is the covariance matrix. Posterior inference is conducted via an Elliptical Slice Sampling MCMC algorithm.

#### 4. Feature Selection of Topological Statistics
Nonparametric effect sizes $\beta$ are estimated by projecting the latent variables $f$ back onto the topological features:
$$\beta = (X^\top X)^+ X^\top f$$
A relative centrality metric is assigned to each feature using the Kullback-Leibler Divergence (KLD):
$$\text{KLD}(\beta_j) = \text{KL}(p(\beta_{-j}) \parallel p(\beta_{-j} \mid \beta_j = 0))$$
These are normalized to yield an association metric $\gamma_j \in [0, 1]$ representing the statistical significance of each topological feature.

#### 5. 3D Evidence Mapping and Reconstruction
Finally, the association metrics are mapped back onto the original 3D protein structure. This produces residue- or atomic-level "evidence scores" scaled from 0 to 100 (where 100 indicates the first reconstructed feature), facilitating the 3D visualization of biophysical signatures.

---

### Key Findings in Real Protein Systems

The utility of SINATRA Pro was validated across five independent protein systems with varying levels of dynamic complexity:

| Protein System | PDB ID | Event/Mutation | Structural Signature Detected |
| :--- | :--- | :--- | :--- |
| **$\beta$-lactamase (TEM)** | `1BTL` | Arg164Ser | Identified increased dynamics of the regulatory O-loop (residues 163–178) caused by the disruption of the Arg164–Asp179 salt bridge, and revealed a correlated shift in the active site upper boundary (residues 210–230), hinting at allosteric coupling. |
| **HIV-1 Protease** | `3NU3` | Ile50Val | Captured asymmetric conformational changes in the flaps (residues 47–55) and the fulcrum region in the presence of the inhibitor Amprenavir. |
| **EF-Tu** | `1TTT` | GTP Hydrolysis | Successfully localized the increased flexibility of Domain 2 (residues 208–308) following GTP hydrolysis, overcoming significant dynamic noise. |
| **Abl1 Tyrosine Kinase** | `3KFA` | Met290Ala | Resolved key structural variations in the DFG motif (residues 381–383) and the $\alpha$C helix (residues 281–293) despite high-noise fluctuations in the unanchored termini. |
| **Importin-$\beta$** | `2P8Q` | IBB Peptide Release | Accurately mapped the global, backbone-wide uncoiling of the superhelix across HEAT repeats upon the release of the IBB peptide. |

Across both controlled simulations and real-world datasets, SINATRA Pro consistently outperformed traditional baselines (RMSF, PCA, Elastic Net, and Neural Networks) in identifying both static (constant displacement) and dynamic (stochastic spherical perturbation) structural changes.

---

### Code and Data Availability

*   **Academic Paper:** "A topological data analytic approach for discovering biophysical signatures in protein dynamics" — Published in *PLoS Computational Biology* (2022). [DOI: 10.1371/journal.pcbi.1010045](https://doi.org/10.1371/journal.pcbi.1010045)
*   **SINATRA Pro Software:** [lcrawlab/SINATRA-Pro](https://github.com/lcrawlab/SINATRA-Pro) (Python 3.6.9)
*   **Paper Results Repository:** [lcrawlab/SINATRA_Pro_Paper_Results](https://github.com/lcrawlab/SINATRA_Pro_Paper_Results)
*   **MD Simulation Data:** Available on [Harvard Dataverse](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/FX0TG5)
