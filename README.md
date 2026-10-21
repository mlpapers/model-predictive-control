# Model Predictive Control

## Receding-horizon control and guarantees

- **[Constrained MPC](https://experts.illinois.edu/en/publications/constrained-model-predictive-control-stability-and-optimality/)** — 2000. Mayne et al. study repeated finite-horizon optimization: apply the first control, observe the new state and replan. State/input constraints, recursive feasibility and closed-loop stability are central design questions.
- **[Terminal ingredients](https://sites.engineering.ucsb.edu/~jbraw/mpc/MPC-book-2nd-edition-1st-printing.pdf)** — 2017. Terminal costs, terminal sets and local controllers can establish feasibility and stability under stated assumptions. Merely solving a finite-horizon problem does not supply these guarantees.
- **[State estimation](https://sites.engineering.ucsb.edu/~jbraw/mpc/MPC-book-2nd-edition-1st-printing.pdf)** — 2017. Output-feedback MPC acts on estimated states. Moving-horizon estimation fits recent measurements under dynamics and constraints; estimation error must enter the closed-loop analysis.
- **[Economic MPC](https://sites.engineering.ucsb.edu/~jbraw/mpc/MPC-book-2nd-edition-1st-printing.pdf)** — 2017. Optimizes an operating objective directly instead of only tracking a setpoint. Closed-loop economic performance and stability require their own analysis; a cheaper predicted trajectory is not a universal stability certificate.

## Uncertainty and explicit control

- **[Explicit MPC](https://cse.lab.imtlucca.it/~bemporad/publications/papers/automatica-mpqp.pdf)** — 2002. Bemporad et al. compute constrained linear-quadratic feedback offline as a continuous piecewise-affine law. Online optimization becomes region lookup and evaluation; the partition must be stored.
- **[Real-time iteration](https://epubs.siam.org/doi/abs/10.1137/S0363012902400713)** — 2005. Diehl et al. interleave Newton-type optimization with feedback, refining approximate solutions as the plant evolves. Contractivity and suboptimality bounds justify this local scheme; control updates need not solve the nonlinear problem to convergence.
- **[Tube-based robust MPC](https://www.sciencedirect.com/science/article/pii/S0005109804002870)** — 2005. Mayne et al. control constrained linear systems with bounded disturbances using a nominal trajectory and invariant error set. Robust stability is established for the disturbance-invariant set under their assumptions.
- **[Stochastic MPC](https://www.merl.com/publications/docs/TR2017-217.pdf)** — 2017/2018. Uses disturbance distributions to optimize expected performance and impose probabilistic constraints. Chance constraints permit specified violation probabilities; they differ from worst-case bounds for every admissible disturbance.
- **[Scenario-based constraints](https://marco-campi.unibs.it/pdf-pszip/IEEE-TAC-scenario.pdf)** — 2006. Samples uncertain convex constraints to form a finite problem. Calafiore and Campi bound violation probability under independent sampling; this risk/confidence guarantee does not establish safety over an entire control trajectory.
- **[MPPI / information-theoretic MPC](https://arxiv.org/abs/1707.02342)** — 2017. Williams et al. derive sampling-based control updates from an information-theoretic objective and test autonomous driving. Sampling evaluates candidate trajectories without requiring a differentiable optimizer.

## Learning dynamics, costs and feasible behavior

- **[Learning-based MPC](https://www.annualreviews.org/content/journals/10.1146/annurev-control-090419-075625)** — 2019/2020. Hewing et al. distinguish learning prediction models, learning controller components and using MPC to constrain learning. Model accuracy, uncertainty and closed-loop guarantees are separate parts of the design.
- **[Learning MPC for iterative tasks](https://arxiv.org/abs/1609.01387)** — 2016. Rosolia and Borrelli build terminal sets and costs from previous successful trajectories. Their construction gives recursive feasibility and non-increasing iteration cost under the stated iterative-task assumptions.
- **[Koopman MPC](https://arxiv.org/abs/1611.03537)** — 2016. Lifts observations into a feature space and fits approximately linear controlled dynamics by least squares. Linear MPC can then optimize nonlinear-system predictions; the finite lifting determines approximation quality.
- **[Cautious GP-MPC](https://arxiv.org/abs/1705.10702)** — 2017. Adds a Gaussian-process residual to nominal dynamics and propagates approximate state uncertainty into chance constraints. Hewing et al. test racing hardware; the uncertainty approximation is part of the controller, not just a prediction interval.
- **[PETS](https://arxiv.org/abs/1805.12114)** — 2018. Combines probabilistic dynamics ensembles with trajectory sampling to plan under model uncertainty. Chua et al. report strong sample efficiency on studied control tasks; uncertainty-aware planning alone does not enforce state constraints.
- **[Differentiable MPC](https://arxiv.org/abs/1810.13400)** — 2018. Amos et al. differentiate through the controller’s convex approximation at a fixed point to learn costs and dynamics. The gradient construction depends on that solution structure, not arbitrary differentiation through any solver.
- **[DeePC](https://arxiv.org/abs/1811.05890)** — 2018. Predicts trajectories directly from recorded input/output data. Coulson et al. establish equivalence to MPC for deterministic linear time-invariant systems with suitable data; noisy nonlinear extensions use regularization.
- **[Distributionally robust DeePC](https://arxiv.org/abs/1903.06804)** — 2019. Coulson et al. relate regularization to worst-case expected cost over distributional uncertainty for stochastic linear systems. The equivalence holds for specified costs; it supplies a rationale for regularization under noisy trajectory data.
- **[Stable data-driven MPC](https://arxiv.org/abs/1906.04679)** — 2019. Berberich et al. add terminal equalities and regularized slack for noisy LTI data. Their multi-step scheme has practical exponential stability with persistently exciting data and small bounded output noise.
- **[Bayesian MPC](https://proceedings.mlr.press/v120/wabersich20a.html)** — 2020. Wabersich and Zeilinger use posterior sampling to trade exploitation against model exploration and derive finite-time regret bounds under assumptions. Learning performance and constraint satisfaction remain distinct criteria.
- **[Predictive safety filters](https://arxiv.org/abs/1812.05506)** — 2018. Check a proposed action against a model-based backup plan and modify it when needed. Wabersich and Zeilinger’s safety argument depends on uncertainty bounds and feasible recovery, not on the upstream policy alone.
- **[Control-barrier-function filters](https://arxiv.org/abs/1609.06408)** — 2016/2017. Enforces inequalities in the control input to keep a specified state set forward invariant. Ames et al. combine barrier and Lyapunov conditions in a quadratic program; feasibility and model assumptions are part of the safety claim.
- **[Learning an MPC approximation](https://arxiv.org/abs/1806.04167)** — 2018. Hertneck et al. imitate a robust MPC law, then use statistical validation of approximation error to support closed-loop guarantees. The robust design tolerates bounded action errors; low average imitation loss alone is insufficient.

## Latent planning and comparative evidence

- **[TD-MPC](https://arxiv.org/abs/2203.04955)** — 2022. Learns task-oriented latent dynamics and a terminal value function jointly by temporal-difference learning. Short-horizon planning uses the value estimate for longer-term return; no observation reconstruction is required.
- **[TD-MPC2](https://arxiv.org/abs/2310.16828)** — 2023. Extends latent MPC and reports strong results across 104 tasks with one hyperparameter set. Its multi-task scaling experiments assess control return; these benchmarks do not certify physical constraint satisfaction.
- **[MPC–RL combinations](https://publications.syscop.de/Reiter2026.pdf)** — 2026 survey. Reiter et al. distinguish MPC as an expert for training, as part of the deployed policy, or as part of the critic. This separates learning from planned demonstrations, learning a controller’s parameters and learning value estimates.
- **[Control evaluation](https://www.annualreviews.org/content/journals/10.1146/annurev-control-090419-075625)**. Report closed-loop cost, constraint violations, failures and solve-time distribution under model error. Compare identical observation access and planning budgets; prediction error alone does not measure controller quality.

## Software and references

- **[acados](https://arxiv.org/abs/1910.13753)** — 2019. Modular C solvers for embedded optimal control, with Python/Matlab interfaces and CasADi-compatible models. Solver choice, tolerances and target hardware determine measured latency.
- **[do-mpc](https://www.do-mpc.com/en/latest/)**. Python tools for nonlinear/economic MPC, robust multi-stage MPC and moving-horizon estimation. Includes simulation and differential-algebraic models; the toolbox supplies implementations, not automatic safety certification.

## Related topics

[Reinforcement learning](https://mlpapers.org/reinforcement-learning/) · [Optimization](https://mlpapers.org/optimization/) · [Symbolic regression](https://mlpapers.org/symbolic-regression/) · [Meta-learning](https://mlpapers.org/meta-learning/) · [Bayesian inference](https://mlpapers.org/bayesian-inference/) · [Evaluation](https://mlpapers.org/evaluation/).
