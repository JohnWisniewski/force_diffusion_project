# Generating Protein Conformation through Force‑Guided Diffusion Models

**Jakeb Milburn · John Wisniewski · Jiahao Xie**  
Department of Computer and Information Sciences, University of Delaware  

---

## Team members
- **Jakeb Milburn :** Writing, Validation  
- **John Wisniewski :** Software Development, Visualization  
- **Jiahao Xie :** Conceptualization, Methodology  

---

## Problem Statement
Proteins are not rigid structures—they adopt a variety of conformations that are crucial for biological functions like molecular recognition, signal transduction, and enzymatic activity. This conformational landscape is governed by the protein’s energy surface, often described by the Boltzmann distribution.

While Molecular Dynamics (MD) simulations offer accurate conformational sampling, they are computationally expensive and suffer from limitations in sampling rare events, especially across biologically relevant timescales. Recent deep learning methods like AlphaFold \cite{jumper2021highly} can predict static folded structures, but fall short in capturing alternative metastable states or transition paths.

Diffusion models \cite{songscore} have emerged as powerful generative tools across modalities. In proteins, models like Str2Str \cite{lustr2str}, DiG \cite{zheng2024predicting}, and EIGENFOLD \cite{jing2023eigenfold} adapt diffusion to sample protein conformations. However, most lack physical guidance, leading to conformations that are diverse but may reside in high‑energy, non‑physical regions of the energy landscape.

---

## Proposed Solution
We propose to design and implement a **Force‑Guided Diffusion Model** for generating protein conformations, inspired by the CONFDIFF framework \cite{wangprotein} but tailored for a simplified and computationally manageable variant.  
Our pipeline combines **SE(3)‑equivariant diffusion modeling** with a novel **intermediate force guidance mechanism** to encourage sampling of physically plausible protein conformations that better reflect the Boltzmann distribution.

### Key components
- **Protein Representation:** backbone coordinate frames, enabling rotational and translational invariance.  
- **Diffusion Model:** an SE(3) diffusion process that perturbs protein structures and learns to reverse the process, generating realistic conformations from noise.  
- **Force Guidance (Main Contribution):** an additional guidance term based on physical forces—either simple analytical potentials or a lightweight neural network—that steers the model toward low‑energy, stable conformations.  
- **Guided Sampling Strategy:** integrates the learned or approximated force signal into the reverse‑time process, prioritizing physically favorable states without sacrificing diversity.  

**Contributions.** Design and implement a force‑guided diffusion framework for protein conformations. Explore physically motivated forces to enhance structural realism in generative models. Systematically evaluate how force guidance affects generation quality, diversity, and energy profiles.

---

## Expected Output / Deliverables
- Functional prototype of a force‑guided diffusion model  
- Comparison with unguided and energy‑guided models  
- Evaluation metrics: RMSD, RMSF, JS divergence, Energy  
- Visualizations: trajectory samples, 2‑D projections, energy histograms  
- Final report and presentation with findings  

---

## Challenges / Open Questions
- Computing physical forces using engines like OpenMM \cite{eastman2017openmm} can be slow, while simpler approximations may lack realism. A trade‑off is needed between computational cost and physical accuracy.  
- Adding force into the reverse diffusion process risks destabilizing sampling. Proper tuning of the guidance strength ( $\eta$ ) and blending with the score model is essential to maintain both fidelity and diversity.  
- Reference ensembles from MD simulations exist for only a few proteins, making it difficult to assess distributional accuracy. Alternative evaluation strategies must be considered.  
- Strong force guidance improves energy stability but may reduce sample diversity. The model must balance conformational richness with adherence to physical constraints.  

---

## Timeline (6 Weeks)

| Week | Milestone                                                             |
|------|----------------------------------------------------------------------|
| 1 | Literature review, setup baseline SE(3) diffusion framework             |
| 2 | Implement force approximation module (simple gradients or analytic)     |
| 3 | Integrate guidance into reverse diffusion process                       |
| 4 | Evaluate on small proteins (e.g., WW‑domain)                            |
| 5 | Analyze metrics, visualize conformations, tune hyperparameters          |
| 6 | Finalize report, figures, and presentation                              |
