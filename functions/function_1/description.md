## Function 1

### Initial Observations
Function 1 initially appeared extremely flat, with early evaluations yielding objective values close to zero across most of the input domain. This lack of informative variation made it difficult to identify promising regions in the initial stages and required an explicitly exploratory optimisation strategy to locate a meaningful maximum while avoiding noise‑dominated fluctuations.

### Observed Behaviour
The first observation sin the "central" unexplored" area quickly showed a tiny but very high spike in the region.

### Effective Optimisation Choices
This function clearly illustrated the limitations of maximising the marginal log‑likelihood over the entire input domain. Global likelihood optimisation consistently favoured very smooth kernels (RBF‑like behaviour), which captured the largely flat structure of the domain but failed to model the narrow, high‑curvature spike located in the region of greatest optimisation interest.

In contrast, analysis of the nearest observations around the incumbent maximum revealed extremely large local gradients at very small normalised distances, indicating strong local curvature. On this basis, the Matérn smoothness parameter was manually adjusted from an RBF‑equivalent setting to a rougher configuration (ν = 0.5), enabling the surrogate to better represent the sharp peak.

Once the presence and location of the spike had been identified, the optimisation strategy transitioned to a more aggressive exploitation regime by increasing the Expected Improvement focus on local refinement, allowing fine‑scale improvements around the candidate optimum.

### Best Observed Solution

