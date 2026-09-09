# Module 4 Talking Points — Nonlinear & Portfolio

**OPIM 5641 - Business Decision Modeling · Dr. Dave Wanik · University of Connecticut**

What you should be able to explain without opening a notebook.

---

## 1 · The world bends

**Linearity was a gift.** Straight lines and flat planes gave us the corner point property, Simplex, and answers that were provably global. The moment a power, root, exponent, or step enters the model, that gift is revoked: the surface has hills and valleys, and a solver can park in a valley that isn't the deepest one.

**The three disciplines of nonlinear work:** initialize (and try several starts — if different starts give different answers, you've found local optima), bound your variables (it helps the solver converge), and if a linear model can do the job, use it. Linear solvers are faster *and* their answers come with a guarantee; nonlinear answers come with a shrug.

**A local optimum isn't a bug.** It's the honest geometry of the problem. The bug is *trusting* one run. Professionals re-run from multiple initializations and compare.

## 2 · Regression is optimization wearing a lab coat

Every stats class you've taken was secretly this class. Least squares *is* an optimization problem: decisions $a$ and $b$, objective = sum of squared errors. Cast it in Pyomo and the mystery evaporates — and suddenly you can do things `sklearn` won't let you: swap squared error for absolute error, bolt on weird functional forms, add business constraints to a regression ("the slope can't be negative").

**The placeholder pattern** is the Pyomo idiom worth remembering: make a prediction variable per row, then pin each one to the model's form with a constraint. The constraints carry the model; the objective just totals the damage.

**Different error metrics live in different universes.** A sum of absolute errors will usually be a smaller *number* than a sum of squared errors. That's units, not quality. Compare fits with your eyes and with the same metric, never across metrics.

## 3 · Distance makes geography nonlinear

Euclidean distance is a square root, so "where should the warehouse go?" is inherently a nonlinear problem. The simple version finds the centroid of your stores. The honest version weights each store by its delivery volume — and the warehouse slides toward the store doing the business. One weighting turns a geometry exercise into a logistics decision.

## 4 · Umbrellas, ice cream, and why covariance is the whole ballgame

Two Caribbean companies each make 10% a year, and each loses money in its off-season. Hold either alone and you ride a rollercoaster; hold both and the seasons cancel. **That's covariance** — and it's why portfolio risk is a property of the *pairings*, not of the stocks one at a time. Diversification isn't "own many things"; it's "own things that zig when the others zag."

**You can't max return and min risk at once.** One objective, period. The move is to maximize return subject to a **risk budget** — then move the budget and solve again.

**Risk is a quadratic.** Portfolio risk = the covariance matrix with every cell weighted by the product of the proportions invested, summed. For two stocks that's four terms; for five, twenty-five. Proportions multiply proportions — that's the nonlinearity, and that's why this sits in Module 4 and not Module 3.

**The efficient frontier is a menu, not an answer.** Each risk cap yields the best-possible return and an allocation. Sweep the caps and the curve appears: steep at first (cheap return for a little risk), flattening as risk stops paying. The model's job ends at drawing the menu. Choosing from it — that's the client's risk appetite, and no solver has one.

---

## The bridge to what's next

Module 5 changes the *kind* of decision. Everything so far asked "how much?" — a continuous answer. Next is "**do we or don't we?**" — binary variables, project selection, and the linking constraints that tie a yes/no to a how-much. From optimization on quantities to optimization on *decisions themselves*.
