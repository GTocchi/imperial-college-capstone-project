# Imperial College Capstone Project: Black-Box Optimisation (BBO)

## Project Overview
This repository contains my work for the **Black-Box Optimisation (BBO) Capstone Project**, completed as part of the **Imperial College Professional Certificate in Machine Learning and AI**.  

The challenge focuses on optimising a set of **unknown functions under strict query constraints**, where no information about the functional form, gradients, or noise structure is available. The core objective is to **design a data-efficient query strategy** that balances exploration and exploitation to identify high-performing inputs with as few evaluations as possible.  

This mirrors many real-world ML problems where experiments are expensive, slow, or irreversible — e.g., hyperparameter tuning, engineering design, and scientific experimentation. The project strengthened my understanding of **surrogate modelling, acquisition strategies, and iterative model refinement**, skills that are directly applicable to optimisation and experimentation in industry.

---

## Inputs and Outputs

### Inputs
- The system exposes **8 unknown objective functions**, each with a different input dimensionality.  
- Inputs are **real-valued vectors** constrained to the unit hypercube:

\[
x \in [0,1]^d
\]

- The dimensionality \(d\) varies by function (from 2 to 8).  
- Queries must be submitted in a **strict formatted string**, with each value rounded to six decimal places:

**Example submission:**  
0.413287-0.928104-0.175602

### Outputs
- Each query returns a **scalar performance value**.  
- The objective function is **unknown** and treated as a black box.  
- Observations may include **noise** and are revealed only after submission.

---

## Repository Structure
- `model_card/` — Documentation describing model assumptions and limitations.  
- `datasheet/` — Data documentation for reproducibility and transparency.  
- *(Future additions)*: Code notebooks, scripts, and examples for submitting queries, surrogate modelling, and acquisition strategies.

---

## Key Skills Demonstrated
- Data-efficient decision-making under uncertainty  
- Surrogate modelling and iterative refinement  
- Exploration vs. exploitation strategies  
- Applied machine learning for optimisation tasks

---

## Approach
The BBO problem was tackled using a **surrogate-based optimisation framework**. The workflow included:

1. **Surrogate Modelling**: Fitting a model to approximate the unknown function using observed query data.
2. **Acquisition Strategy**: Selecting new points to query that balance exploration (learning more about the function) and exploitation (choosing points likely to have high performance).
3. **Iterative Refinement**: Updating the surrogate model with new observations and repeating the acquisition cycle until query budget was exhausted.

This approach allows efficient identification of high-performing inputs with minimal queries, mimicking real-world scenarios such as hyperparameter tuning or engineering design optimization.

---

## Example Data
**Sample input for an 8-dimensional function (`X`) and output (`y`):**  
```text
X = [0.665889, 0.123911, 0.877752, 0.778601, 0.142700, 0.349055, 0.845223, 0.711136]
y = 64.443444
