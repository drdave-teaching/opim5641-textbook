# Module 5 Hub — Integer Programming (Fall 2026)

:::{admonition} ⚠️ Work in progress
:class: warning
This book is under active development for Fall 2026 — Module 5 (M5.1, 7 videos · 37 min) is recorded.
:::

From "how much" to "**do we or don't we**." Integer programming changes the domain of the decision — whole-number answers, yes/no answers — and unlocks a class of problems that quietly run the world: project selection, capital budgeting, product-line decisions, anything with a fixed cost.

> **A binary variable is a light switch. Linking constraints are the wiring that connects the switch to everything else.**

## The pieces

| What | Where | Why |
|---|---|---|
| 🎥 **The videos** | HuskyCT (Module 5) · [what each one covers](videos.md) | watch in order, run the notebook alongside |
| 📓 **The notebooks** | table below | every video drives one of these |
| ✅ **Skills sheet** | [what you can do now](skills.md) | check yourself off after the videos |
| 🧠 **Talking points** | [the theory to know](talking_points.md) | explain each in two sentences and you've got the module |
| 🛠️ **Working in this course** | [Colab + GitHub workflow](../module1_hub/working_in_course.md) | how to run and SAVE your work |
| ✍️ **Weekly checks** | [opim-math worksheets](https://github.com/drdave-teaching/opim-math) | the by-hand practice bank |

## The notebooks

Open in Colab and **Runtime → Run all**. Save your own copy before editing! (These install solvers from IDAES-PSE in the first cell — give it a minute.)

**The integer arc (`8_Integer/`):**
- **Integer Furniture** — the gateway: change the domain, watch the objective pay for it &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/8_Integer/Integer_Furniture.ipynb)
- **Project Selection** — binary variables and the logic constraints (at least / at most / exactly, mutually exclusive, contingent) &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/8_Integer/Integer_Project%20Selection.ipynb)
- **Fixed & Variable Costs: Mayhugh** — linking constraints, big-M and little-m &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/8_Integer/Fixed_VariableCosts_Mayhugh.ipynb)
- **Activation Variables** — the pattern on its own &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/8_Integer/Introduction%20and%20Activation%20Variables.ipynb)

**Going deeper:**
- **Covering** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/8_Integer/Covering.ipynb) · **Maximum Covering** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/8_Integer/Maximum%20Covering.ipynb) — facility-location flavors of the binary toolkit

```{tableofcontents}
```
