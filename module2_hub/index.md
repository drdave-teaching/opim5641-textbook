# Module 2 Hub — Brute Force & the Graphical Method (Fall 2026)

:::{admonition} ⚠️ Work in progress
:class: warning
This book is under active development for Fall 2026 — Module 2 is complete - brute force and the graphical method are both recorded.
:::

Module 1 gave you two verbs: when you have data you **explore** it, when you don't you **simulate** it. Module 2 adds the third:

> **When you have to decide, you optimize.**

We start with the dumbest, most honest method there is - try every possibility and keep the best one - and we push it until it breaks. That breakage is the whole reason the rest of the course exists.

## The pieces

| What | Where | Why |
|---|---|---|
| 🎥 **The videos** | HuskyCT (Module 2) · [what each one covers](videos.md) | watch in order, run the notebook alongside |
| 📓 **The notebooks** | table below | every video drives one of these |
| ✅ **Skills sheet** | [what you can do now](skills.md) | check yourself off after the videos |
| 🧠 **Talking points** | [the theory to know](talking_points.md) | explain each in two sentences and you've got the module |
| 🛠️ **Working in this course** | [Colab + GitHub workflow](../module1_hub/working_in_course.md) | how to run and SAVE your work |
| ✍️ **Weekly checks** | [opim-math worksheets](https://github.com/drdave-teaching/opim-math) | the by-hand practice bank |

## The notebooks

Open in Colab and **Runtime → Run all**. Save your own copy before editing!

**The brute-force arc (record order):**
- **Password Cracking Warm-Up** — brute force at its purest: crack a PIN and the word `apple` with nested loops, then watch the search space explode &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/3_BruteForce/Password_Cracking_Warmup.ipynb)
- **The Brute Force Method** — the four building blocks, the full Veerman Furniture search, and the running-time explosion &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/3_BruteForce/The%20Brute%20Force%20Method.ipynb)
- **Brute Force: Wyndor Glass** — word problem → linear program → brute-force solution (our Rosetta Stone problem) &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/3_BruteForce/BruteForce_Wyndor%20Glass.ipynb) · [blank version](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/3_BruteForce/BruteForce_Wyndor%20Glass_blank.ipynb)
- **Monte Carlo Meets Brute Force** — stress-test the "optimal" plan when demand and hours are uncertain &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/3_BruteForce/Monte%20Carlo%20Simulation%20and%20Brute%20Force.ipynb)

**Going deeper / legacy:**
- **Introduction to Optimization** — the original long-form version of the Veerman material &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/3_BruteForce/Introduction%20to%20Optimization_DW.ipynb) · [blank version](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/3_BruteForce/Introduction%20to%20Optimization_DW_blank.ipynb)

**Coming next — the graphical method** (`4_Graphical/`): draw the feasible region, walk the corner points, read off the optimum - plus the messy cases (redundant, infeasible, alternate optima, unbounded). Videos in production.

```{tableofcontents}
```
