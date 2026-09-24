# Adversarial Evaluation of Deep Learning-Based IDS for Encrypted Network Traffic

This repository contains the experimental code used to evaluate the adversarial vulnerability of a hybrid CNN--ECA--Transformer intrusion detection model for encrypted network traffic. The experiments assess how the model behaves under clean conditions and under adversarial perturbations generated with FGSM and PGD.

## Repository Objective

The goal of this repository is to support the reproducibility of an empirical study on adversarial attacks against deep learning-based intrusion detection systems (IDS). The code evaluates the target model under two threat settings:

- **White-box attacks**, where the adversary has access to the target model gradients.
- **Black-box transfer attacks**, where adversarial examples are generated using a surrogate model trained from target-model outputs.

The evaluation is conducted on two encrypted traffic datasets:

- **HIKARI-2021**
- **CIRA-CIC-DoHBrw-2020**

## Experimental Scope

The repository includes notebooks for:

- Training and evaluating the target IDS model under clean conditions.
- Generating adversarial examples with **FGSM** and **PGD**.
- Evaluating white-box adversarial robustness.
- Evaluating surrogate-based black-box transferability.
- Computing standard classification metrics and the IDS-specific **Attack Success Rate for IDS (ASR-I)**.

ASR-I measures the proportion of malicious samples that were correctly detected before the attack and became misclassified as benign after adversarial perturbation. This avoids counting pre-existing clean-model errors as successful adversarial evasions.

## Files

| File | Description |
|---|---|
| `Adversarial_Attacks_WhiteBox_HIKARI.ipynb` | White-box FGSM/PGD evaluation on HIKARI-2021. |
| `Adversarial_Attacks_WhiteBox_CIRA.ipynb` | White-box FGSM/PGD evaluation on CIRA-CIC-DoHBrw-2020. |
| `Adversarial_Attacks_BlackBox_HIKARI.ipynb` | Surrogate-based black-box FGSM/PGD evaluation on HIKARI-2021. |
| `Adversarial_Attacks_BlackBox_CIRA.ipynb` | Surrogate-based black-box FGSM/PGD evaluation on CIRA-CIC-DoHBrw-2020. |

## Main Methodological Features

- Stratified train/validation/test splitting.
- Training-set-only class balancing with SMOTE.
- Min--Max normalization fitted only on the training set.
- Removal of invalid values and duplicate records.
- Evaluation across multiple random seeds.
- FGSM and PGD attacks under multiple perturbation budgets.
- White-box and black-box threat-model comparison.
- Reporting of Accuracy, Precision, Recall, F1-score, AUC, and ASR-I.

## Requirements

The notebooks were developed in Python and rely mainly on:

- TensorFlow / Keras
- NumPy
- Pandas
- Scikit-learn
- Imbalanced-learn

A GPU-enabled environment is recommended for efficient execution.


## Reproducibility Notes

Each notebook is designed to run an independent experimental protocol for one dataset and one threat setting. To reproduce the complete evaluation, execute the four notebooks and aggregate the exported metric files.

## Anonymity Notice

This repository is intended for anonymous peer review. Author names, affiliations, and identifying metadata have been intentionally omitted.


## Dataset Access

The datasets are not redistributed in this repository due to licensing and storage constraints. Users must download them from their official sources before running the experiments.

- **HIKARI-2021**: available through Zenodo.  
  Official download page: [https://zenodo.org/records/5199540](https://zenodo.org/records/5199540)

- **CIRA-CIC-DoHBrw-2020**: available through the Canadian Institute for Cybersecurity, University of New Brunswick.  
  Official dataset page: [https://www.unb.ca/cic/datasets/dohbrw-2020.html](https://www.unb.ca/cic/datasets/dohbrw-2020.html)

After downloading the datasets, place the primary CSV files directly in the repository root directory (the same folder containing the notebooks) and name them exactly as follows:

├── Adversarial_Attacks_WhiteBox_HIKARI.ipynb
├── Adversarial_Attacks_WhiteBox_CIRA.ipynb
├── Adversarial_Attacks_BlackBox_HIKARI.ipynb
├── Adversarial_Attacks_BlackBox_CIRA.ipynb
├── ALLFLOWMETER_HIKARI2021.csv
├── CIRA-CIC-DoHBrw-2020.csv



## Environment Setup

The repository provides a minimal `requirements.txt` file containing the main dependencies required to run the four experimental notebooks.

To install the dependencies, run:

```bash
pip install -r requirements.txt