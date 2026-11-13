# Structure-Based Discovery of Natural Product Candidates Targeting FabI in *Acinetobacter baumannii*

**Computational Drug Discovery | Cheminformatics | Molecular Docking | Molecular Dynamics**

## Project Overview

Antimicrobial resistance has increased the need to identify new antibacterial compounds with alternative mechanisms of action. Fatty acid biosynthesis provides potential opportunities for antibacterial drug discovery, including the enzyme enoyl-ACP reductase (FabI).

This project presents a structure-based virtual screening pipeline to identify natural product candidates targeting FabI from *Acinetobacter baumannii*. Approximately 94,400 compounds from the NPASS database were processed through cheminformatics-based filtering, molecular docking, chemical-space analysis, ligand efficiency assessment, protein–ligand interaction analysis and molecular dynamics simulations.

Four compounds were selected for molecular dynamics simulations. Among these, NPC87794 and NPC253314 maintained relatively stable binding poses during 100 ns simulations and were prioritized for further investigation.

**Research status:** Manuscript under preparation. All findings are computational and require experimental validation.

## Research Objectives

- Identify potential natural product candidates targeting *A. baumannii* FabI.
- Develop a cheminformatics-based compound filtering and virtual screening pipeline.
- Explore the chemical space of screened compounds using molecular fingerprints and clustering.
- Prioritize candidates through docking scores, ligand efficiency and interaction analysis.
- Investigate the stability of selected protein–ligand complexes through molecular dynamics simulations.

## Computational Workflow

NPASS library → RDKit filtering → 3D structure generation → ADMET assessment → AutoDock Vina docking → PCA and K-means clustering → Ligand efficiency filtering → Interaction analysis → 100 ns molecular dynamics

## Screening Summary

| Stage | Method | Compounds |
|---|---|---:|
| Initial library | NPASS natural product database | ~94,400 |
| 1 | RDKit filtering and predicted ADMET assessment | 369 |
| 2 | AutoDock Vina docking (score ≤ -8.0 kcal/mol) | 128 |
| 3 | PCA and K-means clustering (4 clusters; top 4 per cluster) | 16 |
| 4 | Ligand efficiency threshold (≥ 0.35) | 12 |
| 5 | Complex preparation and interaction analysis | 10 analyzed |
| 6 | Selection for molecular dynamics | 4 |
| 7 | 100 ns molecular dynamics simulations | 2 relatively stable candidates |

## Target Protein and Docking Validation

