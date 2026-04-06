# Part 4: Mastering Salt Stripping and SMILES Curation with RDKit
### <sub>This repository contains the implementation of a high-fidelity chemical data curation pipeline. The goal is to transform "noisy" raw SMILES into clean, standardized structures ready for drug-likeness assessment and machine learning.</sub>

![Python](https://img.shields.io/badge/python-3.7+-blue.svg)
![RDKit](https://img.shields.io/badge/RDKit-2022.03+-green.svg)
![Pandas](https://img.shields.io/badge/Pandas-Latest-orange.svg)

## 🧪 Project Overview
In drug discovery, raw datasets often include non-pharmacophore fragments that distort physicochemical descriptors. A common example is a Bromide counter-ion (~80 Da) pushing a 450 Da molecule over the 500 Da Lipinski limit, resulting in a false negative.

This pipeline provides a three-stage hierarchy to solve these challenges:

Neutralization: Converting ions to their neutral active forms (e.g., Sodium Benzoate → Benzoic Acid).

Intelligent Salt Stripping: Removing common counter-ions while protecting permanent cations like Quaternary Ammonium salts using custom SMARTS filtering.

Stoichiometric Deduplication: Cleaning redundant fragments (e.g., Drug.Drug → Drug) to ensure accurate Molecular Weight and LogP calculations.

## 📂 Repository Structure
* Part_4_SMILES_Curation.ipynb: The main Jupyter Notebook containing the step-by-step tutorial.
* functions/: Python scripts for the Mol_Uncharger, Salt_Remover, and Final_Cleaner.
* data/: Sample dataset featuring complex salts, zwitterions, and duplicates.

## 💻 How to Use
You can import the curation functions and run them in sequence to process your dataset:
```python
from rdkit import Chem
# ... (Import your custom functions here)

smi_list = ['C(C1=CC=CC=C1)(=O)[O-].[Na+]', '[Cl-].C(=[NH2+])N']

# Apply the Pipeline
u_mol, uncharged = Mol_Uncharger(smi_list)
s_mol, stripped = Salt_Remover(uncharged)
f_mol, final_data = Final_Cleaner(stripped)

print(final_data) 
# Output: ['C(=O)(O)c1ccccc1', 'NC=[NH]']
```

## 📊 Results
The script implements a hierarchical data cleaning pipeline. By sequentially applying Uncharging, Selective Salt Stripping, and Fragment Deduplication, it successfully transforms complex chemical mixtures into standardized, single-component SMILES. This ensures that downstream molecular descriptor calculations reflect the properties of the active pharmaceutical moiety.

## 🔗 Related Articles
Part 1: A Chemist’s Guide to RDKit & Python

Part 2: SMILES Standardization and Tautomers

Part 3: Analysis of Drug-Likeness

Part 4: SMILES Data Cleaning: Mastering Salt Stripping

## 🤝 Contributing
If you find a stubborn salt or a specific SMARTS pattern that should be added to the protection logic, feel free to open an issue or a pull request!
