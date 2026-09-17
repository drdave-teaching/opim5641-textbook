# Module 5 Skills Sheet — Integer Programming

**OPIM 5641 - Business Decision Modeling · Dr. Dave Wanik · University of Connecticut**

After the M5.1 videos and notebooks, these are the skills you own.

---

## 🔢 Integer domains
*Notebook: `8_Integer/Integer_Furniture.ipynb`*

- ☐ Decide when a fractional answer is acceptable (round 1,776.2 trucks) and when the domain genuinely must be integer
- ☐ Change a variable's domain to integers in Pyomo and predict the direction of the objective change (red tape: never better)
- ☐ Explain *why* integrality costs objective — it's one more constraint on the feasible set

## 💡 Binary variables & selection logic
*Notebook: `8_Integer/Integer_Project Selection.ipynb`*

- ☐ Model a yes/no decision with a **Binary** domain — and show what nonsense a plain integer domain produces ("select project four five times")
- ☐ Formulate a capital-budgeting problem: maximize NPV subject to a budget, one switch per project
- ☐ Write the logic constraints cold: **at least m** ($\sum y \ge m$), **at most n** ($\sum y \le n$), **exactly k** ($\sum y = k$)
- ☐ Encode **mutually exclusive** projects ($y_4 + y_5 \le 1$) and **contingent** ones ($y_a \le y_b$)
- ☐ Verify any binary constraint with a **truth table** — enumerate the 0/1 cases and check which are allowed

## 🔗 Linking constraints
*Notebooks: `8_Integer/Fixed_VariableCosts_Mayhugh.ipynb` · `Introduction and Activation Variables.ipynb`*

- ☐ Explain the fixed-cost problem in one sentence: the lights cost money before the first unit
- ☐ Write the **big-M** link $x \le M \cdot y$ and choose a sensible $M$ (the demand ceiling — not a random huge number)
- ☐ Write the **little-m** link $x - m \cdot y \ge 0$ for minimum thresholds ("if you're in, you're in for at least 2%")
- ☐ Put the fixed cost on the switch in the objective — and interpret it when the model drops a product line entirely
- ☐ Combine both links to bracket a decision: in for at least $m$, at most $M$, or out at zero

---

## The one-sentence version

> **You can model decisions themselves — fund it or don't, activate the line or don't — and wire those switches to quantities with big-M and little-m, which is how capital budgets, product portfolios, and fixed-cost decisions actually get made.**

Coming later this semester: **networks** — flows, paths, and assignments (videos drop before Studio 7).
