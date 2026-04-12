## Function 7

### Initial Observations

The function has six input dimensions, with 30 initial (X,y) observations.
Function 7 objective values are all positive, with an average value of approximately 0.2 and no immediately clear global structure or consistently high-performing regions. One notable exception was an isolated observation with objective value 1.36.

### Observed Behaviour

Right after the first evaluation, a broader region of the input space was identified in which objective values consistently exceeded the initial incumbent maximum. This indicated that the early high-performing observation was not isolated, but instead located within a wider promising basin suitable for further (balanced) exploitation.

### Effective Optimisation Choices

Maximisation of the marginal log-likelihood (MLL) over the full input domain showed a preference for a nu of 1.5 or 2.5. However, the limited number of observations (20 initially, 32 prior to the final submission) and sparse coverage of the input space MLL-based selection was treated as indicative rather than decisive in this case.
Nearest-neighbour analysis proved more useful in this case, as a single promising region was identified early and repeatedly sampled throughout the optimisation process. This provided multiple nearby observations around the incumbent maximum, enabling a clearer assessment of local function behaviour.

| obj. value (y) | distance (norm.) | slope |
|:--------------:|:----------------:|:-----:|
| 3.1142 | 0.0339 | 236.6729 |
| 3.0906 | 0.0418 | 187.8700 |
| 3.0363 | 0.0651 | 115.2543 |
| 3.0225 | 0.0743 | 99.7142 |
| 2.9804 | 0.0869 | 82.0827 |

The consistently large local slopes over relatively small normalised distances indicated sharp local variation and behaviour more consistent with a rougher surrogate prior. Based on this evidence, the kernel smoothness parameter was reduced to ν=0.5, improving the model’s responsiveness to local structure. This adjustment was followed by a sustained sequence of improved objective values across successive submissions.

### Best Observed Solution
```
y: 3.149521
X: 0.221626-0.141333-0.317596-0.293670-0.307649-0.654382
```
<br>

<p align="center">
  <img src="diagnostics/obj_values7.PNG" width="600">
</p>

<em>Figure 1: Objective values (initial vs predicted samples), showing the trajectory of evaluations during the optimisation process.</em>
