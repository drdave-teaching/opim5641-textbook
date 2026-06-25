# Chapter 1 — Foundations of Optimization

Every optimization problem in this book — no matter how fancy — is built from the **same four pieces**. Learn to spot them in a word problem and you can model almost anything.

```{admonition} The four building blocks
:class: important
1. **Decision variables** — the things you control (how many chairs to build, where to put a warehouse).
2. **The objective function** — the single quantity you want to **maximize** (profit) or **minimize** (cost). You optimize *one* thing.
3. **Constraints** — the rules of reality (only 1,850 fabrication hours; demand ≤ 100 tables).
4. **Parameters / data** — the numbers you're given (profit per item, hours per unit).
```

Our running example is the **Veerman Furniture** company: decide how many **chairs, desks, and tables** to build to maximize profit, subject to limited fabrication, assembly, and shipping hours. In math:

$$
\max_{c,d,t}\; 15c + 24d + 18t \quad\text{s.t.}\quad
\begin{cases}
4c + 6d + 2t \le 1850 & \text{(fabrication)}\\
3c + 5d + 7t \le 2400 & \text{(assembly)}\\
3c + 2d + 4t \le 1500 & \text{(shipping)}\\
c,d,t \ge 0
\end{cases}
$$

That's the whole game: an objective, some constraints, and variables you're solving for. The rest of the book is about *recognizing* this structure in business problems and solving ever-richer versions of it.

```{admonition} Two quotes to model by
:class: tip
**H. L. Mencken:** *"For every complex problem there is an answer that is clear, simple, and wrong."* Don't oversimplify reality away. And **George Box:** *"All models are wrong, but some are useful."* Don't over-engineer it either. A model is a deliberate, useful simplification — your job is to make it useful, not perfect.
```

## 1.1 Brute-force search

Before any clever algorithm, there's the most honest method of all: **try every combination and keep the best.** If chairs, desks, and tables each range over some possibilities, loop over all of them, check feasibility, and track the best objective:

```python
best_profit, best_plan = float('-inf'), None
for c in range(0, 361):
    for d in range(0, 301):
        for t in range(0, 101):
            if (4*c+6*d+2*t <= 1850 and 3*c+5*d+7*t <= 2400 and 3*c+2*d+4*t <= 1500):
                profit = 15*c + 24*d + 18*t
                if profit > best_profit:
                    best_profit, best_plan = profit, (c, d, t)
print(best_plan, best_profit)
```

Brute force is **guaranteed correct** and easy to reason about — and **catastrophically inefficient**. Three variables with a few hundred values each is already millions of combinations; add variables and the count explodes combinatorially. That inefficiency is exactly the motivation for everything that follows: linear programming and the Simplex algorithm find the optimum without enumerating the universe.

## 1.2 Monte Carlo simulation — deciding under uncertainty

Real decisions involve **uncertainty**: a stock return, the number of insurance claims, how long a part lasts. **Monte Carlo simulation** handles this by *sampling* the randomness many times and looking at the **distribution** of outcomes rather than a single point estimate.

The recipe is a three-step escalation:

1. **One run.** Simulate a single trajectory — e.g., a 35-year retirement nest egg where each year's stock growth is `np.random.normal(0.07, 0.20)` — accumulating year by year.
2. **Repeat 10,000 times.** Wrap it in a loop, keep the **ending value** of each run, and plot a **histogram** of outcomes with mean and 25th/75th-percentile lines.
3. **"Spaghetti."** Keep *every* year of *every* run and plot all 10,000 trajectories at once to see the cone of possibilities widen over time.

```python
import numpy as np
endings = []
for sim in range(10000):
    money = 10000.0
    for year in range(35):
        money *= (1 + np.random.normal(0.07, 0.20))   # uncertain annual growth
    endings.append(money)
np.percentile(endings, [25, 50, 75])   # report a range, not a single number
```

```{admonition} Why simulate instead of just averaging?
:class: tip
Plugging in the *average* return gives you one number and a false sense of certainty. Simulation gives you the **whole distribution** — so you can say "there's a 25% chance of ending below \$X" — which is exactly the kind of risk statement a decision-maker needs. The same machinery powers the insurance, inventory, and reliability examples later in the course.
```

## Wrap-up

```{admonition} Key takeaways
:class: tip
- Every model has **decision variables, an objective, constraints, and data** — find them first.
- You optimize **one** objective (max profit *or* min cost), subject to constraints.
- **Brute force** always works and never scales — the reason we need real optimization algorithms.
- **Monte Carlo** turns uncertainty into a distribution of outcomes; report a *range*, not a point.
- Keep Mencken and Box on your shoulder: a model should be **useful**, neither naïvely simple nor needlessly complex.
```
