# Module 3 Skills Sheet — LP in Pyomo

**OPIM 5641 - Business Decision Modeling · Dr. Dave Wanik · University of Connecticut**

After the M3.1 videos and notebooks, these are the skills you own. Check yourself off — if one feels shaky, the notebook to revisit is named right there.

---

## 🐍 The Pyomo framework
*Notebook: `6_Pyomo_LP/0_General_Framework_LP_Pyomo` (blank + answers)*

- ☐ Recite the **five things**: import → `ConcreteModel()` → decision variables → objective → constraints, then solve and investigate
- ☐ Declare a decision variable with the right domain: `model.chairs = Var(domain=NonNegativeReals)`
- ☐ Write the objective with an explicit `sense` (maximize or minimize)
- ☐ Add constraints one at a time with names a stranger could read (`fabConstraint`, not `c7`)
- ☐ Solve, then pull out the **objective value** and every **decision variable's value** — never report a model you haven't inspected
- ☐ Explain how this is the same data/model split you practiced with dictionaries and loops in Module 2

## 📈 Allocation models + interrogation
*Notebook: `6_Pyomo_LP/1_Allocation_Models.ipynb`*

- ☐ Recognize an **allocation model** on sight: limited resource, competing uses, maximize against ≤ constraints
- ☐ Print each constraint's **left-hand side** after solving and classify it as **binding** (resource exhausted) or slack
- ☐ Say what a binding constraint means in business terms: this is the bottleneck — the place more capacity is worth money
- ☐ Run a **sensitivity sweep** with a for loop: range of RHS values → re-solve per value → collect profit → plot
- ☐ Read a **shadow price** off that plot as the slope (the value of one more unit of the resource) — and spot where it goes flat (the constraint stopped binding)
- ☐ Explain why "can we get more fabrication hours?" is worth real money and "can we get more shipping hours?" may be worth nothing

## 🥣 Covering models
*Notebook: `6_Pyomo_LP/2_CoveringModels.ipynb`*

- ☐ Recognize a **covering model**: minimize cost subject to ≥ floors (nutrition, staffing, service levels)
- ☐ Build one in Pyomo and get the compliant-but-disgusting answer without panicking
- ☐ Fix it like an analyst: add "at least a little of everything" constraints — or equivalent variable bounds — and defend the choice
- ☐ Explain why the disgusting trail mix is the model working correctly: your constraints were incomplete, not the math

## ☕ Blending models
*Notebook: `6_Pyomo_LP/3_BlendingModels_Coffee.ipynb`*

- ☐ Recognize a **blending model**: quality targets expressed as **weighted averages** of the inputs
- ☐ Do the algebra that clears the fraction so the constraint stays linear (solvers don't like denominators)
- ☐ Set up the coffee problem: three beans, aroma/strength scores, costs, inventory limits, a target blend profile
- ☐ Name the three patterns cold — **allocation, covering, blending** — and sort a new word problem into one of them in under a minute

---

## The one-sentence version

> **You can take any of the three classic LP patterns from a word problem to a solved, interrogated Pyomo model — and walk into the meeting knowing not just the plan, but which bottleneck is worth money and how much.**

Next stop: **nonlinear** — powers, roots, and distances, where a linear solver won't take the problem at all.
