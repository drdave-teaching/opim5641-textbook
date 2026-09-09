# Module 3 Video Guide — LP in Pyomo

**OPIM 5641 - Business Decision Modeling · Dr. Dave Wanik · University of Connecticut**

Module 2 ended with Wyndor solved three ways by hand. This block hires the machine: **Pyomo**, a Python package with real solvers behind it, that scales to real data — `pd.read_csv` straight into a model, no spreadsheet cells to highlight.

:::note
**Recorded 2026-08-11.** Seven videos (51 min), matching HuskyCT M3.1. Transcripts and polished scripts live in `opim5641-transcripts/hybrid_fall2026/async4_module3_1/`.
:::

## Notebook · `6_Pyomo_LP/0_General_Framework_LP_Pyomo` (blank + answers pair)

**M3.1 · 1 — Welcome to Module 3, and the blank Pyomo guide** *(8:08)*
Why Pyomo: this course used to run on Excel, highlighting cells and rows — limiting. Pyomo reads real tables and scales with real data. The teaching move is **blank-first**: Dave walks the blank notebook to plant the **five things to remember**, then flips to the answers version. Two monitors recommended — that's the whole course workflow in miniature.

**M3.1 · 2 — My first Pyomo code** *(10:04)*
The five things, coded: import Pyomo → `ConcreteModel()` (the blank canvas you append attributes to) → decision variables (`model.chairs = Var(domain=NonNegativeReals)`) → the objective with `sense=maximize` → constraints one by one (name them like an engineer, `Constraint1..3`, or like an analyst, `fabConstraint`, `paintingConstraint`...) → **solve and investigate**: objective value, variable values, and which constraints are the problems.

## Notebook · `6_Pyomo_LP/1_Allocation_Models.ipynb`

**M3.1 · 3 — Allocation models and shadow prices** *(5:32)*
The first of three problem patterns: an **allocation model** hands out a **limited resource among competing uses** — maximize, subject to ≤ constraints. The furniture example with a twist: this time we don't just *fit* the model, we **interrogate** it. Print the left-hand side of every constraint after solving and spot the **binding constraint** — fabrication is maxed out, and that's the production bottleneck worth money.

**M3.1 · 4 — Sensitivity analysis, the transparent way** *(8:23)*
The transparent route to shadow prices — no dual-variable mysticism, just a **for loop**. Fabrication is the bottleneck at 1,850 hours, so sweep it (1,500 → 5,000), re-solve once per value, save profit each pass, and plot profit vs. hours. The slope IS the shadow price — the value of one more hour — and you can *see* where it flattens (where the constraint stops binding). The same loop pattern as Monte Carlo and sensitivity everywhere: change one number, re-run, collect.

## Notebook · `6_Pyomo_LP/2_CoveringModels.ipynb`

**M3.1 · 5 — Covering models** *(6:59)*
Pattern two, flipped: **minimize cost subject to ≥ constraints.** Delby Outfitters trail mix — hit every nutritional floor for the lowest cost. And the famous punchline: the optimizer's first trail mix is *technically compliant and absolutely disgusting*, which is the judgment lesson from Module 2 arriving in code form.

**M3.1 · 6 — Enhancing the trail mix recipe** *(3:20)*
Put on the business hat: marketing won't sell the analytics department's trail mix, so add "at least a little of everything" constraints (each ingredient ≥ 0.1) and watch the recipe become sellable. Design note from Dave: you could set the same floors via variable **bounds** instead of constraints — both work, he likes *seeing* the constraints; it's your preference.

## Notebook · `6_Pyomo_LP/3_BlendingModels_Coffee.ipynb`

**M3.1 · 7 — Blending models: coffee and weighted averages** *(8:28)*
Pattern three: **blending**. You're a coffee maker with Brazilian, Colombian, and Peruvian beans — each with an aroma score, a strength score, a cost, and inventory on hand — and a target profile for the retail blend. Blends mean **weighted averages** in the constraints, and weighted averages mean fractions — which solvers hate — so the video shows the **algebra rearrangement** that clears the denominator and keeps the model linear.

---

*Companions: [skills sheet](skills.md) · [talking points](talking_points.md) · scripts in `opim5641-transcripts`*
