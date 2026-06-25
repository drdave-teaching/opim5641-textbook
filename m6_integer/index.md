# Chapter 6 — Integer Programming

Sometimes a fractional answer is fine — 12.6 tons of steel, round it off. But sometimes it isn't: you can't build 266.67 desks, open half a fire station, or fund 0.4 of a project. **Integer programming (IP)** forces decision variables to take whole-number values, and — surprisingly — that single restriction unlocks the ability to model **logic**: yes/no choices, "if this then that," "pick at most two." This is the most expressive chapter in the book.

## 6.1 Integer constraints

Start with the furniture problem from Chapter 3. Solved as a continuous LP it might say *make 266.67 desks* — meaningless on a factory floor. The fix is one word: change the variable **domain** from `NonNegativeReals` to `NonNegativeIntegers`:

```python
from pyomo.environ import *
model = ConcreteModel()

# the ONLY change from the LP: integer domain
model.c = Var(domain=NonNegativeIntegers)   # chairs
model.d = Var(domain=NonNegativeIntegers)   # desks
model.t = Var(domain=NonNegativeIntegers)   # tables

model.profit = Objective(expr = 15*model.c + 24*model.d + 18*model.t, sense = maximize)
# ... same constraints ...
SolverFactory('cbc').solve(model)
```

```{admonition} Integrality is a constraint — and it costs you
:class: important
Forcing integers is a genuine **constraint**: it shrinks the feasible set, so the integer optimum is **never better** than the relaxed (continuous) optimum and usually a touch worse. Solve the furniture problem both ways and the integer version makes slightly less profit — that's the price of a buildable answer. As a modeler you decide whether the fractional "noise" is acceptable (round it) or whether the decision is genuinely discrete (enforce it).
```

## 6.2 Binary "activation" variables — modeling yes/no

The real power comes from **binary** variables, $y \in \{0,1\}$, that switch a decision **on or off**. They let you model things linear programming simply cannot:

**Fixed (setup) costs.** A plant costs a fixed amount to *operate at all*, plus a per-unit cost. Let $y=1$ if we use the plant. A **linking constraint** ties production $x$ to the switch:

$$
x \le M \cdot y
$$

If $y=0$ the plant is off and $x$ is forced to 0; if $y=1$ we may produce up to its capacity $M$, and we pay the fixed cost $K\cdot y$ in the objective. This **fixed-charge** pattern is everywhere in operations.

**Set covering.** The **fire-station** problem: place stations so every district is covered (has a station in it or in a neighbor), minimizing the number of stations. For each district, require the sum of activation variables over itself and its neighbors to be **≥ 1**:

$$
\min \sum_j y_j \quad\text{s.t.}\quad \sum_{j \in N(i)} y_j \ge 1 \;\;\forall i
$$

The **weighted** version (maximize covered demand with at most *k* stations) adds a coverage variable per district and is the template for facility-siting everywhere from ambulances to cell towers.

## 6.3 Logical constraints — the recipe

Binary variables turn English logic into algebra. The common project-selection rules:

- **Mutually exclusive** ("not both 1 and 2"): $\;y_1 + y_2 \le 1$
- **Contingent** ("3 requires 4"): $\;y_3 \le y_4$
- **Pick exactly one** ("4 or 6, not both"): $\;y_4 + y_6 = 1$
- **At least *k*** ("fund at least 4 projects"): $\;\sum_j y_j \ge 4$

```{admonition} The recipe for any logical constraint
:class: tip
When a rule is gnarly, fall back on a mechanical procedure: **(1)** write a truth table of the relevant binaries and mark the **forbidden** rows; **(2)** for each forbidden row, write one inequality that rules out *exactly* that combination and nothing else; **(3)** add them all. The inequalities are satisfied by every allowed combination and violated only by the ones you want to forbid. Clever one-liners are nice when you spot them, but the recipe always works — and that reliability is what you want under exam or deadline pressure.
```

You build all of this in Pyomo exactly as before — binary `Var(domain=Binary)`, the linking/logical constraints in a `ConstraintList`, and **CBC** (which has an integer solver) to solve. The only conceptual leap is seeing that a business rule like *"we can't do project 5 if we do both 1 and 3"* is just $y_1 + y_3 + y_5 \le 2$.

## Wrap-up

