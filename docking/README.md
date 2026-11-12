# Molecular Docking

Docking of the filtered NPASS natural-product library against FabI from *Acinetobacter baumannii* (PDB: 6AHE, NAD retained).

## Software and settings

| Setting | Value |
|---|---|
| Program | AutoDock Vina |
| Receptor | `protein/receptor.pdbqt` |
| Grid centre | -37.508, -7.028, -3.125 |
| Grid size | 26 x 26 x 30 Å |
| Exhaustiveness | 32 |
| Poses kept | top-ranked pose per compound |

## Protocol validation

The native ligand AFN-1252 was redocked with the same settings. RMSD to the crystallographic pose: 1.73 Å (28 heavy atoms, no superposition). Docking score: -10.8 kcal/mol, used as the reference value.

## Docking and prioritization

All 369 compounds that passed RDKit filtering were docked. Compounds with a score of -8.0 kcal/mol or better were kept:

**369 compounds → 128 compounds**

These 128 compounds were then used for PCA, KMeans clustering, ligand-efficiency filtering and interaction analysis.

## Files

| File | Description |
|---|---|
| `docking_scores_369.csv` | Vina score of each of the 369 docked compounds, plus the AFN-1252 reference row (to be added) |

## Note

Docking scores are computational predictions and are not measured binding affinities. Scores from different programs cannot be compared directly.
