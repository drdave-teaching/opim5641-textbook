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
