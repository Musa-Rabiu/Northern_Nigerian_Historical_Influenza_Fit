# Hierarchical Spatiotemporal Bayesian SEIR Framework for Multi-Stream Epidemic Dynamics

[![Stan](https://shields.io)](https://mc-stan.org/)
[![R](https://shields.io)](https://r-project.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This repository contains the complete source code, Stan implementation, data preprocessing pipelines, fitted model objects, and generated posterior CSV outputs for the research manuscript titled:

> **"Hierarchical Spatiotemporal Bayesian SEIR Modeling of Multi-Stream Epidemic Dynamics: Computational Benchmarking and Climate-Forced Wave Propagation"**

---

## Repository Overview

This project implements and benchmarks a stochastic, state-space **hierarchical spatiotemporal Bayesian (HMB) SEIR** model fitted across 156 weeks of synthetic multi-stream surveillance data (reported cases, hospital admissions, and inpatient deaths) from the **MAEPiMS Challenge 2026**, spanning **20 subnational administrative units** (19 Northern Nigerian states and the Federal Capital Territory).

### Core Methodological Features
* **Decoupled Multi-Stream Observation Cascade:** Evaluates reported cases, hospital admissions, and mortality counts downstream of latent community infection flux (\(\Delta I_{s,t}^{\text{week}}\)) via logit-linked regressions driven by standardized healthcare accessibility indices.
* **Climate-Zone Seasonality:** Incorporates primary annual and secondary semi-annual Fourier harmonic forcing (\(A_{1,c[s]}, A_{2,c[s]}\)) stratified across two contiguous ecological zones (**Sahel** and **Savanna**).
* **Spatiotemporal Dynamics:** Utilizes non-centered spatial random effects and a 3,120-dimensional latent process noise matrix (\(\dim(\boldsymbol{\theta}) = 3,247\)) to capture regional wave propagation fronts without requiring explicit mobility matrices.
* **Numerical Stability via Sub-Stepping:** Employs a 7-day daily sub-stepping integration scheme (\(\Delta t = 1/7\) weeks) within discrete-time mass-conserving SEIR transitions.
* **Full Posterior Inference:** Executed via non-centered Hamiltonian Monte Carlo (HMC) sampling using the No-U-Turn Sampler (NUTS) in Stan.

---

## Repository Directory Structure

```text
├── data/                      # Synthetic challenge surveillance streams, spatial covariates, and accessibility indices
├── models/                    # Stan model files (.stan) implementing the SEIR sub-stepping engine
├── scripts/                   # R data preprocessing, MCMC execution, and diagnostic plotting scripts
├── outputs/                   # Generated posterior CSV draw files, convergence metrics, and summary tables
├── figures/                   # Rendered posterior fits, spatial maps, and MCMC trace/pair diagnostic PDFs
└── README.md                  # Project documentation and reproducibility guide
```

---

## Prerequisites & Installation

To run the model and reproduce the posterior analyses, ensure you have the following software and R packages installed:
* **R** ($\ge 4.2$)
* **Stan / CmdStanR** ($\ge 2.32$)
* **Core R Packages:** `tidyverse`, `cmdstanr`, `posterior`, `bayesplot`, `sf`

You can install `cmdstanr` and CmdStan directly in R via:

```r
install.packages("cmdstanr", repos = c("https://mc-stan.org/r-packages/", getOption("repos")))
cmdstanr::install_cmdstan()
```

---

## Reproducibility Workflow

1. **Preprocess Surveillance Data:**  
   Run the data cleaning script to filter and format the 156-week multi-stream inputs for the 20 administrative units:
   ```r
   source("scripts/01_data_preprocessing.R")
   ```

2. **Execute Stan MCMC Sampling:**  
   Compile and run the hierarchical spatiotemporal Bayesian SEIR model across 4 parallel chains:
   ```r
   source("scripts/02_run_stan_model.R")
   ```

3. **Generate Diagnostics and Figures:**  
   Inspect convergence metrics ($\hat{R} \le 1.05$, Bulk/Tail ESS, zero divergences) and render publication figures:
   ```r
   source("scripts/03_generate_diagnostics.R")
   ```

---

## Citation

If you use code, data structures, or model formulations from this repository in your academic research, please cite our manuscript:

```bibtex
@article{rabiu2026seir,
  title={Hierarchical Spatiotemporal Bayesian SEIR Modeling of Multi-Stream Epidemic Dynamics: Computational Benchmarking and Climate-Forced Wave Propagation},
  author={Rabiu, Musa},
  journal={Preprint},
  year={2026}
}
```

---

## License

This project is open-source and licensed under the **MIT License**.
