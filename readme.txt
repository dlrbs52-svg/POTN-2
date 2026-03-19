# POTN-2: HLA-A*02:01 Immunogenic Peptides Screening Model

POTN-2 is an enhanced neoantigen prediction tool specifically designed for the HLA-A*02:01 allele. It integrates comprehensive feature engineering (sequence length, positional information, amino acid composition, biological properties, and physicochemical features) with machine learning algorithms (Random Forest, Convolutional Neural Network, and Support Vector Machine) to achieve superior prediction performance. The implementation is based on Meng et al., Front. Immunol. 2020 (POTN) and the extended work described in the accompanying manuscript.

## Overview
This repository provides pre-trained models, datasets, and Jupyter notebooks for predicting HLA-A*02:01-binding immunogenic peptides (neoantigens). It includes resources for feature extraction, model training, evaluation, and protocols for predicting the immunogenicity of new peptide sequences using POTN-2 models.

## Features
- Pre-trained models for HLA-A*02:01 neoantigen prediction (RF, CNN, SVM)
- Three optimized feature sets (59, 65, and 109 features) derived from multi-stage selection
- Datasets for training and evaluation (curated from IEDB and UniProt)
- Jupyter notebooks for replicating experiments and model training
- Tools for feature extraction from peptide sequences
- Support for multiple input formats: single peptide sequences, protein FASTA files, and high-throughput sequencing data
- Web server for easy online prediction

## Usage
**1. Feature Extraction:** Use the provided scripts to compute the 109 physicochemical and biological features for your peptide sequences.

**2. Model Training:** Utilize the Jupyter notebooks to train the models with your own datasets or the provided datasets.

**3. Evaluation:** Evaluate the performance of the models using the provided test sets and independent validation datasets.

**4. Prediction:** Follow the protocols to predict the immunogenicity of new peptides using the pre-trained POTN-2 models.

## Directory Structure
- **`dataset/`** – Contains training, testing, and independent validation datasets.
- **`models/`** – Pre-trained models organized by algorithm and feature set (e.g., RF_59, CNN_109, SVM_65).
- **`notebooks/`** – Jupyter notebooks for feature analysis, model training, and evaluation.

## Models
Pre-trained models are available for each combination of algorithm and feature set:
- **Random Forest (RF)**: `tumor_model_59_features.joblib`, `tumor_scaler_59_features.joblib`
- **Convolutional Neural Network (CNN)**: `tumor_model_new_features_cnn.h5`
- **Support Vector Machine (SVM)**: `Stumor_svm_model_final.joblib`, `tumor_scaler_final.joblib`

The best-performing model is **CNN_109** (AUC = 0.9516 on independent test set).

## Datasets
- **`A0201_160000.xlsx`** – 160,000 samples used for model training (positive : negative = 2 : 8).
- **`A0201_100000_test.xlsx`** – 100,000 samples used for model testing/evaluation (positive : negative = 2 : 8).

## How to Use It

### Preparing Your Data
1. Save your peptide sequences in a  Excel file named `user_peptides.csv` with a column named `sequence` containing the peptide strings (9-mers recommended; non-9-mers will be truncated or padded as described in the paper).
2. If you have protein sequences (FASTA) or exome sequencing data, refer to the `notebooks/` for preprocessing steps.

### Extracting Features
1. Open `notebooks/Feature_Extraction.ipynb`.
2. Load your peptide sequences and compute the 109 features using the provided functions.
3. Save the output feature matrix as `user_features.csv`.

**Note:**  
- For SVM models, use `joblib` to load the model and apply the same feature scaling as during training (a fitted `StandardScaler` is provided in `models/`).  
- For RF models, you can use `joblib` or `pickle` to load the model and directly predict.  
- The output `Prediction` column contains `1` for predicted immunogenic peptides (binders) and `0` for non-immunogenic.

### Advanced Usage
For batch processing of protein FASTA files or exome sequencing data, please refer to the comprehensive pipeline described in `notebooks/End_to_End_Prediction.ipynb`. This notebook demonstrates:
- Sliding-window generation of 9-mer peptides from protein sequences
- Feature extraction for all candidates
- Model inference and result ranking
- Export of prioritized neoantigen candidates

## Citation
If you use POTN-2 in your research, please cite the original POTN paper and the upcoming publication describing POTN-2:

- Meng, Q. et al. POTN: A Human Leukocyte Antigen-A2 Immunogenic Peptides Screening Model and Its Applications in Tumor Antigens Prediction. *Front. Immunol.* 11, 02193 (2020).
- [Include the new paper citation here when available.]


## Contact
For questions or issues, please open an issue on GitHub or contact the corresponding authors:
- Jiangfeng Du: jiangfengdu@zzu.edu.cn
- [Other authors as appropriate]

