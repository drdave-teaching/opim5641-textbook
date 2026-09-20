# Module 3 Hub — LP in Pyomo (Fall 2026)

:::{admonition} ⚠️ Work in progress
:class: warning
This book is under active development for Fall 2026 — Module 3 (M3.1, 7 videos · 51 min) is recorded.
:::

You have solved the same problem three ways by hand. Now hand it to a solver — and because you did it the hard way first, the solver is a tool you understand rather than a magic spell.

> **Brute force taught you the problem. The picture taught you the geometry. Simplex taught you the algebra. Pyomo just does the typing.**

This module is also where the course stops being about *one* problem shape: you'll meet the three patterns that cover most of business — **allocation** (maximize against ≤ constraints), **covering** (minimize against ≥ constraints), and **blending** (weighted averages in the constraints) — plus the skill that makes optimization valuable in a meeting: **interrogating the model** for binding constraints and shadow prices.

## The pieces

| What | Where | Why |
|---|---|---|
| 🎥 **The videos** | HuskyCT (Module 3) · [what each one covers](videos.md) | watch in order, run the notebook alongside |
| 📓 **The notebooks** | table below | every video drives one of these |
| ✅ **Skills sheet** | [what you can do now](skills.md) | check yourself off after the videos |
| 🧠 **Talking points** | [the theory to know](talking_points.md) | explain each in two sentences and you've got the module |
| 🛠️ **Working in this course** | [Colab + GitHub workflow](../module1_hub/working_in_course.md) | how to run and SAVE your work |
| ✍️ **Weekly checks** | [opim-math worksheets](https://github.com/drdave-teaching/opim-math) | the by-hand practice bank |

## The notebooks

Open in Colab and **Runtime → Run all**. Save your own copy before editing!

**The Pyomo arc (`6_Pyomo_LP/`):**
- **General Framework: LP in Pyomo** — the five things to remember, taught blank-first &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/6_Pyomo_LP/0_General_Framework_LP_Pyomo_blank.ipynb) · [answers version](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/6_Pyomo_LP/0_General_Framework_LP_Pyomo_answers.ipynb)
- **Allocation Models** — the furniture problem in Pyomo, then the interrogation: binding constraints, shadow prices, and the sensitivity for-loop &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/6_Pyomo_LP/1_Allocation_Models.ipynb)
- **Covering Models** — Delby Outfitters trail mix: minimize cost against nutrition floors, then fix the disgusting answer &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/6_Pyomo_LP/2_CoveringModels.ipynb)
- **Blending Models: Coffee** — weighted averages, and the algebra that keeps fractions out of the solver &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/6_Pyomo_LP/3_BlendingModels_Coffee.ipynb)

**Going deeper:**
- **Blending Models: Furniture** — a second blending workout &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/6_Pyomo_LP/4_BlendingModels_Furniture.ipynb)

```{tableofcontents}
```
