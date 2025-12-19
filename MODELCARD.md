## Model Card: Hybrid Sequential Model-Based Optimization (SMBO) Framework
1. Overview
•	Name: Hybrid SMBO Strategy for Black Box Optimization
•	Type: Bayesian Optimization using Gaussian Processes
•	Version: v1.10 (Week 10 Iteration – Exploitation Phase)
•	Developer: A Sharma
•	Date: September 2025- January 2026
2. Intended Use
•	Primary Tasks: This model is designed for the global optimization of expensive-to-evaluate "black box" functions where gradients are unavailable. It is specifically tuned for scenarios with low query budgets (<100 evaluations) and high dimensionality (up to 8D).
•	Suitable Use Cases:
o	Hyperparameter tuning of Machine Learning models (e.g., Learning Rate, Dropout).
o	Experimental design in physical sciences (e.g., drug discovery compounds, chemical yields).
o	Supply chain or logistics parameter tuning (e.g., warehouse placement).
•	Out-of-Scope / Inappropriate Uses:
o	Real-time or high-frequency decision making (due to computational overhead of fitting GPs).
o	Convex optimization problems (where Gradient Descent is far more efficient).
o	Functions with extremely high dimensionality (>20D) without prior dimensionality reduction.
o	Highly non-stationary environments where the optimal solution drifts significantly over time.
3. Approach Details
The strategy employs a dynamic, multi-stage approach that evolves over the 13-week optimization lifecycle.
•	Techniques Used:
o	Surrogate Model: Gaussian Process (GP) Regression.
o	Kernels: Matern 5/2 (general purpose), RBF (smooth functions), and WhiteKernel (noise handling). Automatic Relevance Determination (ARD) is used to determine feature sensitivity.
o	Acquisition Functions: A portfolio approach including Upper Confidence Bound (UCB) and Expected Improvement (EI).
•	Evolution of Strategy:
o	Phase 1 (Weeks 1–5): Exploration. High-variance sampling using Latin Hypercube Sampling (LHS) and UCB with high kappa values to map the global landscape and identify basins of attraction.
o	Phase 2 (Weeks 6–9): Transition. Shift to Expected Improvement (EI) to balance exploring new areas with refining known good regions.
o	Phase 3 (Weeks 10–13): Exploitation. Implementation of Trust Region Optimization. The search space is artificially restricted to small hypercubes cantered on the best-known solutions. Boundary constraints are locked for variables identified as monotonic, effectively reducing the dimensionality of the search.
4. Performance
Performance is measured by Simple Regret (the difference between the best output found so far and the theoretical maximum). Since the true maximum is unknown, we track the Best Observed Value.
•	F1 (2D): Stalled. Function appears to be a "needle-in-a-haystack" or flat plateau. Outputs are approx 0.
•	F2 (2D): Strong. Identified a high-performing region (X_1 approx 0.7), successfully managing significant stochastic noise.
•	F3 (3D): Excellent. Successfully bracketed the global maximum.
•	F4 (4D): Strong. Identified two competing peaks; current strategy involves interpolating between them.
•	F5 (4D): Near-Optimal. Identified that the solution lies on the boundaries (0.0/1.0) for 3 out of 4 dimensions.
•	F6 (5D): Good. Located a sensitive basin of attraction; currently performing gradient-like descent.
•	F7 (6D): Strong. Achieved new records by identifying dimension sparsity (X_1 pinned to 0).
•	F8 (8D): Moderate. Progress hindered by high dimensionality and sparsity, but a valid local optimum has been secured.
5. Assumptions and Limitations
•	Key Assumptions:
o	Local Smoothness: The approach assumes the functions are Lipschitz continuous (small input changes = small output changes). It struggles with discontinuous "cliffs."
o	Stationarity: It assumes the function logic does not change between weeks.
•	Limitations:
o	The Trap of Local Optima: The current "Trust Region" strategy explicitly prevents the model from discovering better peaks if they lie far from the current best point.
o	Boundary Bias: The strategy assumes that if a variable improves as it approaches 1.0, the optimum is at 1.0. If the peak is at 0.99, the model may overshoot.
o	Computational Scaling: The computational cost of the GP scales cubically (N^3); while fine for this challenge, it does not scale to thousands of data points.
6. Ethical Considerations
•	Transparency: All decision logic, code, and data logs are maintained in open Jupyter Notebooks to ensure the process is auditable.
•	Reproducibility: Random seeds (random_state=42) are used in optimizers to ensure that another researcher running the same code would derive the same query suggestions.
•	Resource Efficiency: By prioritizing sample efficiency (minimizing queries), this approach reduces the computational or physical waste associated with trial-and-error testing in real-world applications.

