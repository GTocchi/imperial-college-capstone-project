# Imperial College Capstone Project: Black-Box Optimisation (BBO)

## Project Overview
This repository contains my work for the **Black-Box Optimisation (BBO) Capstone Project**, completed as part of the **Imperial College Professional Certificate in Machine Learning and AI**.  

The challenge focuses on optimising a set of **unknown functions under strict query constraints and few observations**, where no information about the functional form, gradients or noise structure is available. The core objective is to **design a data-efficient query strategy** that balances exploration and exploitation to identify high-performing inputs with as few evaluations as possible.  

This mirrors many real-world ML problems where experiments are expensive, slow, or irreversible — e.g., hyperparameter tuning, engineering design, and scientific experimentation. The project strengthened my understanding of **surrogate modelling, acquisition strategies, and iterative model refinement**, skills that are directly applicable to optimisation and experimentation in industry.

---

## Problem Setting

### Inputs
- The system exposes **8 unknown objective functions**, each with a different input dimensionality.  
- Inputs are **real-valued vectors** constrained [0,1]
- The dimensionality varies by function (from 2 to 8).  
- Queries must be submitted in a **strict formatted string**, with each value rounded to six decimal places:

**Example submission:**  
0.413287-0.928104-0.175602

### Outputs
- Each query returns a **scalar performance value**, rounded to six decimal places.  
- The objective function is **unknown** and treated as a black box.  
- Observations may include **noise** and are revealed only after submission.

---

## Repository Structure
- `model_card/` — Documentation describing model assumptions and limitations.  
- `datasheet/` — Data documentation for reproducibility and transparency.  
- *(Future additions)*: Code notebooks, scripts, and examples for submitting queries, surrogate modelling, and acquisition strategies.

---

## Key Skills Demonstrated
- Data‑efficient decision‑making under uncertainty
- Surrogate modelling with Gaussian Processes
- Exploration vs. exploitation trade‑offs
- Hyperparameter sensitivity analysis
- Applied optimisation in constrained, low‑data regimes

---

## Approach
The BBO problem was tackled using a **surrogate-based optimisation framework**. The workflow included:

1. **Surrogate Modelling**: A Gaussian Process (GP) surrogate was fitted to approximate the unknown objective function using observed query–evaluation pairs.
2. **Acquisition Strategy**: New query points were selected by balancing:
  - Exploration: reducing uncertainty about the function, and
  - Exploitation: querying points likely to improve upon the current best observation.
4. **Iterative Refinement**: Updating the surrogate model with new observations and repeating the acquisition cycle until query budget was exhausted.

This approach allows efficient identification of high-performing inputs with minimal queries, mimicking real-world scenarios such as hyperparameter tuning or engineering design optimization.

---

## Data Preprocessing
All input variables were provided natively within the unit hypercube [0,1]^d and therefore required no further rescaling. 
Output observations were standardised to zero mean and unit variance prior to fitting the Gaussian Process surrogate. This standardisation improved numerical stability and ensured well‑behaved kernel hyperparameter estimation under severe data sparsity.

---

## Key Design Insight: Local Geometry Matters
A **central challenge** in this project was accurately modelling sharp or highly localised maxima under severe data sparsity.
In standard Gaussian Process modelling, the Matérn smoothness parameter ν is typically tuned by maximising the marginal log‑likelihood, often **restricted to a neighbourhood around the current maximum** to ensure local relevance. 

However, in this project such localised likelihood optimisation was not feasible due to the **very limited number of observations** near candidate optima. As a result, log‑likelihood maximisation had to be performed over the entire input domain.

In situations where the objective function is largely flat but contains a small, extremely sharp spike, global likelihood optimisation tends to favour overly smooth priors (e.g. high‑ν Matérn or RBF kernels). While these kernels explain the global structure well, they fail to capture the local geometry near narrow maxima, which is precisely the **region of greatest interest for optimisation**.

To address this issue, I adopted a local, **geometry‑informed strategy** for selecting ν, independent of global likelihood maximisation.
Slopes between the current maximum and its k nearest neighbours were computed as differences in output value divided by Euclidean distance. Distances were rescaled by a dimension‑dependent factor to ensure slope magnitudes were comparable across input dimensionalities d, thereby highlighting curvature signals arising from very small neighbourhoods around the maximum.

$$
s_i = \frac{|y_{\max} - y_k|}{\|x_k - x_{\max}\| / \sqrt{d}}
$$

The **key intuition** is that normalised distances from the current max reveal how much information is expressed by local slopes:

  - **Extremely large** slopes at very small distances indicate sharp spikes, favouring lower ν (rougher sample paths),
  - **Moderate slopes** at small distances indicate locally rough but smoother behaviour, favouring higher ν,
  - When **insufficient** nearby observations were available, ν was set to a standard smoothness value (ν = 2.5) to avoid overfitting sparse local structure.

When strong local variation was observed near the maximum, the suggestions obtained by maximizing the log‑likelihood were manually overridden in favour of rougher Matérn kernels (e.g. ν = 0.5), which are better suited to modelling narrow, high‑curvature peaks.
This local ν‑selection strategy proved particularly important in later optimisation rounds, where a higher density of points near the current maxima was available and the strategy shifted toward more aggressive exploitation; in this phase, accurately modelling local structure around candidate optima was more critical than achieving a good global fit.

---

## Example Data
**Sample input for an 8-dimensional function (`X`) and output (`y`):**  
```text
X = [0.665889, 0.123911, 0.877752, 0.778601, 0.142700, 0.349055, 0.845223, 0.711136]
y = 64.443444
