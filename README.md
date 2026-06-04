# Cell-Penetrating Peptide Activity Prediction (CPP)

ML pipeline for CPP classification and cellular uptake regression,
built on the POSEIDON experimental database. Developed as part of the
DataCon 3.0 hackathon (AI in Chemistry track).

## Problem

Cell-penetrating peptides (CPPs) are short amino acid sequences capable of crossing
cell membranes, enabling intracellular delivery of drugs, nucleic acids, and proteins.
The goal is to design CPPs with superior activity using ML models — reducing the need
for costly wet-lab screening.

## Pipeline

**Data**  
♡ Source: POSEIDON database (~2 000 experimental records)  
♡ Preprocessing: messy uptake parsing (±, <, / notation), time/temp normalization,
  IQR-based outlier removal, modified sequence filtering  
♡ Feature engineering: RDKit molecular descriptors (MolWt, TPSA, MolLogP, BertzCT,
  BalabanJ, HeavyAtomCount, NHOHCount, NOCount, RingCount, Ipc, LabuteASA, MolMR, qed),
  molecular mass via molmass, binary CPP label from curated FASTA/txt sources  

**Task 1 — CPP Classification**  
♡ Model: Random Forest (MinMaxScaler + SimpleImputer pipeline)  
♡ Features: RDKit descriptors  
♡ Target: CPP / non-CPP binary label  

| Metric | Score |
|---|---|
| Accuracy | 0.802 |
| Precision | 0.804 |
| Recall | 0.802 |
| F1-score | 0.801 |

**Task 2 — Cellular Uptake Regression**  
♡ Model: CatBoost (grid search over iterations, learning rate, depth)  
♡ Features: descriptors + experimental conditions (cell line, cargo, method, time, temp)  
♡ Target: normalized uptake mean  

| Metric | Score |
|---|---|
| R² | 0.79 |
| MAE | 69.56 |
| RMSE | 225.13 |

## Stack

![Python](https://img.shields.io/badge/Python-D6759E?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-D6759E?style=for-the-badge&logo=pandas&logoColor=white)
![RDKit](https://img.shields.io/badge/RDKit-D6759E?style=for-the-badge&logo=rdkit&logoColor=white)
![BioPython](https://img.shields.io/badge/BioPython-D6759E?style=for-the-badge&logo=biopython&logoColor=white)
![molmass](https://img.shields.io/badge/molmass-D6759E?style=for-the-badge&logo=molmass&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-D6759E?style=for-the-badge&logo=scikit-learn&logoColor=white)
![CatBoost](https://img.shields.io/badge/CatBoost-D6759E?style=for-the-badge&logo=catboost&logoColor=white)

## Data Sources

POSEIDON database · CPPBase (FASTA) · Experimental CPP/non-CPP sequence lists

<h2 align="left"> Materials</h2>

* 📋 <a href="https://github.com/uzlova/datacon2024/blob/main/cpp_database.db" target="_blank">Database</a>
* 💻 <a href="https://github.com/uzlova/datacon2024/blob/main/main.ipynb" target="_blank">Code</a>


