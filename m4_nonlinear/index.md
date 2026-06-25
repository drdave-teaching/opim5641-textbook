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
