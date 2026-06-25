# Chapter 2 — Linear Programming: Graphical Method & Simplex

A **linear program (LP)** is an optimization problem where the objective and all constraints are **linear** — every variable appears only multiplied by a constant and added up, never multiplied together, raised to powers, or buried in functions. That restriction sounds limiting, but it buys us something priceless: a **guarantee** that we can find the true optimum efficiently. This chapter gives you both the *geometry* of LP (the graphical method) and the *algorithm* that scales it to any number of variables (Simplex).

## 2.1 The graphical method (2-D)

With two decision variables you can literally *draw* the problem. Take Flair's Furniture — maximize profit over tables $T$ and chairs $C$ subject to a few resource constraints. Each constraint is a line; the inequality keeps one side of it. **Shade the infeasible side of every constraint, and what's left unshaded is the feasible region** — the set of all decision combinations that obey every rule.

```{admonition} The corner-point theorem
:class: important
For a linear program, **the optimum always sits at a corner (vertex) of the feasible region.** Why? The objective $profit = 7T + 5C$ defines parallel "level lines"; pushing them in the improving direction, the last point of contact with the feasible region is a corner. So you don't need to check infinitely many points — just evaluate the objective at each corner and take the best. (For Flair's Furniture that's \$4,040 at 320 tables and 260 chairs.)
```

Four special cases are worth seeing once so you recognize them forever:

- **Redundant constraint** — a constraint that doesn't touch the feasible region; removing it changes nothing.
- **Infeasible** — constraints conflict, so the feasible region is empty; no solution exists.
- **Unbounded** — the feasible region runs off to infinity in the improving direction; usually a sign you forgot a constraint.
- **Alternate optima** — the objective level line is parallel to a binding constraint, so an *entire edge* of corners is optimal; you have flexibility in the product mix.

The graphical method is perfect intuition but caps out at two variables. The Simplex algorithm generalizes the exact same idea — *walk the corners, improving each step* — to any dimension.

## 2.2 Simplex — walking the corners in any dimension

To run Simplex we first put the LP in **standard form** by turning each "≤" inequality into an equality with a **slack variable** (the unused amount of that resource):

$$
4c+6d+2t \le 1850 \;\;\Longrightarrow\;\; 4c+6d+2t + s_1 = 1850,\quad s_1 \ge 0
$$

With slacks added, the variables split into **basic** (currently in the solution — the slacks, at the start) and **nonbasic** (set to zero — the real variables, at the start). That starting point is the origin: make nothing, use no resources. Simplex then **pivots** from corner to corner, each pivot swapping one variable in and one out, always improving the objective, until no improving move remains.

```{admonition} One pivot, by hand
:class: tip
Lay the system out as a **tableau** (Dave's convention: the **objective function goes in the BOTTOM row**).
1. **Entering variable** — pick the column with the most-negative entry in the bottom (objective) row; that variable improves the objective fastest.
2. **Departing variable** — for that column, compute the ratio $b_i / a_i$ for each positive $a_i$ and pick the **smallest** (the *minimum ratio test*); that row leaves the basis.
3. **Pivot** — divide the pivot row to make the pivot element 1, then add/subtract multiples of it to zero out the rest of the pivot column.
Repeat until **no negative entries remain** in the bottom row — that's the optimum. It's exactly the graphical method's "walk to a better corner," done with arithmetic instead of a picture, and it generalizes to 3-D, 10-D, or a thousand variables.
```

For a **minimization** problem we lean on a beautiful fact — **duality**. Every minimization LP (the *primal*) has a partner maximization LP (the *dual*); you transpose the problem's coefficient matrix, solve the easier maximization with the same Simplex machinery, and **read the minimization's answer off the final tableau**. This primal–dual relationship (due to von Neumann) isn't just a trick — in Chapter 3 the dual values reappear as **shadow prices**, the economic value of each constraint.

## Wrap-up

