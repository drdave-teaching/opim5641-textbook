# Preface

Welcome to **Business Decision Modeling — Optimization with Python**, the book edition of **OPIM 5641** at the University of Connecticut.

Optimization is the science of making the **best possible decision** subject to the constraints of the real world — how many chairs and desks to build, where to put a warehouse, how to route product through a supply chain, which projects to fund. This book teaches you to take a messy business problem, translate it into a precise mathematical model, and solve it in Python with **Pyomo**. The voice is casual; the modeling is rigorous; the code is real and runs.

## Who this book is for

You're a graduate student or analyst comfortable with Python and basic data work. You don't need a background in operations research — we build every concept from the ground up, starting with the four building blocks that appear in *every* optimization problem in this book.

## How the book is organized

```{tableofcontents}
```

- **Chapter 1 — Foundations.** The anatomy of an optimization problem, brute-force search, and Monte Carlo simulation for decision-making under uncertainty.
- **Chapter 2 — Linear Programming: Graphical & Simplex.** The geometry of LP and the algorithm that solves it.
- **Chapter 3 — LP in Pyomo & Sensitivity Analysis.** Building real models in code, and reading the shadow prices and reduced costs that tell you *what your constraints are worth*.
- **Chapter 4 — Nonlinear Optimization.** When the world isn't linear: facility location, portfolio allocation, and regression as optimization.
- **Chapter 5 — Network Optimization.** Minimum-cost flow, assignment, shortest path, and transshipment.
- **Chapter 6 — Integer Programming.** Whole-number decisions, set covering, and the binary "activation" variables that model yes/no choices.

## How to read it

Read with a notebook open and **Pyomo + a solver installed** (CBC for linear/integer, Ipopt for nonlinear). When you hit a model, type it out — the goal is for the modeling pattern to come out of your fingertips. When you hit a **math callout**, don't skip it; the formulations *are* the subject. All code is drawn from the course notebooks on the [`drdave-teaching`](https://github.com/drdave-teaching) GitHub account.

Let's go model some decisions.

— *Dave*
