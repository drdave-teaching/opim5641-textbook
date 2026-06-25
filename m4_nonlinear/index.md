# Chapter 4 — Nonlinear Optimization

Linear programming is wonderful, but the world isn't always linear. The moment your objective or a constraint contains a **square root, a power, a fraction, or two variables multiplied together**, you've left LP behind and entered **nonlinear programming (NLP)**. This chapter is about modeling those problems — and about the new hazard that comes with them: you can no longer trust that the solver found the *global* best.

## 4.1 What makes a problem nonlinear

A linear expression only multiplies variables by constants and adds them. Anything else is nonlinear:

$$
\underbrace{15c + 24d + 18t}_{\text{linear}} \qquad\text{vs.}\qquad \underbrace{\sqrt{(x-x_i)^2+(y-y_i)^2}}_{\text{nonlinear}},\quad \underbrace{p \cdot q}_{\text{two variables multiplied}}
$$

For these we switch solvers — from CBC (linear) to **Ipopt** (nonlinear). The modeling in Pyomo looks almost identical; you just write the nonlinear expression directly and call the nonlinear solver.

```{admonition} Local vs. global optima — the hill climber in the fog
:class: important
A nonlinear solver is like a **hiker climbing in dense fog**: it can only feel the slope right under its feet, so it walks uphill until every direction goes down — and declares victory. But that peak might be a **local** optimum, not the tallest mountain. Two defenses:
1. **Try several starting points** (initialize the decision variables differently) and confirm you converge to the same answer.
2. **Set sensible bounds** on the variables to keep the solver in the region that makes physical sense.
And remember: when Ipopt says "optimal," it means *locally* optimal — not the global guarantee you got for free in LP. This is the central trade-off of NLP: easier to *model*, harder to *trust*.
```

## 4.2 Facility location — the Euclidean-distance model

The cleanest NLP to start with is **warehouse/facility location**. A paper company ships to stores in 10 metro areas; where do we put one distribution center to **minimize total distance** to all of them? The decision variables are the center's coordinates $(x, y)$; the objective sums the **Euclidean distance** from the center to each store $k$:

$$
\min_{x,y}\; \sum_{k=1}^{10}\sqrt{(x - x_k)^2 + (y - y_k)^2}
$$

That square root is the only nonlinear thing in the whole model — which is exactly why it's the perfect first example.

```python
from pyomo.environ import *

model = ConcreteModel()
model.x = Var()                 # distribution-center coordinates
model.y = Var()
model.dist = Var(range(10), domain=NonNegativeReals)

# each store's distance (note the **0.5 = square root → nonlinear)
model.con = ConstraintList()
for k in range(10):
    model.con.add(model.dist[k] == ((model.x - xk[k])**2 + (model.y - yk[k])**2)**0.5)

model.obj = Objective(expr = sum(model.dist[k] for k in range(10)), sense = minimize)
SolverFactory('ipopt').solve(model)
```

Solve it and the center lands at the **geographic center of mass** of the stores — something you could eyeball in 2-D, but the same model works unchanged in 3-D, 4-D, or any number of dimensions where you *can't* eyeball it. That's the power of writing the model instead of guessing.

## 4.3 The nonlinear business toolkit

The same machinery models a surprising range of decisions — and these are the case studies that make the course click:

- **Portfolio allocation (the Womack example).** Choose weights across assets to **minimize variance** (risk) for a target return. Variance is a *quadratic* form in the weights, so it's inherently nonlinear — the classic Markowitz mean–variance problem, built in Pyomo.
- **Regression as optimization.** Fitting a line is *literally* an optimization: choose coefficients to **minimize the sum of squared errors**. Writing regression as a Pyomo model demystifies what `sklearn` does under the hood.
- **Pricing & revenue (CTC, Campbell).** Revenue is price × demand, and demand is a function of price — so revenue is **price × (a function of price)**, a product of decision-related quantities, hence nonlinear.
- **Inventory (Woodstock EOQ).** Order-cost terms divide a constant by the order quantity $Q$ — a **decision variable in the denominator** — which is nonlinear and needs Ipopt.

```{admonition} The modeler's habit for NLP
:class: tip
Because NLP solutions aren't guaranteed global, build two habits: **(1)** initialize variables to reasonable values and re-solve from a few starting points; **(2)** add **bounds** you can justify from the business (a price can't be negative or absurdly large; an order quantity can't exceed annual demand). Bounds both speed the solver and keep it out of nonsense regions.
```