```{admonition} Key takeaways
:class: tip
- An **LP** has a linear objective and linear constraints — and a guarantee of an efficiently-findable optimum.
- The **graphical method**: shade infeasible sides → feasible region → the optimum is at a **corner**.
- Recognize **redundant / infeasible / unbounded / alternate-optima** cases on sight.
- **Simplex** generalizes corner-walking via **slack variables**, a **tableau** (objective in the bottom row), and **pivots** (entering = most-negative bottom row; departing = minimum ratio test).
- **Duality** solves minimization by transposing to a maximization — and seeds the **shadow prices** of Chapter 3.
```


---

## 📌 Lecture key points

*Distilled takeaways from the video lectures behind this chapter — click each to expand.*


:::{admonition} Linear Functions
:class: note dropdown
- An LP has a **linear** objective and **linear** constraints (multiply by constants, then add).
- You **cannot** multiply variables, use logs/exp/abs/sqrt/fractions, or `if` conditions.
- **Linearity guarantees** an efficiently-findable optimum (huge advantage).
- Nonlinear is more expressive but loses optimality guarantees.
- History: **Dantzig** (Simplex) and **von Neumann** (duality); *Good Will Hunting* legend.
:::

:::{admonition} Simple Bounds
:class: note dropdown
- **Upper bounds** for a maximization can be found by deliberately **over-estimating** the objective.
- Inflate the objective coefficients (must be **≥** the real ones) and relax the variable limits.
- A valid bound proves "we cannot make more than \$X."
- Tightening the bound (e.g., $10→$8 coefficients) narrows the gap to the true optimum.
- Bounds make a solution *provably* good.
:::

:::{admonition} Objective Function (Pyomo)
:class: note dropdown
- `Objective(expr=..., sense=maximize)` — a direct transcription of the math.
- Pyomo knows `model.c`, `model.t` etc. because the variables were declared.
- Set **`sense`** to maximize or minimize.
- Build a big expression separately (loops/ifs) then pass it in.
- Linear only: multiply by constants and add.
:::

:::{admonition} Constraints (Pyomo)
:class: note dropdown
- A `Constraint` needs an **expression with a sign and a right-hand side**.
- **Equality needs `==`** (double equals), or Python won't understand it.
- **Name constraints meaningfully** (`fabrication`, not `Constraint1`) — pays off in reports.
- Bounds can be set on variables or via constraints (don't double up).
- Order (LHS vs RHS) is flexible; keep variables on the left for readability.
:::

:::{admonition} Simplex for 2D Maximization — Parts 1–3
:class: note dropdown
- Put the LP in **standard form** with **slack variables** (unused resource).
- **Basic** (in solution) vs **nonbasic** (set to 0); start at the origin.
- **Pivot:** entering var = most-negative bottom row; departing = **minimum ratio test**.
- Keep pivoting until **no negatives in the bottom row** = optimum.
- It's the graphical method's "walk to a better corner," generalized to any dimension.
:::

:::{admonition} Simplex for 3D Maximization (Soup to Nuts)
:class: note dropdown
- Same logic with an extra variable x3.
- **Ties for the entering variable** → pick at random.
- Read the optimal solution off the final tableau.
- Demonstrates Simplex scaling beyond 2-D.
- The algorithm is mechanical and dimension-agnostic.
:::

:::{admonition} Simplex for 2D Minimization — Parts 1–2
:class: note dropdown
- Minimization solved via the **dual**: build an augmented matrix and solve as a **maximization**.
- **von Neumann duality** — read the min answer off the max tableau.
- (Dave's convention: objective function in the **bottom row**.)
- Same pivoting machinery.
- Dual values foreshadow **shadow prices** (Module 3).
:::

:::{admonition} Simplex for 3D Minimization
:class: note dropdown
- Minimize w with all "≥" constraints.
- Augmented matrix → **transpose** → solve the dual → read the final tableau.
- Generalizes the dual approach to 3-D.
- Reinforces primal–dual relationship.
- Completes the Simplex toolkit.
:::
