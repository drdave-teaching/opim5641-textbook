# Module 3 Talking Points — LP in Pyomo

**OPIM 5641 - Business Decision Modeling · Dr. Dave Wanik · University of Connecticut**

The ideas behind the M3.1 videos — what you should be able to explain to a classmate or an interviewer without opening a notebook.

---

## 1 · Why a solver, and why now

**You earned it.** Wyndor fell to brute force, then to a picture, then to tableau pivots — the same \$36,000 three times. Only *after* that does a solver make sense: you know exactly what Pyomo is doing under the hood (Simplex, mostly), so its answers are checkable, not oracular. When someone in a meeting asks "how do you know that's right?", you have three independent machines' worth of answer.

**Why Pyomo over Excel.** The old version of this course ran on Solver in Excel — highlighting cells, rows, columns. It works and it doesn't scale. `pd.read_csv` into Pyomo means real tables, real data files, and models that don't break when the data grows a row.

**The five things.** Import → `ConcreteModel()` → variables → objective → constraints; then solve and investigate. That's every Pyomo model you'll ever write. `ConcreteModel()` is just a blank canvas you append attributes to — which is why the code reads like the word problem.

## 2 · Fitting is half the job; interrogation is the other half

**A solved model is a starting point.** The objective value tells you the best you can do *under today's rules*. The interesting question is which rule to change. Print every constraint's left-hand side: the ones sitting at their limit are **binding** — the bottlenecks.

**Shadow prices, the transparent way.** The textbook route is dual variables; the transparent route is a **for loop**. Sweep the bottleneck's RHS (1,500 → 5,000 fabrication hours), re-solve at each value, plot profit against hours. The slope of that line is the **shadow price** — the dollar value of one more hour — and where the line flattens, the constraint has stopped binding and extra hours are worthless. One plot answers "what would you pay for overtime?" precisely.

**This is the meeting skill.** "Fabrication is binding; an hour of it is worth \$X up to about Y hours; painting is slack, don't spend a dime there" — that sentence is what separates an analyst from a person with a spreadsheet.

## 3 · The three patterns

**Allocation** — hand out a limited resource among competing uses. Maximize, ≤ constraints. Product mix is the classic.

**Covering** — meet floors at minimum cost. Minimize, ≥ constraints. Nutrition standards, staffing minimums, service levels.

**Blending** — hit a quality target that's a **weighted average** of what you mix. Coffee: the blend's aroma is the bean-weighted average of aromas. The wrinkle is algebraic: weighted averages put a fraction in the constraint, and solvers want linear expressions — so you **clear the denominator** by hand before the model ever sees it.

**Why patterns matter:** once you can sort a new word problem into allocation / covering / blending, you've done most of the formulation before touching a keyboard. Most business LPs are one of these three wearing a costume.

## 4 · The disgusting trail mix (the judgment lesson, again)

The covering model's first answer meets every nutritional standard at minimum cost — and is coconut flakes with a couple of raisins. That is not a bug. The model optimized exactly what it was told. The *analyst's* move is to notice the answer is absurd, realize a constraint is missing ("it should resemble trail mix"), encode it (everything ≥ 0.1), and re-solve. Module 2 taught this as a slogan; Module 3 makes you *do* it. Also a style note from Dave: floors can be constraints or variable bounds — both correct, pick the one you can read.

---

## The bridge to what's next

Everything so far was linear — straight lines and flat planes. Module 4 bends the world: powers, roots, exponents, distances. A linear solver won't take those problems, and a nonlinear one will confidently hand you an answer that isn't the best one. That's a new kind of danger, and it needs a new kind of care.