## Wrap-up

```{admonition} Key takeaways
:class: tip
- A problem is **nonlinear** if it has square roots, powers, fractions, or products of variables — solve it with **Ipopt**, not CBC.
- NLP is **easier to model but harder to trust**: solvers find **local** optima ("hill climber in the fog").
- Defend with **multiple starting points** and **sensible bounds**.
- **Facility location** (minimize Euclidean distance) is the canonical first NLP; the model scales past what you can draw.
- The nonlinear toolkit covers **portfolio variance, regression-as-optimization, price×demand revenue, and EOQ inventory** — all real business decisions.
```


---

## 📌 Lecture key points

*Distilled takeaways from the video lectures behind this chapter — click each to expand.*


:::{admonition} Introduction to Nonlinear Programming
:class: note dropdown
- Nonlinear = objective/constraints with powers, fractions, sqrt, or **products of variables**.
- **Easier to model** (no linearity restriction) but **harder to solve**.
- **No global guarantee** — solvers may return a local optimum.
- **Initialize** decision variables and re-solve from several starting points.
- Prefer **linear** whenever you can; use nonlinear when you must.
:::

:::{admonition} Local Optimum vs Global Optimum
:class: note dropdown
- A nonlinear solver is a **"hill climber in the fog"** — only feels the local slope.
- It may stop at a **local** peak, not the global one.
- Defense: **multiple starting points** + sensible **bounds**.
- Don't trust "optimal" from a nonlinear solver as a global guarantee.
- Visualized on a multi-peak polynomial surface.
:::

:::{admonition} Facility Location Model (Simple) — Parts 1–2
:class: note dropdown
- Decision variables = the center's **(x, y)**; objective = total **Euclidean distance** (the sqrt → nonlinear).
- Solver = **Ipopt** (not the linear CBC).
- Compute pairwise distances with a loop + a `dist` variable per store; sum them.
- Optimum = the **geographic center of mass**; the model scales past what you can eyeball (3-D, 4-D…).
- Square root = raising to the **0.5 power**.
:::

:::{admonition} Model — Advertising Budget
:class: note dropdown
- Maximize **profit = revenue − cost** across 4 quarters (16 decision variables).
- **Seasonal factors** (0.9/1.1/0.8/1.2) change demand by quarter.
- Decompose into revenue and cost components → objective writes itself.
- Budget constraint: total spend ≤ \$40,000.
- Overhead = 15% of revenue; unit cost × units; fixed sales expense.
:::

:::{admonition} Incorporation of a Lower Bound
:class: note dropdown
- Adding a constraint (≥ \$8k/quarter) **shrinks** the feasible set → objective gets **worse**.
- If a configuration were attractive, the freer model would've picked it already.
- Use **`setlb`/`setub`** to set bounds; tip: a clear **upper bound** = the total budget.
- Re-solve from different starts; Ipopt "optimal" isn't a global guarantee.
- Bounds both help the solver and keep it in sensible regions.
:::

:::{admonition} CTC (Coastal Telephone) — Description & Solution
:class: note dropdown
- Choose **day/evening prices** to **maximize revenue**; demand is a function of prices.
- **Nonlinear** because revenue = price × demand (two decision-related quantities multiplied) → **Ipopt**.
- Watch units: demand is **per minute** × minutes (10h day / 14h evening × 60).
- Part 2 adds a constraint (**day ≥ evening + 2¢**) for a more *reasonable* solution.
- Set lower/upper price bounds from tacit business knowledge.
:::

:::{admonition} Campbell (Campo Motors) — Description
:class: note dropdown
- Set **truck/wagon prices** to **maximize profit**; demand depends on price.
- **Nonlinear** (demand × price); needs Ipopt.
- Preparation-time constraint (3h truck, 2h wagon, ≤ 250h) — like an LP resource limit.
- Careful with **bounds**: price ≥ cost, demand ≥ 0.
- Bounds help the solver and rule out nonsense.
:::

:::{admonition} Woodstock (EOQ Inventory) — Description & Solution
:class: note dropdown
- Choose **order quantity Q** per product to minimize ordering + inventory cost.
- **Nonlinear** because **Q is in the denominator** (D/Q orders) → Ipopt.
- Average inventory ≈ **Q/2**; carrying cost h = % × purchase cost.
- Shared **warehouse-capacity** constraint ties the four products together.
- Separate model/data, name variables to match the problem (K, h…), print the model to debug.
:::
