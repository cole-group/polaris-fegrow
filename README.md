# polaris-fegrow

Submission to [polaris binding pose challenge](https://polarishub.io/competitions/asap-discovery/antiviral-ligand-poses-2025).

Compounds are grown using [FEgrow](https://github.com/cole-group/FEgrow). FEgrow is an open-source software package for building congeneric series of compounds in protein binding pockets. For a given ligand core and receptor structure, it employs hybrid machine learning / molecular mechanics potential energy functions to optimise the bioactive conformers of supplied linkers and functional groups.

Specifically, an ensemble of ligand conformations is generated using the ETKDG algorithm in RDKit, with tight restraints on a user-defined rigid core. Conformers are structurally optimised using the OpenMM software. During energy minimisation, the protein is treated using the AMBER FF14SB force field. Intramolecular energetics of the ligand are described,using the ANI-2x machine learning potential. Non-bonded interactions between the protein and ligand are described using a mechanical embedding scheme, with electrostatics and Lennard-Jones terms described by the Open Force Field 'Sage' general force field. The general idea is to make maximum use of structural biology input through the rigid core, and advanced MLPs to accurately describe the ligand's potential energy surface (while being significantly faster than full QM/MM).

### SARS

Pyridine was taken as the core structure, as it seemed to be structurally conserved amongst many of the training set. The core structure was taken from `complex-79` from the training set, as it provided a well-conserved vector into the binding pocket. All test set compounds were grown from the same core.

For compounds for which no structures could be grown (or that lacked the pyridine substructure), a second round started from `complex-48` (as there was some movement in key binding pocket residues in this structure).

Finally, the remaining four structures were docked using gnina.

### MERS

The provided reference ligand did not seem to provide a good vector off the pyridine. So the pyridine R-group was first re-built off the 5-membered ring, and the re-built core used for growing the test compounds.

Molecules that could not be grown were attempted again by overlaying training structure `complex-79` with the MERS reference, and growing off the pyridine core.

Finally, the remaining four structures were docked using gnina (one of which was due to a protonation state mis-match between FEgrow and the provided SMILES).

