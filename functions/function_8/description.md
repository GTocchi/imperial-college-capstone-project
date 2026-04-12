## Function 8

### Initial Observations

The function has 8 input dimensions, with 40 initial (X,y) observations.
Initial objective values were all positive and tightly concentrated around an average value of approximately 7, with no immediately clear global structure or consistently superior regions of the search space.

### Observed Behaviour

The absence of clearly promising regions or sharp local maxima favoured a prolonged exploratory strategy. Throughout much of the optimisation process, no pronounced spikes in objective value were observed, suggesting that the underlying objective function was relatively smooth.
As a result, this function was explored more extensively than the others, with exploitation deferred until the final stages. Furthermore, many subsequently evaluated points produced values just below 10, indicating that strong local exploitation was unlikely to provide substantial gains over continued global search.

### Effective Optimisation Choices

Maximisation of the marginal log-likelihood (MLL) over the full input domain showed a clear preference for a Radial Basis Function (RBF) kernel, reinforcing the smooth behaviour already suggested by the observed optimisation trajectory.
Nearest-neighbour analysis was less informative in this case, as no evaluated points were located particularly close to the incumbent maximum under the normalised distance metric (the closest normalized distance is 0.3177). This further supported the decision to maintain an exploratory search policy for most of the optimisation process.

Finally, the presence of multiple high-performing observations near the incumbent maximum, combined with relatively consistent slopes over larger normalised distances, suggested a broad and smoothly varying optimum region rather than a narrow sharp peak. This provided further support for retaining an RBF kernel.

### Best Observed Solution
```
y: 9.975787
X: 0.091375-0.094036-0.069340-0.092904-0.890601-0.482209-0.232975-0.580419
```
<br>

<p align="center">
  <img src="diagnostics/obj_values8.PNG" width="600">
</p>

<em>Figure 1: Objective values (initial vs predicted samples), showing the trajectory of evaluations during the optimisation process.</em>
