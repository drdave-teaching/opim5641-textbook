# Module 5 Talking Points — Integer Programming

**OPIM 5641 - Business Decision Modeling · Dr. Dave Wanik · University of Connecticut**

What you should be able to explain without opening a notebook.

---

## 1 · The domain is a modeling decision

Most of the time a fractional answer is harmless — 1,776.2 trucks means 1,776 trucks and nobody is hurt. Integrality matters when the *unit is indivisible and expensive*: factories, machines, projects, people. And it's never free: requiring whole numbers is one more piece of red tape, so the objective can only hold or fall. Know what you're paying before you pay it.

**Also worth saying in an interview:** integer problems are *harder* for solvers than continuous ones — the corner-point guarantee that made LP easy doesn't survive. That's why we don't make everything integer "just to be safe."

## 2 · Binary variables turn logic into arithmetic

A Binary variable is a light switch: 1 = fund the project, 0 = don't. The magic is that **business logic becomes arithmetic on switches**:

- *at least two of these* → $\sum y \ge 2$
- *no more than three* → $\sum y \le 3$
- *exactly one* → $\sum y = 1$
- *these two can't coexist* (same staff, NVIDIA-vs-AMD) → $y_4 + y_5 \le 1$
- *A only if B* → $y_A \le y_B$

**The truth-table habit:** for any of these, enumerate the 0/1 combinations and check which ones the constraint admits. Mutually exclusive admits (0,0), (1,0), (0,1), forbids (1,1). Thirty seconds of checking saves an afternoon of debugging.

**And the cautionary tale:** with the wrong domain (plain integers), the solver funded project four *five times* for \$40M. Binary fixed it at \$34M, projects 1, 3, 4. The model isn't wrong — the formulation was. Domains are part of the formulation.

## 3 · Linking constraints: wiring the switch to the dial

The fixed-cost problem is everywhere: \$10M to turn on the factory before the first pair of sneakers; a sales team's salary before the first pill is sold. That's a **yes/no** decision (activate?) coupled to a **how-much** decision (produce how many?) — and the coupling is a linking constraint.

**Big-M** ($x \le M \cdot y$): if the switch is off, the quantity is forced to zero; if on, the quantity can run up to $M$. Choose $M$ meaningfully — the demand ceiling — not "a billion," which makes solvers numerically seasick.

**Little-m** ($x - m \cdot y \ge 0$): if the switch is on, the quantity must be at least $m$. The portfolio rule: any stock you're in, you're in for at least 2% — no breadcrumbs.

**Together** they bracket a decision the way real policies do: *out entirely, or in between m and M.* And once the fixed cost sits on the switch in the objective, the model will make the cold-blooded call — fire the sales team, drop the line — whenever margin doesn't cover overhead. Your job is to check that the cold-blooded call survives contact with judgment (Module 2's lesson, one last time).

---

## The bridge to what's next

The final stretch is **networks** — flows through arcs, shortest paths, assignments. The punchline you can already anticipate: they're all LPs with clever structure, and the toolkit you now own (domains, switches, links) is exactly what they're built from. Videos drop before Studio 7; the reference chapter on networks is in Part II meanwhile.
