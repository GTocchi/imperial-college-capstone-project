# BBO Capstone Project Dataset

## Identification and Purpose
The **goal of this dataset** is to support experimentation with **black-box optimisation tasks**, specifically aimed at **finding the maxima of unknown functions**, as part of the Imperial College *Artificial Intelligence and AI* Professional Certificate Capstone.  

The dataset enables testing of **Bayesian Optimisation, surrogate models, exploration/exploitation strategies, and hyperparameter tuning**, while also allowing students and researchers to explore **manual adjustments of hyperparameters** guided by **graphical visualisation of the input space and function behaviour**.

This dataset simulates realistic optimisation scenarios, helping users develop and evaluate query strategies and understand the impact of **kernel choice, smoothness (ν), length scales, and output variance** on surrogate predictions.

---

## Dataset Composition
The dataset contains **input vectors (`X`) and corresponding output evaluations (`y`)** collected during BBO experiments across 8 unknown functions.  

**Details:**  
- **Input dimensions:** 2–8 numeric features per point.  
- **Output:** Scalar function evaluation at each query point.  
- **Size:** 20–40 points per function, depending on the function.  
- **Format:** CSV or NumPy arrays; each row corresponds to one query and its evaluated output.  
- **Limitations:** Only a subset of the search space is sampled. Some regions, especially in higher dimensions, remain unexplored, limiting the ability to represent extreme or rare function behaviours. Global hyperparameter tuning was required due to the small number of observations, as restricting tuning to promising regions was not possible.

---

## Collection Process
Queries were generated using **Bayesian Optimisation with Gaussian Process surrogate models (Matérn or RBF kernels)** combined with **manual interventions** when the optimiser stalled.  
Initially, queries were selected using Upper Confidence Bound (UCB) and later transitioned to Expected Improvement (EI) to prioritise points likely to improve the best observed value while accounting for uncertainty.

**Details:**  
- **Hyperparameter tuning:**  
  - **ν (nu)** – Matérn smoothness parameter, optimised via **log-likelihood**, but sometimes manually set (e.g., ν = 0.5) for functions with mostly flat regions and small sharp peaks.  
  - **Kernel choice** – Matérn or RBF; manual override applied in cases where automatic selection was not adequate to capture sharp maxima.  
  - **Length scale (`l`)** – controls correlation between function values; constrained when values became unstable.  
  - **Output variance (`σ`)** – controls overall magnitude of GP; also constrained when necessary.  
- **Query strategy:** Combination of **exploitation of predicted maxima** and **targeted exploration of uncertain or boundary regions**.  
- **Visualization:** Graphical inspection of the input space and function behaviour was crucial to guide manual hyperparameter adjustments.  
- **Time frame:** Iterative rounds of 13 queries per function.  

---

## Preprocessing and Intended Uses
- **Transformations:** Outputs (`y`) were standardised (mean=0, std=1); inputs were scaled to [0,1] across all dimensions.  
- **Intended uses:** Developing, testing, and evaluating **Bayesian Optimisation strategies, surrogate models, and hyperparameter tuning**, especially for **finding maxima of unknown black-box functions**.  
- **Inappropriate uses:**  
  - Large-scale supervised learning with many labeled examples.  
  - Deterministic optimisation with fully known objective functions.  
  - Problems in **high-dimensional spaces**, as no unsupervised methods (e.g., PCA or clustering) were applied prior to Bayesian Optimisation due to small input dimensionality (≤8).  

---

## Example Data
**Sample input (`X`) and output (`y`):**  
```text
X = [0.665889, 0.123911, 0.877752, 0.778601, 0.142700, 0.349055, 0.845223, 0.711136]
y = 64.443444
