# Module 4 Skills Sheet — Nonlinear & Portfolio

**OPIM 5641 - Business Decision Modeling · Dr. Dave Wanik · University of Connecticut**

After the M4.1 and M4.2 videos and notebooks, these are the skills you own.

---

## 🌀 Nonlinear fundamentals
*Notebook: `7_Nonlinear/Polynomial.ipynb`*

- ☐ Say what makes a model nonlinear — a power, root, exponent, or stepwise term anywhere in it — and why a linear solver won't accept it
- ☐ Recite the three rules: **initialize** decision variables (and try several starts), **bound** them where you can, and **prefer linear when linear works**
- ☐ Explain **local vs. global optima**, and show how changing the initialization changes which optimum the solver finds
- ☐ Treat a solver's confident answer with appropriate suspicion — re-run from different starting points before you believe it

## 📉 Regression as optimization
*Notebooks: `Pharmacy - Complete_guided.ipynb` (+ blank) · `General Framework_Regression in Pyomo.ipynb`*

- ☐ Cast $y = a + bx$ as an optimization problem: decision variables $a, b$, objective = sum of squared errors
- ☐ Use the **placeholder pattern**: a prediction variable per row, pinned to the model's form by one constraint per row
- ☐ Explain why error is squared (always positive, punishes outliers) and what changes with absolute error
- ☐ Never compare objective values across different error metrics — different units
- ☐ Swap in a different functional form (powers, roots) and let the solver fit it — and say when that's overboard

## 📦 Location problems
*Notebooks: `Location Problem_Simple_guided.ipynb` (+ blank) · `Location Problem_Advanced_guided.ipynb`*

- ☐ Explain why distance makes a problem nonlinear (square root of coordinate differences)
- ☐ Set up the centroid problem: minimize the sum of distances from one point to many
- ☐ Weight the objective by demand (deliveries per store) and interpret how the answer moves
- ☐ Sanity-check a location answer on a plot — the purple dot should sit where your eyes expect it

## 💼 Portfolio optimization (Ms. Womack)
*Notebooks: `2_Covariance_and_Correlation.ipynb` · `Portfolio_Allocation_Womack.ipynb`*

- ☐ Explain covariance with umbrellas and ice cream — and why a negatively-correlated pair is safer than either alone
- ☐ State why you can't maximize return and minimize risk in one objective — and what to do instead (maximize return under a **risk cap**)
- ☐ Define the decision variables (proportions), the sum-to-one constraint, and the beat-the-savings-bond floor
- ☐ Compute portfolio risk as the proportion-weighted covariance matrix, summed — write out all four terms for two stocks
- ☐ Explain what `calc_risk` does cell by cell (the [figure](https://raw.githubusercontent.com/drdave-teaching/OPIM5641-notebooks/main/figures/calc_risk_two_stocks.png) is the check)
- ☐ Sweep risk caps in a loop and plot the **efficient frontier**
- ☐ Read the frontier like an advisor: every point is defensible; the client picks the risk, the model picks the allocation

---

## The one-sentence version

> **You can fit a curve, place a warehouse, and build a real Markowitz portfolio — because you can write any of them as decision variables, an objective, and constraints, and you know the extra care a nonlinear solver demands.**

Next stop: **integer programming** — from "how much" to "do we or don't we."
