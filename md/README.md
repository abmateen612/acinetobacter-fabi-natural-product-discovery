# Molecular Dynamics

100 ns MD simulations of FabI (PDB: 6AHE) in complex with NADH and each of four natural-product ligands, plus a control with the co-crystallized ligand AFN-1252 (PDB ligand ID 0WE).

## Systems

| System | Description |
|---|---|
| NPC87794 | FabI + NADH + ligand |
| NPC253314 | FabI + NADH + ligand |
| NPC223274 | FabI + NADH + ligand |
| NPC293138 | FabI + NADH + ligand |
| Control | FabI + NADH + AFN-1252 (0WE) |

Each system was simulated once.

## Setup

| Setting | Value |
|---|---|
| Software | GROMACS 2023.3 |
| Force field | CHARMM36 |
| Ligand and NADH topologies | CGenFF server, converted with `cgenff_charmm2gmx.py` |
| Water model | TIP3P, neutralized with counterions |
| Equilibration | NVT 1 ns (300 K), NPT 100 ps (1 bar, Berendsen), position restraints on protein and ligand |
| Production | 100 ns, 2 fs time step, 300 K, 1 bar |
| Thermostat / barostat | V-rescale / Parrinello-Rahman |
| van der Waals | force-switch 1.0 to 1.2 nm |
| Electrostatics | PME, real-space cutoff 1.2 nm |
| Constraints | LINCS (bonds involving hydrogens) |

## Files

| File | Purpose |
|---|---|
| `ions.mdp` | Adding counterions |
| `em.mdp` | Energy minimization |
| `nvt.mdp` | NVT equilibration |
| `npt.mdp` | NPT equilibration |
| `md.mdp` | 100 ns production run |

## Analysis

Trajectories were analyzed with GROMACS tools after removing periodic boundary effects and fitting to the protein backbone: protein backbone RMSD, ligand RMSD, Cα RMSF, radius of gyration, and ligand-protein hydrogen bonds.

Trajectory files are not included because of their size.
