# Epileptic Seizure Prediction using an Evolving Neuro-Fuzzy Model

![MATLAB](https://img.shields.io/badge/MATLAB-Research%20Code-orange)
![Status](https://img.shields.io/badge/status-research%20prototype-blue)
![Domain](https://img.shields.io/badge/domain-EEG%20%7C%20Seizure%20Prediction-purple)
![Model](https://img.shields.io/badge/model-Evolving%20Neuro--Fuzzy-green)

This repository contains a MATLAB implementation of an online epileptic seizure prediction framework based on EEG phase synchronization and an evolving neuro-fuzzy model.

The project is associated with the following peer-reviewed paper:

> **Alaei, H. S., Khalilzadeh, M. A., & Gorji, A. (2019).**  
> *Optimal selection of SOP and SPH using fuzzy inference system for on-line epileptic seizure prediction based on EEG phase synchronization.*  
> Australasian Physical & Engineering Sciences in Medicine, 42, 1049–1068.  
> https://doi.org/10.1007/s13246-019-00806-w

---

## Overview

Epileptic seizures can occur unpredictably, which creates serious risks for people with drug-resistant epilepsy. A reliable seizure prediction system should not only identify an upcoming seizure accurately, but also provide a useful warning time while keeping the number of false alarms low.

This project implements an online seizure prediction model using:

- EEG phase synchronization features
- Mean phase coherence between EEG channel pairs
- Patient-specific feature selection
- Evolving Neuro-Fuzzy Model (ENFM)
- Seizure Prediction Horizon (SPH)
- Seizure Occurrence Period (SOP)
- Moving-average-based post-processing to reduce false alarms

The original study proposed a fuzzy inference system to select suitable SOP and SPH values for each patient. The aim was to provide a clinically meaningful warning interval while keeping the uncertainty period as short as possible.

---

## Key Concepts

### Seizure Prediction Horizon (SPH)

The **Seizure Prediction Horizon (SPH)** is the time interval between an alarm and the beginning of the period in which a seizure is expected to occur.

A longer SPH can be useful because it gives the patient more time to take safety precautions.

### Seizure Occurrence Period (SOP)

The **Seizure Occurrence Period (SOP)** is the time window after the SPH during which the seizure is expected to happen.

A shorter SOP is preferable because it reduces uncertainty and may lower patient stress.

### Evolving Neuro-Fuzzy Model (ENFM)

The **Evolving Neuro-Fuzzy Model (ENFM)** is an adaptive online learning model based on recursive fuzzy clustering. It can update its structure over time by adding or merging fuzzy rules as new samples arrive.

---

## Method Pipeline

The general workflow is:

```text
EEG recordings
    ↓
Sliding-window segmentation
    ↓
Frequency-band decomposition
    ↓
Phase synchronization calculation
    ↓
Mean phase coherence features
    ↓
Feature selection
    ↓
Online classification using ENFM
    ↓
Moving-average post-processing
    ↓
Seizure warning output
```
---

## Repository Structure

```text
Epileptic-Seizure-Prediction/
│
├── README.md          # Project documentation
├── main.m             # Main script for running the seizure prediction example
├── ENFM.m             # Evolving Neuro-Fuzzy Model implementation
├── X.mat              # Selected phase synchronization features
├── Y.mat              # Binary labels: seizure / non-seizure
├── Z.mat              # Phase synchronization features from the non-evaluative segment
└── .gitattributes
```

---

## Data Description

The included `.mat` files provide pre-extracted feature-level data used by the MATLAB script.

| File | Description |
|---|---|
| `X.mat` | Selected EEG phase synchronization features |
| `Y.mat` | Binary labels for seizure and non-seizure states |
| `Z.mat` | Phase synchronization features from the non-evaluative segment |
| `main.m` | Loads the data, applies ENFM, and performs post-processing |
| `ENFM.m` | Implements the evolving neuro-fuzzy classifier |

The raw EEG preprocessing and full feature extraction pipeline are not fully included in this repository. The current version focuses mainly on the online prediction model using extracted features.

---

## Requirements

This project was implemented in **MATLAB**.

Recommended environment:

- MATLAB R2018a or later
- Basic MATLAB numerical computing functionality

---

## How to Run

1. Clone the repository:

```bash
git clone https://github.com/Hesam-lab/Epileptic-Seizure-Prediction.git
cd Epileptic-Seizure-Prediction
```

2. Open MATLAB.

3. Set the repository folder as the current working directory.

4. Run:

```matlab
main
```

The script loads the feature matrices and labels, applies the ENFM classifier, and performs post-processing to generate seizure prediction outputs.

---

## Main Parameters

In `main.m`, the main configurable parameters include:

```matlab
sop = 10;      % Seizure Occurrence Period in minutes
sph = 30;      % Seizure Prediction Horizon in minutes

N = 16;        % Length of each EEG time window in seconds
M = 3.2;       % Length of overlap between windows in seconds

m = 2;         % Fuzziness parameter for clustering
lambda = 1;    % Forgetting factor in RLS update rule

th1 = 0.2;     % Threshold for adding new clusters
th2 = 0.3;     % Threshold for merging similar clusters

window = 15;   % Moving-average filter length in minutes
```

You can change `sop` and `sph` to test different seizure prediction horizons and occurrence periods.

---


## Citation

If you use this code or build upon this work, please cite:

```bibtex
@article{alaei2019optimal,
  title={Optimal selection of SOP and SPH using fuzzy inference system for on-line epileptic seizure prediction based on EEG phase synchronization},
  author={Shokouh Alaei, Hesam and Khalilzadeh, Mohammad Ali and Gorji, Ali},
  journal={Australasian Physical \& Engineering Sciences in Medicine},
  volume={42},
  pages={1049--1068},
  year={2019},
  publisher={Springer},
  doi={10.1007/s13246-019-00806-w}
}
```

---

## Author

**Hesam Shokouh Alaei**  
Researcher in biomedical signal processing, EEG/ECG analysis, machine learning, and seizure-related modelling.

GitHub: [Hesam-lab](https://github.com/Hesam-lab)
