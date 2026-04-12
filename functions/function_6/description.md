## Function 6

### Initial Observations

The function has five input dimensions, with 20 initial (X,y) observations.
Function 6 initially produced negative objective values tightly clustered around approximately −1, with no clear global structure or identifiable regions of high performance.

### Observed Behaviour

Following a limited number of exploratory evaluations, a broader region of the input space was identified in which objective values were closer to zero, suggesting weak global structure and limited exploitable gradients in the early stage of optimisation.

### Effective Optimisation Choices

Maximisation of the marginal log-likelihood (MLL) over the full input domain did not yield a clearly dominant kernel configuration, likely due to the limited number of observations (20 initially, 32 prior to the final submission) and sparse coverage of the input space. For this reason, MLL-based selection was treated as indicative rather than decisive in this case.

Initially, a relatively smooth prior was adopted using a Matérn kernel with smoothness parameter ν=2.5. However, nearest-neighbour analysis in later iterations revealed increased local variability, with relatively large changes in objective value over small normalised distances, indicating moderate non-smooth behaviour.

| obj. value (y) | distance (norm.) | slope |
|:--------------:|:----------------:|:-----:|
| -0.1810 | 0.0579 | 178.1225 |
| -0.2295 | 0.1403 | 75.5416 |
| -0.2630 | 0.1408 | 76.6092 |
| -0.2144 | 0.1467 | 71.6597 |
| -0.2374 | 0.1732 | 61.4584 | 

Based on this empirical evidence, the kernel smoothness was reduced to ν=1.5, providing a better balance between flexibility and smoothness and improving the surrogate model’s ability to capture local variation.

### Best Observed Solution
```
y: 0.020466
X: 0.432845-0.352953-0.692657-0.755685-0.061697
```
<br>

<p align="center">
  <img src="diagnostics/obj_values6.PNG" width="600">
</p>

<em>Figure 1: Objective values (initial vs predicted samples), showing the trajectory of evaluations during the optimisation process.</em>
