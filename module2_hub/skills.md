# Module 2 Skills Sheet — Brute Force

**OPIM 5641 - Business Decision Modeling · Dr. Dave Wanik · University of Connecticut**

After the brute-force videos and notebooks, these are the skills you own. Module 1 taught you to explore data and simulate what you don't have. This is where you start **deciding**. Check yourself off - if one feels shaky, the notebook to revisit is named right there.

---

## 🔓 Enumeration - the brute-force mindset
*Notebook: `3_BruteForce/Password_Cracking_Warmup.ipynb`*

- ☐ Explain brute force in one sentence to a non-technical person (the garage-door opener works)
- ☐ Say what makes optimization different from Monte Carlo: a password has ONE answer, a distribution has a range
- ☐ Turn "N decisions, each with K choices" into **N nested for loops** - and compute the size of the space as $K^N$
- ☐ Crack a 5-digit PIN and a 5-letter password with explicit nested loops, counting every attempt
- ☐ Explain why a password's *position in the enumeration* decides how long the search takes (`apple` at 2.3%, `zebra` at 96.8%)
- ☐ `break` out of nested loops correctly - one `break` per level - and explain why optimization deliberately does NOT break early
- ☐ Measure your own machine's guess rate and use it to estimate how long a bigger search would take (don't hand-wave, measure)
- ☐ Quantify why password rules exist: widening the character set (26 → 52 → 62) vs. adding length - and know which lever is stronger

## 🧱 The four building blocks of a model
*Notebooks: `The Brute Force Method.ipynb` · `BruteForce_Wyndor Glass.ipynb`*

- ☐ Name all four pieces of any optimization model: **decision variables, objective, constraints, data**
- ☐ Read a word problem and pull out all four (Veerman Furniture and Wyndor Glass, from scratch)
- ☐ Write the objective as a formula, e.g. maximize $15c + 24d + 18t$
- ☐ Translate a capacity sentence into an inequality, e.g. "Plant 3 has 18 hours" → $3x_1 + 2x_2 \le 18$
- ☐ Remember the constraint everybody forgets: you can't build a negative number of anything
- ☐ Use the vocabulary precisely: **feasible** (satisfies every constraint) · **infeasible** (violates at least one) · **optimal** (feasible AND best objective value)
- ☐ Recognize a **resource-allocation / product-mix** problem when you see one (LHS uses a resource, RHS is what's available, LHS ≤ RHS)

## 🔁 Writing the search (the house style)
*Notebooks: `The Brute Force Method.ipynb` · `BruteForce_Wyndor Glass.ipynb` (+ blank twins)*

- ☐ Write a brute-force search in the course style: **nested integer for-loops, clear upper bounds, every constraint in ONE `if`, print the answer** - this is what the weekly checks ask for
- ☐ Set defensible upper bounds on each decision variable (demand limits, or a safe over-estimate like Wyndor's 40)
- ☐ Include **zero** in every range - making none of a product is a valid plan
- ☐ Use the **incumbent pattern**: `best_*` variables initialized OUTSIDE the loops, updated only when you find something better (same accumulator idea as Monte Carlo)
- ☐ Keep **data separate from the model** - dictionaries for the numbers, loops for the logic - so a new scenario means changing only the data
- ☐ Read the `continue` style when you meet it in the wild, and explain why the one-big-`if` version reads better
- ☐ Compute how many combinations a search will try *before* you run it

## 💥 Knowing when brute force breaks
*Notebook: `The Brute Force Method.ipynb`*

- ☐ Explain why running time explodes as a problem grows (11M → 87M combinations ≈ 9x the time)
- ☐ Say why brute force can't handle **continuous** variables at all
- ☐ Explain why proving *no* feasible solution exists forces you to check the entire space
- ☐ Name when brute force is genuinely the right call: sanity-checking a model, or small/weird one-off problems
- ☐ Explain why adding a constraint can never *improve* the objective (more red tape, never more profit)
- ☐ Make the argument for why the rest of this course exists - and what you'd reach for instead (graphical, then Simplex)

## 🎲 Optimization under uncertainty
*Notebook: `Monte Carlo Simulation and Brute Force.ipynb`*

- ☐ Take an optimal plan and **stress-test it** with Monte Carlo instead of trusting the single number
- ☐ Explain why the deterministic optimum is a **ceiling**: jitter demand and the average profit lands below it, never above
- ☐ Tell the difference between uncertainty in the **objective** (demand moves → profit moves) and uncertainty in the **constraints** (hours move → your plan can become *infeasible*)
- ☐ Estimate the probability your plan is infeasible by counting simulations, and identify **which** constraint is the fragile one
- ☐ State the division of labor out loud: optimization hands you the plan; Monte Carlo tells you how much to trust it

---

## The one-sentence version

> **You can take a business problem written in English, pull out the decisions, the goal, and the rules, and have a computer grind through every possible plan to find the provably best one - and you know exactly when that approach will fall on its face.**

Next stop: the first method that's actually *smart* about it.
