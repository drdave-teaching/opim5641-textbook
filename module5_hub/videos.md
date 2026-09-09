# Module 5 Video Guide — Integer Programming

**OPIM 5641 - Business Decision Modeling · Dr. Dave Wanik · University of Connecticut**

The decision itself becomes the variable: whole numbers, then yes/no switches, then the linking constraints that wire a switch to a quantity.

:::note
**Recorded 2026-08-19.** Seven videos (37 min), matching HuskyCT M5.1. Transcripts and polished scripts live in `opim5641-transcripts/hybrid_fall2026/async7_module5_1/`.
:::

## Notebook · `8_Integer/Integer_Furniture.ipynb`

**M5.1 · 1 — Introduction to integer programming** *(5:26)*
The gateway drug: the furniture problem with one tweak. Often a fractional answer is fine — 1,776.2 trucks is 1,776 trucks — but sometimes it truly isn't, and then you change the variable's **domain** to integers. The red-tape rule rides again: an integer requirement is one more constraint, so the objective can only stay the same or get worse. You pay for whole numbers; this video shows the bill.

## Notebook · `8_Integer/Integer_Project Selection.ipynb`

**M5.1 · 2 — Project selection: binary variables** *(7:11)*
The application students use at work the next day — grants, capital expenditures, project portfolios. You're consulting on capex: each project has a cost and a net present value, the budget won't cover them all, which do you fund? The key move is the **Binary domain**: each project's variable is a yes/no switch, and suddenly "which subset?" is just an LP with switches.

**M5.1 · 3 — Basic project selection constraints** *(5:25)*
Why Binary matters, demonstrated by getting it wrong first: with a plain integer domain the solver "selects project four five times" for \$40M — nonsense, you can't install the same machine five times. Binary fixes it: \$34M, projects one, three, and four. Then the logic vocabulary: **at least m** projects, **at most n**, **exactly k** — each one a one-line constraint on a sum of switches, and each one costs objective (red tape, always).

**M5.1 · 4 — Mutually exclusive and contingent projects** *(4:47)*
The two advanced relationships. **Mutually exclusive** ($y_4 + y_5 \le 1$): both off, either on, never both — "if you choose NVIDIA you can't choose AMD." **Contingent** ($y_a \le y_b$): project A only if project B. Work the truth table by hand and check the constraint allows exactly the right rows — that habit is how you'll debug binary logic forever.

## Notebook · `8_Integer/Fixed_VariableCosts_Mayhugh.ipynb`

**M5.1 · 5 — Intro to linking constraints: Mayhugh** *(4:49)*
Dave's favorite of the block: **fixed costs**. Before you make one pair of sneakers, you pay to turn the factory lights on. Think of it as a pharma company with three drugs, each needing its production line activated. The pattern: couple a **yes/no** variable (activate the line?) with a **how much** variable (pills made) — that coupling is a **linking constraint**.

**M5.1 · 6 — Product maximums: fire the sales team** *(5:44)*
The big-M linking constraint: $x \le M \cdot y$, where $M$ is a genuinely big number (the demand ceiling works). If the line isn't activated ($y=0$), production is forced to zero; if it is, production can go up to demand. Attach the sales team's fixed cost to $y$ in the objective and the model will happily **fire the sales team** — drop a whole product line — when the margin doesn't cover the overhead.

**M5.1 · 7 — Product minimums and thresholds** *(3:57)*
The mirror image, little-m: $x - m \cdot y \ge 0$. If you're in, you're in for at least $m$ — Dave's portfolio rule: invest in a stock at all, and it must be at least 2% of the money, so you don't scatter breadcrumbs across twenty tickers. Same wiring, opposite sign, and together big-M and little-m bracket a decision: *in for at least this, at most that, or out entirely.*

---

*Companions: [skills sheet](skills.md) · [talking points](talking_points.md)*
