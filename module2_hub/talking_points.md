# Module 2 Talking Points — Brute Force & the Graphical Method

**OPIM 5641 - Business Decision Modeling · Dr. Dave Wanik · University of Connecticut**

The ideas behind the brute-force videos - the things I say out loud that you should be able to explain to a classmate or an interviewer without opening a notebook. Skills are what you can *do*; this is what you *understand*.

---

## 1 · Simulation vs. optimization

**The password question settles it.** Is there a *distribution* of values for your computer password, or is there one password? One. That's the whole distinction. **Monte Carlo characterizes uncertainty** - it hands you a distribution of outcomes so you can talk about a business problem probabilistically. **Optimization hunts for the single best answer** - the one combination of decisions that maximizes (or minimizes) what you care about. Module 1 was simulation. From here on, this course is an optimization course.

**Scrabble is the same idea.** Five tiles on your rack, a board in front of you: there's one word that scores the most points. Maybe a tie, but there's one best move. That's optimization - and notice it has all the pieces: decisions (which word, where), a constraint (you only have those tiles), and an objective (points).

**Optimal ≠ sensible.** Our furniture answer says build zero chairs. That's genuinely the most profitable plan, and it might still be a terrible business decision - you may need chairs in the catalog to keep the distributor happy. The model optimizes what you *told* it to optimize. Your judgment stays in the room.

## 2 · Brute force, the honest algorithm

**The garage-door opener.** There's an 80s toy that sweeps the entire frequency spectrum and opens anybody's garage door. It isn't clever - it just tries everything until something works. That is brute force, and it's exactly how you'd crack a password: `aaaaa`, `aaaab`, `aaaac`... until you hit `apple`.

**The recipe, three steps.** (1) For each decision variable, list every value it could take. (2) Make every combination. (3) Check each one for feasibility, score the survivors, keep the best. When the loop ends, whatever you're holding IS the optimum - no cleverness required, just a computer and patience.

**N decisions means N nested loops.** Five letters in a password = five nested loops. Three products in a factory = three nested loops. The shape of the code is the shape of the problem.

**Enumeration order decides your luck.** `apple` costs 274,071 guesses because `a` is early in the alphabet; `zebra` costs 11.5 million because `z` is late. Same code, same length, ~42x the work. That's why we judge an algorithm by its **worst case**, not the run where we got lucky.

**Why brute force is worth teaching at all:** it's always correct, it's explainable to a five-year-old or a CEO, and it needs no special math. Use it to sanity-check a fancier model - if a small version of your problem doesn't agree with brute force, your model is wrong.

## 3 · The four building blocks

Every optimization model, however fancy, is four pieces:

