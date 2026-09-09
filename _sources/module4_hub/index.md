# Module 4 Hub — Nonlinear & Portfolio Optimization (Fall 2026)

:::{admonition} ⚠️ Work in progress
:class: warning
This book is under active development for Fall 2026 — Module 4 is fully recorded: nonlinear (M4.1, 6 videos · 41 min) and the Ms. Womack portfolio block (M4.2, 4 videos).
:::

Everything so far was linear — straight lines and flat planes. Here the world bends: powers, roots, exponents, distances. A linear solver won't take these problems, and a nonlinear one will confidently hand you an answer that isn't the best one.

> **New module, new dangers: initialize your variables, bound them where you can — and if a linear model will do, use it.**

The payoff for the new care is the best application in the course: **Ms. Womack's portfolio** — real modern portfolio theory, where risk is a quadratic (the weighted covariance matrix) and the reward is an efficient frontier you built yourself.

## The pieces

| What | Where | Why |
|---|---|---|
| 🎥 **The videos** | HuskyCT (Module 4) · [what each one covers](videos.md) | watch in order, run the notebook alongside |
| 📓 **The notebooks** | table below | every video drives one of these |
| ✅ **Skills sheet** | [what you can do now](skills.md) | check yourself off after the videos |
| 🧠 **Talking points** | [the theory to know](talking_points.md) | explain each in two sentences and you've got the module |
| 🛠️ **Working in this course** | [Colab + GitHub workflow](../module1_hub/working_in_course.md) | how to run and SAVE your work |
| ✍️ **Weekly checks** | [opim-math worksheets](https://github.com/drdave-teaching/opim-math) | the by-hand practice bank |

## The notebooks

Open in Colab and **Runtime → Run all**. Save your own copy before editing!

**The nonlinear arc (M4.1 · `7_Nonlinear/`):**
- **Polynomial** — why nonlinear, and why initialization matters &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/7_Nonlinear/Polynomial.ipynb) · [blank version](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/7_Nonlinear/Polynomial_blank.ipynb)
- **Pharmacy: regression as optimization** — fit $y = a + bx$ by minimizing squared error in Pyomo &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/7_Nonlinear/Pharmacy%20-%20Complete_guided.ipynb) · [blank version](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/7_Nonlinear/Pharmacy%20-%20Complete_blank.ipynb)
- **Warehouse location, simple** — minimize total distance (a square root!) to 10 stores &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/7_Nonlinear/Location%20Problem_Simple_guided.ipynb) · [blank version](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/7_Nonlinear/Location%20Problem_Simple_blank.ipynb)
- **Warehouse location, advanced** — weight the stores by deliveries and watch the warehouse move &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/7_Nonlinear/Location%20Problem_Advanced_guided.ipynb)

**The portfolio arc (M4.2):**
- **Covariance and Correlation** — umbrella-and-ice-cream intuition to the covariance matrix &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/7_Nonlinear/2_Covariance_and_Correlation.ipynb)
- **Portfolio Allocation: Ms. Womack** — five stocks, risk buckets, and the efficient frontier (with DEMO 1/DEMO 2 comparing even-split vs. concentrated) &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/7_Nonlinear/Portfolio_Allocation_Womack.ipynb)

**Going deeper:**
- **Regression framework in Pyomo** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/7_Nonlinear/General%20Framework_Regression%20in%20Pyomo.ipynb) · **Pharmacy from CSV** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/7_Nonlinear/Pharmacy_from_csv.ipynb) · **Womack generalized (live-class build)** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/7_Nonlinear/Live_GeneralizeWomack.ipynb)

## Two pictures worth keeping open

**The whole Ms. Womack methodology, end to end:**

![Ms. Womack methodology: data → summarize → model → solve → sweep the risk budget to draw the efficient frontier](https://raw.githubusercontent.com/drdave-teaching/OPIM5641-notebooks/main/figures/womack_methodology.png)

**What `calc_risk` is really computing** — every cell of the covariance matrix weighted by the proportions, then summed:

![calc_risk for two stocks: each covariance cell weighted by the product of proportions, summed into portfolio risk](https://raw.githubusercontent.com/drdave-teaching/OPIM5641-notebooks/main/figures/calc_risk_two_stocks.png)

```{tableofcontents}
```