**Target:** Enoyl-ACP reductase (FabI)  
**Organism:** *Acinetobacter baumannii*  
**Structure:** [PDB 6AHE](https://www.rcsb.org/structure/6AHE)  
**Resolution:** 2.29 Å

The crystal structure contains FabI in complex with the inhibitor AFN-1252 and a nicotinamide adenine dinucleotide cofactor.

The receptor preparation retained protein chain A and the NAD cofactor for docking.

### Redocking Validation

The native inhibitor AFN-1252 was extracted and redocked into its binding site to assess the docking protocol.

| Parameter | Result |
|---|---:|
| Redocking score | -10.8 kcal/mol |
| Heavy-atom RMSD | 1.73 Å |
| RMSD acceptance threshold | 2.0 Å |

The redocking RMSD was below the commonly used 2.0 Å threshold, supporting the ability of the docking protocol to reproduce the crystallographic binding pose.

### Docking Parameters

| Parameter | Setting |
|---|---|
| Software | AutoDock Vina |
| Exhaustiveness | 32 |
| Grid center X | -37.508 Å |
| Grid center Y | -7.028 Å |
| Grid center Z | -3.125 Å |
| Grid dimensions | 26 × 26 × 30 Å |
| Selection threshold | ≤ -8.0 kcal/mol |

### Ligand Preparation

- 3D conformer generation using RDKit ETKDGv3.
- Geometry optimization using MMFF94.
- PDBQT conversion using Open Babel.
- Gasteiger partial charges for docking.

## Cheminformatics and Chemical-Space Analysis

The initial NPASS library was processed using RDKit to remove invalid and duplicate structures and apply molecular property filters.

### Compound Filtering

The filtering pipeline included:

- Lipinski's Rule of Five (zero violations).
- PAINS substructure filtering.
- Fewer than 10 rotatable bonds.
- Predicted ADMET assessment using ADMET-AI.

A total of 369 compounds passed the applied filtering criteria.

### Chemical-Space Analysis

Morgan fingerprints (radius 2, 1024 bits) were generated to represent molecular structures.

Principal Component Analysis (PCA) was applied to explore chemical-space distribution, followed by K-means clustering using four clusters.

The first two principal components explained approximately 11.33% of the total variance.

The top four docking-scoring compounds from each cluster were selected for further assessment.

PCA and K-means were used for exploratory chemical-space analysis and candidate organization, not as predictive biological activity models.

### PCA Chemical-Space Distribution

The PCA plot illustrates the distribution of screened compounds across the four K-means clusters.

![PCA chemical-space distribution](figures/pca_clusters.png)

[View PCA figure](figures/pca_clusters.png)

### K-means Cluster Optimization

The elbow method and silhouette analysis were used to examine the clustering configuration.

![K-means elbow and silhouette analysis](figures/Kmeans_Elbow_Silhouette.png)

[View K-means analysis](figures/Kmeans_Elbow_Silhouette.png)

### Ligand Efficiency Assessment

Ligand efficiency was estimated using docking scores normalized by the number of heavy atoms:

LE = -Docking score / Number of heavy atoms

Compounds with an estimated ligand efficiency of at least 0.35 kcal/mol per heavy atom were retained for further analysis.

## Selected Natural Product Candidates

Four compounds were prioritized following docking, clustering, ligand efficiency assessment and protein–ligand interaction analysis.

| Compound | Cluster | Vina score (kcal/mol) | Heavy atoms | LE |
|---|---:|---:|---:|---:|
| NPC253314 | 3 | -11.1 | 31 | 0.358 |
| NPC223274 | 4 | -10.4 | 23 | 0.452 |
| NPC87794 | 1 | -10.0 | 22 | 0.455 |
| NPC293138 | 1 | -9.3 | 20 | 0.465 |

Reference inhibitor AFN-1252 had a redocking score of -10.8 kcal/mol.

## Protein–Ligand Interaction Analysis

The selected compounds were further examined to characterize their interactions within the FabI binding pocket.

Two-dimensional interaction analysis was performed using Discovery Studio Visualizer to inspect the protein–ligand interaction patterns.

The four selected compounds were:

- NPC253314
- NPC223274
- NPC87794
- NPC293138

Interaction diagrams are available in the [`interaction_analysis/`](interaction_analysis/) directory.

## Molecular Dynamics Simulations

The four selected protein–ligand complexes and the reference inhibitor were subjected to 100 ns molecular dynamics simulations using GROMACS 2023.3.

### Simulation Setup

| Parameter | Setting |
|---|---|
| Software | GROMACS 2023.3 |
| Force field | CHARMM36 |
| Water model | TIP3P |
| Ligand parameterization | CGenFF |
| Cofactor | NADH |
| NVT equilibration | 1 ns |
| NPT equilibration | 100 ps |
| Production simulation | 100 ns |
| Time step | 2 fs |
| Temperature | 300 K |
| Pressure | 1 bar |
| Thermostat | V-rescale |
| Barostat | Parrinello-Rahman |
| Electrostatics | Particle Mesh Ewald (PME) |
| Constraints | LINCS |

Each system was simulated once for 100 ns.

### Trajectory Analysis

The following parameters were analyzed:

- Ligand RMSD.
- Ligand radius of gyration.
- Protein RMSF.
- Protein–ligand hydrogen bonds.

### Molecular Dynamics Results

Values are reported as mean ± standard deviation.

| System | Ligand RMSD (nm) | Last 20 ns RMSD (nm) | Mean H-bonds | Frames with ≥1 H-bond |
|---|---:|---:|---:|---:|
| NPC87794 | 0.275 ± 0.048 | 0.256 ± 0.053 | 1.28 | 90.4% |
| NPC253314 | 0.361 ± 0.041 | 0.392 ± 0.030 | 0.85 | 68.9% |
| NPC223274 | 0.471 ± 0.204 | 0.704 ± 0.081 | 0.55 | 48.6% |
| NPC293138 | 0.686 ± 0.243 | 0.958 ± 0.149 | 1.36 | 83.5% |
| AFN-1252 (control) | 0.326 ± 0.076 | 0.384 ± 0.046 | 1.31 | 78.6% |

### Interpretation

NPC87794 maintained a relatively stable binding pose throughout the simulation, with a mean ligand RMSD of 0.275 nm and hydrogen bonding observed in 90.4% of analyzed frames.

NPC253314 also maintained a relatively stable binding pose, with a mean ligand RMSD of 0.361 nm.

In comparison, NPC223274 showed a substantial increase in ligand RMSD after approximately 40 ns, while NPC293138 exhibited progressive displacement from its initial binding pose.

Based on these computational observations, NPC87794 and NPC253314 were prioritized for further investigation.

Molecular dynamics analysis files and available results are organized in the [`md/`](md/) directory.

## Repository Structure

```text
acinetobacter-fabi-natural-product-discovery/
│
├── data/                    # Selected candidate compounds
├── docking/                 # Molecular docking results
├── docs/                    # Methodology documentation
├── figures/                 # PCA and clustering visualizations
├── interaction_analysis/    # Protein–ligand interaction diagrams
├── md/                      # Molecular dynamics files and analysis
├── notebooks/               # Cheminformatics and post-docking analysis
├── protein/                 # Prepared receptor structures
│
├── requirements.txt
├── LICENSE
└── README.md
```

## Computational Tools

| Tool | Application |
|---|---|
| Python | Computational workflow |
| RDKit | Molecular processing and fingerprints |
| Scikit-learn | PCA and K-means clustering |
| AutoDock Vina | Molecular docking |
| Open Babel | Molecular format conversion |
| ADMET-AI | Predicted ADMET properties |
| UCSF Chimera | Molecular structure preparation |
| Discovery Studio Visualizer | Protein–ligand interaction analysis |
| GROMACS | Molecular dynamics simulations |
| CHARMM36 / CGenFF | Protein and ligand parameterization |

## Installation and Requirements

Python dependencies are listed in `requirements.txt`.

Install them using:

```bash
pip install -r requirements.txt
```

The following external software packages are also required:

- AutoDock Vina
- Open Babel
- UCSF Chimera
- Discovery Studio Visualizer
- GROMACS

See [`docs/workflow_methodology.md`](docs/workflow_methodology.md) for additional methodology details.

## Limitations

- Docking scores are computational estimates and do not represent experimentally measured binding affinities.
- Docking validation was performed through redocking; decoy-based enrichment validation was not conducted.
- ADMET properties were predicted computationally.
- PCA and K-means provide exploratory chemical-space analysis rather than biological activity prediction.
- Each molecular dynamics system was simulated once; independent replicate simulations are needed to assess reproducibility.
- Binding free-energy calculations were not performed.
- Gram-negative bacterial permeability and efflux were not experimentally assessed.
- No biochemical, microbiological or cellular experiments have been performed.

The selected compounds should therefore be considered computationally prioritized candidates rather than experimentally validated FabI inhibitors or antibiotics.

## Data Availability

- **Protein structure:** [RCSB Protein Data Bank, PDB 6AHE](https://www.rcsb.org/structure/6AHE)
- **Natural product library:** [NPASS database](https://bidd.group/NPASS/)
- **Source code:** Available in this repository.

## License

This project is distributed under the MIT License. See [`LICENSE`](LICENSE).

## Author

**Mateen Ahmad**

MS Biotechnology | Computational Drug Discovery

- GitHub: [@abmateen612](https://github.com/abmateen612)
- Repository: [Acinetobacter FabI Natural Product Discovery](https://github.com/abmateen612/acinetobacter-fabi-natural-product-discovery)
