# Chapter 3 — Linear Programming in Pyomo & Sensitivity Analysis

Chapter 2 solved LPs by hand. Now we solve them in **Pyomo**, a Python modeling language that lets you write a model that *looks like the math*, hand it to an industrial solver, and get the answer in milliseconds. Then we do the part that separates an analyst from a button-pusher: **sensitivity analysis** — asking what the solution would do if the numbers changed, and what each constraint is actually *worth*.

## 3.1 Building a model in Pyomo

Every Pyomo model has the same four parts you learned in Chapter 1 — variables, objective, constraints, data — written in code. Here's Veerman Furniture, end to end:

```python
from pyomo.environ import *

model = ConcreteModel()

# 1. decision variables (non-negative, continuous)
model.c = Var(domain=NonNegativeReals)   # chairs
model.d = Var(domain=NonNegativeReals)   # desks
model.t = Var(domain=NonNegativeReals)   # tables

# 2. objective — maximize profit
model.profit = Objective(expr = 15*model.c + 24*model.d + 18*model.t, sense = maximize)

# 3. constraints — the rules of reality
model.fabrication = Constraint(expr = 4*model.c + 6*model.d + 2*model.t <= 1850)
model.assembly    = Constraint(expr = 3*model.c + 5*model.d + 7*model.t <= 2400)
model.shipping    = Constraint(expr = 3*model.c + 2*model.d + 4*model.t <= 1500)

# 4. solve
SolverFactory('cbc').solve(model)
model.pprint()
```

Read it top to bottom and it's just the math from Chapter 1, transcribed. `ConcreteModel()` makes the container; `Var(domain=NonNegativeReals)` declares a continuous, non-negative decision; `Objective(..., sense=maximize)` is what we optimize; each `Constraint(expr=...)` is a rule; `SolverFactory('cbc').solve(model)` calls the **CBC** solver. **Name your constraints meaningfully** (`fabrication`, not `Constraint1`) — it pays off enormously when you read the reports below.

```{admonition} The three classic LP shapes
:class: tip
Almost every LP you'll build is a flavor of three patterns:
- **Allocation** — *maximize* an objective subject to **"≤"** resource limits (the furniture problem).
- **Covering** — *minimize* cost subject to **"≥"** requirements (meet a minimum nutrition profile).
- **Blending** — mix inputs to hit target proportions/scores, rewritten algebraically to stay linear.
Spot which pattern a word problem is, and the formulation writes itself.
```

## 3.2 Sensitivity analysis — what are your constraints worth?

Solving the model gives you *a* plan. Sensitivity analysis tells you how *robust* that plan is and where the leverage lies. Two ideas carry the whole topic.

```{admonition} Shadow price & reduced cost
:class: important
A **binding** constraint is one your solution meets *exactly* (left-hand side = right-hand side) — you've used every last fabrication hour. Its **shadow price** is the improvement in the objective for **one more unit** of that constraint's right-hand side:

$$
\text{shadow price} = \frac{\partial(\text{optimal objective})}{\partial(\text{RHS of the constraint})}
$$

If fabrication's shadow price is \$4, then one more fabrication hour is worth \$4 of profit (and one fewer costs \$4). Non-binding constraints have **slack** and a shadow price of **0** — more of a resource you aren't fully using is worthless. The **reduced cost** is the analogous quantity for a decision variable sitting at a bound: how the objective changes if you force that variable up or down.
```

The practical payoff: the shadow prices tell a manager **exactly where to invest**. If fabrication is the only binding constraint and it's worth \$4/hour, that's the bottleneck — move people *to* fabrication from assembly and shipping (whose shadow prices are \$0 because they have slack), and profit goes up.

Each shadow price comes with an **allowable range** (an "activity range") — the interval over which you can change that right-hand side and still use the shadow price to predict the new objective via:

$$
\text{new objective} = \text{old objective} + (\Delta\text{RHS}) \times (\text{shadow price})
$$

Within the range you know how the *objective value* changes — but not exactly what the new *solution* looks like (add one fabrication hour and you'll likely make one more desk, but you'd re-solve to be sure).

You can pull all of this in Python. A quick look comes straight from the solved Pyomo model's **dual values** (shadow prices) and variable info, and the full report — reduced costs, marginals, and allowable ranges for every variable and constraint — comes from solving with **GLPK** and reading its sensitivity report. Either way, the discipline is the same: solve, then *interrogate* the solution.

## Wrap-up

```{admonition} Key takeaways
:class: tip
- A **Pyomo** model is the Chapter-1 math in code: `ConcreteModel` → `Var` → `Objective` → `Constraint` → `SolverFactory('cbc').solve`.
- Name constraints meaningfully; recognize **allocation (≤ max), covering (≥ min), blending** patterns.
- A **binding** constraint is met at equality; its **shadow price** is the value of one more unit of its right-hand side; non-binding constraints have **slack** and a shadow price of 0.
- **Reduced cost** is the shadow-price analog for a variable at a bound.
- Use **shadow prices to find the bottleneck** and decide where to invest; the **allowable range** says how far the linear prediction holds.
```
