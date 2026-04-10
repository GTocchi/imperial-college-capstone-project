## Function 4

### Initial Observations
The function has four input dimensions, with 30 initial (x,y) observations.
Initial evaluations exhibit a wide dispersion of predominantly negative objective values, spanning a broad range with no immediately discernible structure.

### Observed Behaviour
After a small number of exploratory evaluations, a relatively large central region of the four‑dimensional input space was identified, characterised by objective values close to zero.
Following this discovery, the optimisation strategy was adapted to focus exploration within the identified subspace.

### Effective Optimisation Choices
Maximisation of the marginal log‑likelihood (MLL) over the full input domain throughout the submissions consistently favoured non‑smooth kernels, with a Matérn kernel of smoothness parameter ν=1.5.

To assess local structure, a nearest‑neighbour analysis around the incumbent maximum was performed once a sufficient number of samples had been collected within small normalised distances.
This analysis revealed extremely large local slopes, strongly indicating the presence of sharp curvature:

| obj. value (y)      | distance (norm.) | slope |
|:---------:|:---------------:|:-----:|
| 0.4904 | 0.0194 | 279.5676 |
| 0.5265 | 0.0240 | 216.1015 |
| 0.3109 | 0.0305 | 216.1646 |
| -0.1935 | 0.0450  | 219.9192 |
| 0.2320 | 0.0481 |  148.0482 |

Based on this empirical evidence, the Matérn smoothness parameter was deliberately reduced to a rougher configuration (ν = 0.5).

### Best Observed Solution
```
y: 0.578296
X: 0.170347-0.756959-0.276520-0.531232
```

<p align="center">
  <img src="diagnostics/visualization_final.PNG" width="400">
</p>
<em>Figure 2: Final evaluations localised a narrow spike surrounded by an otherwise flat objective region.</em>
