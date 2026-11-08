# Hierarchical Bayesian SEIRH Framework for Multi-Stream Epidemic Surveillance in Northern Nigeria

[![Stan](https://img.shields.io/badge/Stan-MCMC-red.svg)](https://mc-stan.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This repository contains the complete source code, Stan implementation, data preprocessing pipelines, fitted model objects, and generated posterior CSV outputs for the research manuscript titled:
> **"Hierarchical Bayesian SEIRH Modeling of Multi-Stream Epidemic Dynamics in Northern Nigeria: Spatiotemporal Wave Propagation and Climate-Forced Transmission"**

---

## Repository Overview

This project implements a stochastic, state-space hierarchical Bayesian **SEIRH** model fitted across 156 weeks of multi-stream surveillance data (reported cases, clinical hospitalizations, and deaths) spanning **20 administrative units** (19 Northern Nigerian states and the Federal Capital Territory).

### Core Methodological Features
* **Multi-Stream Observation Link:** Integrates reported cases, hospital admissions, and mortality counts using a logit-linked observation process mapped via healthcare accessibility indices.
* **Climate-Zone Seasonality:** Incorporates primary annual and secondary semi-annual Fourier harmonic forcing ($A_1, A_2$) mapped across Sahelian, Sudan Savannah, and Guinea Savannah ecological zones.
* **Spatiotemporal Dynamics:** Utilizes spatial random fields and high-dimensional latent process noise ($\dim(\boldsymbol{\theta}) = 5,899$) to capture regional wave propagation fronts.
* **Numerical Stability via Sub-Stepping:** Employs a 7-day daily sub-stepping integration scheme ($\Delta t = 1/7$ days) within discrete-time SEIR transitions.
* **Full Posterior Inference:** Executed via non-centered Hamiltonian Monte Carlo (HMC) sampling using the No-U-Turn Sampler (NUTS) in Stan.

---

## Repository Directory Structure

```text
├── data/                      # Raw surveillance streams, spatial covariates, and healthcare accessibility indices
├── models/                    # Stan model files (.stan) implementing the SEIRH sub-stepping engine
├── scripts/                   # R/Python data preprocessing, MCMC execution, and out-of-sample validation scripts
├── outputs/                   # Generated posterior CSV draw files, convergence metrics, and table summaries
├── figures/                   # Rendered posterior fits, spatial maps, and MCMC trace/pair diagnostic PDFs
└── README.md                  # Project documentation and usage guide


To run the model and reproduce the posterior analyses, ensure you have the following software and R packages installed:R >= 4.2, Stan / CmdStanR (>= 2.32), Core R Packages: tidyverse, cmdstanr, posterior, bayesplot, deSolve, sf. You can install cmdstanr in R via:
install.packages("cmdstanr", repos = c("[https://mc-stan.org/r-packages/](https://mc-stan.org/r-packages/)", getOption("repos")))
cmdstanr::install_cmdstan()


Preprocess Surveillance Data:
Run the data cleaning script to format the 156-week multi-stream inputs for the 20 administrative units:Rsource("scripts/01_data_preprocessing.R")
Execute Stan MCMC Sampling:
Compile and run the hierarchical Bayesian SEIRH model using multiple parallel chains:Rsource("scripts/02_run_stan_model.R")
Generate Diagnostics and Figures:
Inspect convergence metrics ($\hat{R}$, Bulk/Tail ESS) and generate publication figures:Rsource("scripts/03_generate_diagnostics.R")
CitationIf you use code, data, or model structures from this repository in your academic research, please cite our manuscript:Code snippet@article{rabiu2026seirh,
  title={Hierarchical Bayesian SEIRH Modeling of Multi-Stream Epidemic Dynamics in Northern Nigeria: Spatiotemporal Wave Propagation and Climate-Forced Transmission},
  author={Rabiu, Musa},
  journal={Preprint},
  year={2026}
}
LicenseThis project is open-source and licensed under the MIT License.