```{admonition} Key takeaways
:class: tip
- **Integer programming** forces whole-number decisions — one word in Pyomo (`NonNegativeIntegers`) — at a small cost in objective value (integrality is a real constraint).
- **Binary activation variables** model **yes/no**; a **linking constraint** $x \le My$ ties a quantity to its on/off switch (the **fixed-charge** pattern).
- **Set covering** ($\sum_{j\in N(i)} y_j \ge 1$) places fire stations, ambulances, cell towers.
- **Logical rules** become algebra: mutually exclusive, contingent, exactly-one, at-least-*k* — and the **truth-table recipe** handles anything.
- Solve it all with **CBC**; the leap is realizing business logic *is* linear constraints on binaries.
```


---

## 📌 Lecture key points

*Distilled takeaways from the video lectures behind this chapter — click each to expand.*


:::{admonition} Introduction to Integer Programming (+ Intro to IP — Furniture)
:class: note dropdown
- Fractional answers (266.67 desks) are often unacceptable → force **integers**.
- Change the domain `NonNegativeReals` → **`NonNegativeIntegers`** (one word).
- **Integrality is a constraint** → integer optimum is never better (furniture: \$8,200 → \$8,199).
- Two schools: **round** the fractional answer, or **enforce** integers.
- As modeler, decide if the fractional "noise" matters.
:::

:::{admonition} Application — Linking Constraints (Portfolio)
:class: note dropdown
- **Linking constraint**: invest in a stock only if you invest **≥ 10%**.
- Adds threshold-minimum logic to portfolio allocation.
- Smoother efficient-frontier trade-off (a policy decision).
- Consistent naming; cross out previously-infeasible constraints.
- Shows the flexibility/policy power of integer/linking constraints.
:::

:::{admonition} Fire Station Problem (+ Weighted + Solving Weighted)
:class: note dropdown
- **Set covering**: every district covered by a station in it or a **neighbor**; minimize # stations.
- Constraint: sum of activation variables over a district + neighbors **≥ 1**.
- **Weighted** version: maximize **covered demand** with **at most k** stations (cardinality).
- Careful: **activation ≠ coverage**; count a covered demand **only once**.
- Bind the two binary sets so coverage requires an activated neighbor.
:::

:::{admonition} Project Selection — Intro + 1st/2nd/Last Constraints + Pyomo Model
:class: note dropdown
- Maximize total **NPV** by selecting projects (binary activation variables).
- **Logical constraints** as algebra: mutually exclusive (y1+y2≤1), contingent (y3≤y4), exactly-one (y4+y6=1), at-least-k (Σ≥4).
- The **recipe**: truth table → forbid "no" rows → one inequality each.
- Model **each constraint independently** (ignore the others while writing it).
- Smart one-liners are fine, but the recipe always works.
:::

:::{admonition} Formulation and Pyomo Code — Setup Costs
:class: note dropdown
- **Fixed-charge**: pay a setup cost to operate a plant at all (independent of volume).
- Two variable types: integer **production** + binary **activation**.
- **Linking constraint** `x ≤ M·y`: y=0 → x=0; y=1 → up to capacity.
- Objective: profit per unit − setup cost × activation.
- Solve with **CBC** (handles integers).
:::

:::{admonition} Banana Problem & E.R. Problem
:class: note dropdown
- **Banana** (smartphones): activation variables for plants with **fixed operation costs**; maximize profit.
- **E.R.**: a covering problem — pick doctors so each procedure has ≥ 1 capable doctor; minimize salary cost.
- Both = binary activation variables + covering/fixed-charge patterns.
- E.R. solution: cost \$600, doctors 1 & 2.
- Same recipe as fire station / project selection.
:::

:::{admonition} Mixed Problems
:class: note dropdown
- Real problems mix **"≤" and "≥"** constraints (extend the diet problem).
- A maximization with only lower bounds is **unbounded** → add a **budget** ("≤").
- **Packing↔maximization, covering↔minimization** duality helps diagnose crazy solutions.
- "Weird" optimal solutions (all fish) are correct given the constraints → add realism (min amounts, equalities).
- Use `setlb`, `==` for equalities.
:::

:::{admonition} Excel appendix (Intro/Spreadsheet Org, Solving in Excel, Excel vs Python)
:class: note dropdown
- **Frontline Solver** + `SUMPRODUCT` build LP models in Excel; color-code input/variables/objective/constraints.
- Excel pros: easy to **test/play**, familiar, fast prototyping, single-screen for small problems, condensed **sensitivity report**.
- Excel cons: **doesn't scale**, hides constraints in cells (poor explainability), OS-dependent, manual to re-shape.
- Python wins for **scalability, data science, explainability, free/Colab, reproducibility**.
- Use Excel for quick/small/results-only; **Python for real-world** optimization.
:::
