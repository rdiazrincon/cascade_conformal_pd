# CASCADE Conformal Prediction

**Official Implementation of: *"CASCADE Conformal Prediction: Uncertainty-Adaptive Prediction Intervals for Two-Stage Clinical Decision Support"* (Diaz-Rincon et al., 2026)**

This repository contains the code for applying CASCADE (Calibrated Adaptive Scaling via Conformal And Distributional Estimation) to Parkinson's Disease medication management. 

We utilize the **LEDD (Levodopa Equivalent Daily Dose)** as a standardized metric to measure the medication requirements for a Parkinson's Disease patient.

## Overview
High-stakes clinical workflows often follow a hierarchical, two-stage logic: 
1. **Classification:** Is an intervention needed?
2. **Regression:** What is the correct dose?

Standard AI pipelines treat these stages independently, creating an "uncertainty silo" where the epistemic ambiguity of the initial triage is lost. **CASCADE** solves this by preventing information loss at the decision boundary, propagating Stage 1 epistemic uncertainty directly into Stage 2 to formulate dynamically scaled Conformal Prediction (CP) intervals.

## The CASCADE Effect
Our approach calculates the patient's epistemic uncertainty in Stage 1 through **Venn-Abers (VA)** calibration. The length of the VA multi-probabilistic interval ($u_{VA}$) acts as a highly discriminative uncertainty score to inform and scale Stage 2 Conformal Prediction intervals.

* **Low Uncertainty (Confident Stage 1):** Stage 2 provides narrow, precise dosage intervals for stable patients.
* **High Uncertainty (Cautious Stage 1):** Stage 2 provides wide intervals. For highly atypical, error-prone patients, the intervals expand drastically, acting as a "safety buffer" that safely flags the patient for careful manual titration and clinician review.

## Implemented Strategies
This notebook implements and evaluates three conformal strategies for two-stage pipelines:

1. **Baseline (Standard CP):** Standard marginal conformal prediction that does not utilize Stage 1 uncertainty information.
2. **Mondrian (VA-Stratified):** Discretizes uncertainty into bins to create separate conformal predictors for each uncertainty category.
3. **Continuous CASCADE:** Our proposed method. Uses a continuous scalar based on $u_{VA}$ to dynamically scale the bounds, achieving precise marginal validity without unnecessary inflation.

## Clinical Benefits
* **Unified Uncertainty Propagation:** The first framework to explicitly carry epistemic uncertainty across a multi-stage clinical task.
* **Adaptive Safety Nets:** Translates extreme Stage 1 ambiguity into massive, non-actionable prediction intervals to prevent unsafe automated titrations.
* **Clinical Interpretability:** Clinicians are provided with both triage confidence and continuous dose prediction bounds simultaneously.

## Data Privacy & Reproducibility
Due to the sensitive nature of clinical Electronic Health Records (EHR) and institutional IRB constraints, the real Parkinson's Disease patient dataset cannot be publicly shared in this repository.
