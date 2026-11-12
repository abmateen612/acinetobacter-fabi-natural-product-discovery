# Workflow and Methodology

Workflow of the FabI virtual screening project. Only the NPASS natural product library is used.

**Status:** research code accompanying a manuscript in preparation. All results are computational and have not been tested experimentally.

## Pipeline

| Step | Method | Compounds left |
|---|---|---|
| 0 | NPASS library (2023 update) | ~94,400 |
| 1 | RDKit filtering: invalid/duplicate removal, Lipinski (0 violations), PAINS, rotatable bonds < 10, predicted ADMET | 369 |
| 2 | AutoDock Vina docking, score <= -8.0 kcal/mol | 128 |
| 3 | Morgan fingerprint PCA + KMeans (k = 4), top 4 per cluster | 16 |
| 4 | Ligand efficiency >= 0.35 kcal/mol per heavy atom | 12 |
| 5 | Complex preparation (failed for 2 compounds), then 2D interaction analysis | 10 → 4 |
| 6 | 100 ns molecular dynamics (GROMACS) | 2 stable |

## Receptor

PDB 6AHE (A. baumannii FabI with NAD and AFN-1252, 2.29 Å, homotetramer), prepared in UCSF Chimera 1.19. Water molecules, ions and non-essential chains were removed, and chain A was kept with its NAD cofactor. The native ligand (0WE) was saved separately for docking validation. NAD was kept in the receptor because AFN-1252 forms a ternary complex with FabI and the cofactor. Partial charges were assigned and the receptor was saved in PDBQT format. For MD, the cofactor was converted to NADH.

## Docking validation

The native ligand AFN-1252 was redocked into the NAD-bound receptor with the screening settings. The top pose was compared with the crystallographic pose (heavy-atom RMSD over 28 atoms, no superposition): RMSD 1.73 Å (below 2.0 Å). Docking score: -10.8 kcal/mol, used as the reference value.

## Filtering

Compounds from NPASS were filtered in RDKit. Invalid structures and duplicates were removed. Compounds were kept only if they had no Lipinski violations, no PAINS substructures, fewer than 10 rotatable bonds, and favorable predicted ADMET properties. 369 compounds remained.

## Ligand preparation

3D structures were generated with ETKDGv3 (RDKit), minimized with MMFF94, and converted to PDBQT with Open Babel (Gasteiger charges).

## Docking

| Setting | Value |
|---|---|
| Program | AutoDock Vina |
| Grid centre | -37.508, -7.028, -3.125 |
| Grid size | 26 x 26 x 30 Å |
| Exhaustiveness | 32 |
| Poses kept | top-ranked pose per compound |
| Score cut-off | <= -8.0 kcal/mol (128 compounds) |

## Selection

- **Diversity:** Morgan fingerprints (radius 2, 1024 bits), PCA (PC1 6.66%, PC2 4.67% of variance), KMeans with k = 4 chosen by elbow and silhouette analysis (cluster sizes 35, 27, 34, 32). Top 4 compounds per cluster by docking score gave 16 compounds.
- **Efficiency:** ligand efficiency = -(docking score) / number of heavy atoms. Compounds with LE >= 0.35 were kept