1. **Decision variables** - what *you* control (how many chairs, which machine does which job).
2. **The objective** - the single number you're maximizing or minimizing. You optimize *one* thing.
3. **Constraints** - the rules of reality (1,850 fabrication hours; demand ≤ 100 tables; and the one everybody forgets - you can't build a negative number of anything).
4. **Data** - the given numbers. Fixed; you just use them.

**Feasible, infeasible, optimal.** A *feasible* solution satisfies every constraint. An *infeasible* one violates at least one. The *optimal* one is feasible AND has the best objective value. Notice the order of those words - "optimal but infeasible" is nonsense.

**Resource-allocation is the most common pattern you'll meet.** Left-hand side = the amount of a resource your plan uses; right-hand side = the amount available; LHS ≤ RHS. Product mix is the classic case. Once you see that shape, most business problems start looking familiar.

**More red tape can never help.** Adding a constraint can only shrink the feasible region, so the objective can never *improve* - it can only stay the same or get worse. That's why "can we relax this rule?" is such a powerful question in a real meeting.

## 4 · Writing the search well

**The house style, and why.** Nested integer for-loops, clear upper bounds, **every constraint in ONE `if`**, print the answer. No `continue`, no early exits. The reason isn't taste - it's that the logic then reads top to bottom exactly like the word problem does, which is what the weekly checks ask you to produce by hand. (The `continue` style works fine and you should be able to *read* it. It's also marginally faster, since it bails the moment one constraint fails - about 10-15%. Not enough to save you, as you'll see.)

**The incumbent pattern.** The `best_*` variables live **outside** the loops so they survive every pass - that's the same accumulator that carried your balance forward year after year in the Monte Carlo videos. There it carried money; here it carries the champion.

**Zero counts.** Every range starts at zero, because making none of a product is a perfectly valid plan - and in Veerman, "zero chairs" turns out to be the *right* plan.

**Soft coding.** Keep the data in dictionaries and the model in the loop. The payoff shows up on screen: to solve a completely different scenario, we changed only the data and reran the identical search. That data/model separation is exactly what Pyomo formalizes in Module 3 - you're building the habit early.

**Don't break early in optimization.** In password cracking you stop the instant you find the answer. In optimization you can't - a better plan might be sitting three combinations later, so you have to score them all.

## 5 · The explosion (and why this course exists)

**Watch it die.** Double the demands and the hours and the *same* problem goes from 11 million combinations to **87 million** - roughly **9x** the runtime. Scale by 10x instead of 2x and you're looking at about **1,000x**. That's not a slow afternoon; that's hours of your life.

**Password math makes it visceral.** Five characters, lowercase only: 11.9 million combinations. Add capitals: **32x** bigger. Add digits too: **77x** bigger - all without making the password any longer. Now go from 5 characters to 8 and the space grows **17,576x** ($26^3$), turning seconds into most of a day. **Length beats complexity** - that's the practical security lesson, and the algorithmic one.

**Where brute force truly fails, not just struggles:**
- **Continuous variables** - if a variable can be any real number, you can't list its values; there are infinitely many.
- **Proving infeasibility** - if no feasible solution exists, you must check the entire space to know it.
- **Combinatorial blowup** - 70 machines and 70 jobs is about $10^{100}$ permutations, a googol. There are only about $10^{80}$ atoms in the observable universe, so you'd run out of universe before you ran out of options.

**So the honest conclusion:** brute force is exact and simple, and on real problems it usually isn't good enough. That gap is precisely why the graphical method, Simplex, and Pyomo take up the rest of this course.

## 6 · Optimization under uncertainty

**The deterministic optimum is a ceiling, not a promise.** We found \$8,400 assuming we knew demand exactly. Let demand wobble ±10% and re-score that same plan 10,000 times: the average comes in *below* \$8,400 and never above. You can only sell what shows up, so surprises on the downside cost you and surprises on the upside are wasted inventory.

**Two flavors of uncertainty, and the second one is scarier.** Uncertainty in the **objective** (demand moves) means your profit is lower than advertised. Uncertainty in the **constraints** (available hours move) means your plan may not be *possible at all* - and in our run the plan was infeasible about half the time, always because of fabrication. That's the constraint to protect in real life.

**The division of labor, in one line:** optimization hands you the plan; Monte Carlo tells you how much to trust it. Neither is complete alone, and that's the arc of the whole course.

## 7 · The graphical method - the first smart method

**Every constraint is the equation of a line.** Strike the inequality off $3T + 4C \le 2400$ and you have $3T + 4C = 2400$ - grade-school algebra. That's the whole leap: an optimization problem is a *picture* you can draw in two dimensions.

**How you plot one.** Set one variable to zero and solve for the other; then swap. For carpentry: when $T=0$, $C=600$; when $C=0$, $T=800$. Two points make a line. And a constraint with only one variable in it (like $C \le 450$ or $T \ge 100$) is just a flat horizontal or vertical line.

**Which side do you shade?** Don't guess - **use a test point.** Plug in something easy like $(1,1)$ and ask whether the inequality holds. If it does, that side is allowed and you shade the other. It works every time and it's what you'll do on paper under exam pressure.

**The feasible region is the leftover white space** - the only place where every constraint is satisfied at once. Every point in it is a plan you could actually run.

**The corner point property is the whole trick.** The optimum always sits at a **corner** of the feasible region, because anything strictly inside is a linear combination of the corners - some suboptimal blend. So you never check the infinite interior; you check a handful of extreme points. That's how millions of brute-force combinations collapse into **five**.

**Finding the corners:** the ones on an axis you read straight off the graph - typically three of five come free. For the rest you do algebra: scale one equation so a variable matches, **subtract to cancel it**, solve for what's left, then **back-substitute**. Multiplying an equation of a line by a constant doesn't move the line - same slope, just scaled - which is why that manoeuvre is legal.

**Then plug and chug.** Every corner goes into the objective function, and the best value wins.

**A property worth noticing** (and it pays off later in Simplex): as you walk around the feasible region, the objective climbs, climbs, climbs - and then falls off. It isn't random. Simplex exploits exactly that.

**Minimization works identically.** The corner point property doesn't care which direction you're going. Only the "which corner wins" step flips.

**Two edge cases you should recognize on sight:**
- **Redundant constraints** - a line that isn't doing any work. It sits outside the feasible region and shapes nothing. Harmless, but worth spotting: it means a rule you were worried about isn't binding.
- **Infeasible setups** - constraints that *fight each other*, leaving no feasible region at all. This is the single most common error you'll hit later in this course, and the fix is never "run it again" - it's going back and finding which two rules can't both be true.

**And the limitation that drives the rest of the course:** the graphical method only works with **two decision variables**. Three needs a 3-D plot; four has nothing to draw. So we need an **algebraic extension of this geometric technique** - which is precisely what **Simplex** is.

## 8 · Optimal is not the same as sensible

The furniture optimizer says build **zero chairs**. Mathematically perfect - and possibly terrible, because customers walk into a furniture store expecting chairs.

The trail-mix optimizer fills the bag with **coconut flakes and about two raisins**. It satisfies every nutritional constraint you wrote down, at the lowest possible cost. It is also not trail mix.

**The lesson:** the model optimizes exactly what you told it to optimize, using exactly the constraints you gave it. When the answer looks absurd, that's not the math failing - it's the model telling you that your constraints were incomplete. Your judgment doesn't leave the room just because you found the optimum.

---

## The bridge to what's next

Brute force works, and brute force dies. The graphical method rescued us by drawing a picture instead of enumerating - millions of combinations down to five corner points - but it can only ever handle two decision variables.

So the next stop is **Simplex**: the algebraic extension of the graphical method, walking those same corners in any number of dimensions, long after we can't draw the picture. And **Wyndor Glass** is our Rosetta Stone - you've now solved it with brute force *and* graphically, and you'll solve it a third time with Simplex, so you can watch the same answer (\$36,000 at 2 doors and 6 windows) fall out of three completely different machines.
