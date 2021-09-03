---
title: Background
weight: 20
---

Molecular Docking (MD) is an important step of the drug discovery process which aims at calculating 
the preferred position and shape of one molecule to a second when they are bound to each other. This step focuses on computationally simulating the molecular recognition process. It aims to achieve an optimized conformation for both the protein and ligand and relative orientation between protein and ligand such that the free energy of the overall system is minimized. 

![Molecular Docking](/images/molecule-docking.png)

In this work, The protein or the pocket is considered as a rigid structure. The ligand is considered as a 
flexible set of atoms. There are usually three main phases in MD:

* Ligand expansion
    * Identification of the rotatable bonds
    * Internal distances maximization
    * Remove tool related bias (e.g. smile-to-3D)
* Initial Placement
    * Ligand main fragments decomposition
    * Ligand initial poses identification
    * Placement of the ligand into the pocket with rigid roto-translations
* Shape Refinement
    * Use of the rotatable bonds to modify the ligand shape and to match the protein pocket
    * Docking score maximization

In this work, actually the first phase, ligand expansion or the molecule unfolding (MU), is focused and 
implemented using quantum annealer. This phase is important for improving docking. In fact, an initial
pose of the ligand that is set a priori may introduce shape bias affecting the final quality of the
docking. MU is the technology used for removing such initial bias.