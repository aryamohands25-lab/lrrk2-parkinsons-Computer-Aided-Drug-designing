# Parkinson’s Disease Drug Discovery Using Machine Learning (CADD)

## Overview

This educational project explores a machine-learning workflow for computer-aided drug design (CADD), using molecular structures and IC50 measurements associated with LRRK2 to model pIC50 activity. It includes data cleaning, RDKit Morgan fingerprints, molecular descriptors, PaDEL descriptor processing, regression-model comparison, and an exploratory virtual-screening step for selected Parkinson’s-related compounds.

> **Important:** This is an exploratory computational project. Predicted pIC50 values are not experimental results and do not establish clinical efficacy, safety, or suitability for treating Parkinson’s disease. The notebook requires further validation before its predictions should be interpreted biologically.

## Project workflow

1. Load a BindingDB-derived LRRK2 activity dataset.
2. Select compound identifiers, SMILES, and IC50 values.
3. Clean missing, duplicate, and non-numeric activity records.
4. Convert IC50 (nM) to pIC50 using `pIC50 = 9 - log10(IC50 in nM)`.
5. Generate RDKit Morgan fingerprints and molecular descriptors.
6. Generate PaDEL descriptors in batches and examine feature correlations.
7. Train and compare regression models using cross-validation and a held-out split.
8. Apply the trained model to selected Parkinson’s-related compounds as an exploratory virtual-screening exercise.

## Tools

- Python, Pandas, NumPy
- RDKit
- PaDEL-Descriptor / `padelpy`
- scikit-learn
- Matplotlib and Seaborn
- Google Colab (the notebook currently contains Colab-specific paths and Drive mounting)

## Repository contents

- `Parkinsons_Disease_CADD_ML.ipynb` — project notebook
- `results/` — selected result screenshots
- `requirements.txt` — main Python dependencies
- `REVIEW_BEFORE_PUBLICATION.md` — important reproducibility and scientific checks

## Dataset

The notebook expects a tab-separated file named `LRRK2.tsv` at `/content/LRRK2.tsv`. The dataset itself is not included in this repository. Obtain it from the original source and verify its license/terms before use or redistribution. Update the file path when running outside Google Colab.

## Run the notebook

1. Open the notebook in Google Colab or Jupyter.
2. Obtain the dataset and place it at the expected path, or update the loading cell.
3. Install the dependencies listed in `requirements.txt`. PaDEL may require Java and may need additional setup depending on the environment.
4. Run the notebook from top to bottom, ensuring generated batch CSVs and descriptor tables are available where expected.
5. Review `REVIEW_BEFORE_PUBLICATION.md` and address the listed issues before treating metrics as final.

## Preliminary results

The screenshots currently included show an example PaDEL descriptor model comparison where Random Forest achieved a test R² of approximately 0.65. This value is from the current notebook run and should be treated as preliminary until data alignment, leakage, split strategy, and target consistency have been checked.

## Limitations and next steps

- Verify that descriptor rows remain correctly aligned with each molecule and its pIC50 label after invalid molecules and missing descriptors are removed.
- Use a molecule-aware/scaffold split and fit feature selection only on training data to reduce leakage risk.
- Confirm target identity and activity assay comparability for every record.
- Investigate duplicate structures and repeated measurements.
- Validate predictions on independent compounds with known activity against the same target.
- Do not use the agreement of predicted values for marketed Parkinson’s drugs as proof that the model is validated.

## Disclaimer

For educational and research use only. This project does not provide medical advice or experimentally confirmed drug recommendations.
