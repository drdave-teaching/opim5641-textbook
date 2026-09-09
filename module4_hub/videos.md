# Module 4 Video Guide — Nonlinear & Portfolio

**OPIM 5641 - Business Decision Modeling · Dr. Dave Wanik · University of Connecticut**

Two blocks. **M4.1** bends the world — regression as optimization, and distance-based location problems. **M4.2** is the payoff: Ms. Womack's portfolio, real modern portfolio theory with a quadratic risk term.

:::note
**Recorded 2026-08-11 (M4.1) and 2026-08-17 (M4.2).** Ten videos total, matching HuskyCT. Transcripts and polished scripts live in `opim5641-transcripts/hybrid_fall2026/async5_module4_1/` and `async6_module4_2/`.
:::

## M4.1 — Nonlinear Optimization (6 videos · 41 min)

### Notebook · `7_Nonlinear/Polynomial.ipynb`

**M4.1 · 1 — Polynomial, and what makes a model nonlinear** *(7:51)*
Why nonlinear at all: not every process is a straight line — powers, roots, exponents, stepwise pieces — and if any of those are in your problem, a linear solver won't take it. Sometimes one curve beats a pile of stitched linear pieces. Then **the three rules of this module**: (1) **initialize** your decision variables, and try different starting values — the polynomial example shows the solver settling into a *local* optimum that depends on where it started; (2) **bound** your variables to help convergence; (3) if a linear model will do the job, **use the linear model**.

### Notebook · `7_Nonlinear/Pharmacy - Complete_guided.ipynb`

**M4.1 · 2 — Setting up our first regression** *(8:18)*
Regression as optimization — the bridge to every stats class you've taken. CVS pharmacy staffing: $y = a + bx$, find the $a$ (intercept) and $b$ (slope) that **minimize the sum of squared errors**. Error is a distance; squaring it keeps it positive and punishes outliers. The Pyomo trick: $y$ is a **placeholder decision variable**, one per store.

**M4.1 · 3 — Different flavors of objective function** *(7:48)*
How the placeholder gets its meaning: ten constraints — one per row — each forcing *prediction minus the linear form of the model* to equal zero, with $a$ and $b$ shared across every row. The constraints enforce the model's shape; the objective just sums the squared gaps. Once you see that, swapping the model's form or the error metric is a one-line change.

**M4.1 · 4 — Wrapping up regression as optimization** *(3:37)*
Two more flavors: **absolute error** instead of squared (looks "better" — but careful, the two objectives are in different units and can't be compared directly), and the gloriously overboard **mess of polynomials** — seven power terms hard-coded at once, because when the model is an optimization problem you can try anything. Blue line vs. green line, and Dave still likes the blue.

### Notebooks · `7_Nonlinear/Location Problem_Simple_guided.ipynb` → `Location Problem_Advanced_guided.ipynb`

**M4.1 · 5 — The simple warehouse location problem** *(6:26)*
The classic: a paper company with 10 big-box stores needs a distribution center. **Distance is a square root** — inherently nonlinear — so minimizing total distance to all stores needs a nonlinear solver. Find the centroid; simple version first, business rules later.

**M4.1 · 6 — The weighted warehouse location problem** *(6:39)*
Solve it: total distance **670** with the warehouse at **(114, 35)** — bing, right in the middle. Then the better question: stores aren't equal. Weight each store by its **delivery volume** and watch the warehouse slide toward the store doing 90% of the business. Same model, one weighting, much smarter answer.

## M4.2 — Portfolio Optimization: Ms. Womack (4 videos)

### Notebook · `7_Nonlinear/Portfolio_Allocation_Womack.ipynb`

**M4.2 · 1 — Intro to Ms. Womack** *(4:25)*
The pretend-you're-a-millionaire exercise (the ones where students pay the most attention). You're advising a client who's picked **five stocks in five industries** — computer, chemical, power, auto, electronic — with **two years of monthly returns** each. The data: some average a strong monthly return, some barely beat a savings bond. The question is not "which is best" — it's **how much of each**.

### Notebook · `7_Nonlinear/2_Covariance_and_Correlation.ipynb`

**M4.2 · 2 — Correlation and covariance** *(6:33)*
You can't maximize return *and* minimize risk in one objective — you must pick one and constrain the other. So: maximize return subject to **risk buckets**. But what is risk? The Caribbean parable: **umbrellas and ice cream** both make 10% a year and each loses money in its off-season — hold both and the seasons cancel. That's **negative covariance** doing the work, and it's the heart of modern portfolio theory: the right *pair* is safer than either stock alone.

### Notebook · `7_Nonlinear/Portfolio_Allocation_Womack.ipynb`

**M4.2 · 3 — Building the model and calc_risk** *(7:36)*
The build: decision variables are the **proportions** invested in each stock; the objective is the proportion-weighted average return; proportions sum to one; and **risk = the covariance matrix weighted by the proportions, summed** — for two stocks, all four cells: $Cov(A,A)p_A p_A + Cov(A,B)p_A p_B + Cov(B,A)p_B p_A + Cov(B,B)p_B p_B$. That's `calc_risk`, and it's quadratic — hence the nonlinear solver. (The even-split vs. concentrated comparison lives in the notebook as DEMO 1 and DEMO 2.)

**M4.2 · 4 — First outputs and the frontier** *(5:11)*
Run it in a loop: for each risk cap $r$, constrain risk ≤ $r$, maximize return, store the allocation. Sweep 100 risk levels and the (risk, return) pairs trace the **efficient frontier** — more risk buys more return, with visibly diminishing payoff. Every point is a defensible portfolio; where your client sits on the curve is her call, not the model's. Keep the [methodology figure](https://raw.githubusercontent.com/drdave-teaching/OPIM5641-notebooks/main/figures/womack_methodology.png) open while you watch.

---

*Companions: [skills sheet](skills.md) · [talking points](talking_points.md)*
