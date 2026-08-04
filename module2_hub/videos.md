# Module 2 Video Guide — Brute Force (Async 2, part 1)

**OPIM 5641 - Business Decision Modeling · Dr. Dave Wanik · University of Connecticut**

Module 1 ended with *"when you have data you explore it; when you don't, you simulate it."* Module 2 adds the third verb: **when you have to decide, you optimize.** This half of Async 2 is brute force - the dumbest, most honest optimization method there is, and the one that makes you *want* the smarter methods coming next.

Watch in order; each video drives one stretch of its notebook. The 🔴 markers inside the notebooks show exactly where each video starts.

---

## Notebook 1 · `3_BruteForce/Password_Cracking_Warmup.ipynb`
**The big ideas:** brute force = N decisions → N nested for loops · enumeration order decides your luck · widening the alphabet multiplies the work, adding length multiplies it harder · a password has ONE right answer, a business has thousands of workable plans - which is why optimization needs an objective.

**Video 1 — Brute force warm-up: cracking passwords** *(~8 min)*
The 1980s garage-door opener that sweeps the whole frequency spectrum and opens anybody's door - that's brute force in one image. The pivot out of Module 1: *is there a distribution of values for your password, or is there one password?* One. That's simulation versus optimization in a sentence. Then the 5-digit PIN with five nested loops (cracked on attempt **12,346** - a PIN's value IS its position in the enumeration), and finally the quiz question you've threatened in class for years: loop a-to-z five deep, **when do you hit `apple`?** Answer: **274,071 guesses**, only 2.3% into the space, because `a` is early - where `zebra` would cost 11.5 million.

**Video 2 — Why IT makes you use capitals and numbers** *(~6 min)*
The explosion, measured rather than asserted: the notebook times its own guess rate, then shows that widening the alphabet from 26 → 52 multiplies the work **32x**, and 26 → 62 multiplies it **77x** - same five characters. Then the bigger lever: keep the alphabet at lowercase and go from 5 characters to 8, and it's a **17,576x** jump - five seconds becomes most of a day. Closes on the table that maps password cracking onto Veerman Furniture, one row at a time, ending on the row that matters: *one right answer vs. many feasible answers.*

---

## Notebook 2 · `3_BruteForce/The Brute Force Method.ipynb`
**The big ideas:** the four building blocks of EVERY optimization model · brute force as enumerate-filter-score · the incumbent pattern (best-so-far outside the loop) · keeping data separate from the model · why the running time explodes and what that costs you.

**Video 3 — The four building blocks + what brute force means** *(~9 min)*
Every optimization problem, however fancy, is the same four pieces: **decision variables, an objective, constraints, and data.** Spot all four in Veerman Furniture (chairs, desks, tables across fabrication/assembly/shipping) before writing a line of code. Then the thesis: brute force is wildly inefficient but foolproof - you get the right answer *and* you see why.

**Video 4 — (optional) Python warm-up: lists, dictionaries, filtering** *(~6 min)*
The on-ramp for rusty Python - and the real point is **soft coding**: data lives in dictionaries, the model lives in the loop. Plant the seed here that this exact data/model split is what Pyomo formalizes in Module 3. Skippable if your students did Module 1.

**Video 5 — The full brute-force search** *(~9 min)*
Initialize the incumbent, loop everything, keep the winner. Nested integer for-loops, clear upper bounds, **every constraint in ONE readable `if`**, print the answer - this is the house style and the style the weekly checks use. The `best_*` variables live outside the loops, which is the same accumulator pattern that carried your balance forward in Monte Carlo; here it carries the champion. Answer: **\$8,400** at 0 chairs, 275 desks, 100 tables, after grinding 10,974,761 combinations (~6-10 seconds on camera).

**Video 6 — Watch it die: the running time explodes** *(~8 min)*
Same code, double the data - and *only* the data changes, which is the soft-coding payoff on screen. 11 million combinations becomes **87 million**, and the runtime goes up about **9x**. ⏱️ *Camera note: this cell takes 60-90 seconds. Have patter ready - it's the perfect window for the red-tape point (adding constraints can never improve the objective) and for planting Studio 2 ("we'll feel this explosion by hand - bring a pencil").* Closes on when brute force IS the right tool (sanity checks, small or weird one-off problems) and the handoff: *the graphical method draws a picture instead.*

---

## Notebook 3 · `3_BruteForce/BruteForce_Wyndor Glass.ipynb`
**The big ideas:** turning a word problem into a formal LP (decision variables → objective → constraints) · feasible vs. infeasible vs. optimal · the resource-allocation pattern · Wyndor as the course's Rosetta Stone.

**Video 7 — Wyndor Glass: from word problem to linear program** *(~9 min)*
The Hillier & Lieberman classic, and the one problem we deliberately solve **three ways** - brute force now, graphically next, then Simplex. Say "Rosetta Stone" on camera. You're the analyst in the management meeting: pull the pieces out of the story (2 products, 3 plants, hours, profits), define $x_1$ and $x_2$, write $Z = 3000x_1 + 5000x_2$, and translate each plant's capacity into an inequality. Formulation finished, no code yet.

**Video 8 — Brute-forcing Wyndor** *(~7 min)*
Dictionaries for the data, loops for the model, one big `if`. 41 × 41 = **1,681 combinations** - and note the zero counts, because making none of a product is a perfectly valid plan. Vocabulary lands here: **feasible / infeasible / optimal**. The answer: **\$36,000 per week at (2, 6)**. Closes on the contrast that sets up everything: 1,681 was instant, 87 million was not - so next we draw a picture instead of looping.

---

## Notebook 4 · `3_BruteForce/Monte Carlo Simulation and Brute Force.ipynb`
**The big ideas:** the deterministic optimum is a **ceiling**, not a promise · uncertainty in the objective (demand) vs. uncertainty in the constraints (hours) · optimization gives you the plan, Monte Carlo tells you how much to trust it.

**Video 9 — Monte Carlo meets brute force** *(~9 min)*
The bridge that ties both modules together. Re-run the search for the deterministic plan (0 chairs, 275 desks, 100 tables, \$8,400), then admit we never actually knew demand - jitter it ±10% and re-score the *same* plan 10,000 times. The punchline: the average lands **below** \$8,400 and never above it. Then the sharper second act - jitter the available *hours* instead, and the plan isn't merely less profitable, it can be **infeasible** (about half the time, and always fabrication). Closes: *optimization hands you the plan; Monte Carlo tells you how much to trust it.*

---

## Coming next in Async 2
**The graphical method** — the first *smart* method: for two-variable problems, draw the feasible region, walk the corner points clockwise from the origin, and read off the optimum. Plus the messy cases (redundant, infeasible, alternate optima, unbounded). Notebooks are in `4_Graphical/`; videos not yet recorded.

## Also in the folder
- `Introduction to Optimization_DW.ipynb` (+ blank twin) — the original long-form version of the Veerman material. `The Brute Force Method.ipynb` is the polished lecture cut of it; keep this one as the deeper/legacy reference.
- `BruteForce_Wyndor Glass_blank.ipynb`, `Introduction to Optimization_DW_blank.ipynb` — blank twins for students to fill in.
- `Week4_MCRefresh_BruteForce.ipynb` — the live-class driver from Fall 2025.

---

*Companions: [Module2_Skills.md](https://github.com/drdave-teaching/OPIM5641-notebooks/blob/main/Module2_Skills.md) · [Module2_Talking_Points.md](https://github.com/drdave-teaching/OPIM5641-notebooks/blob/main/Module2_Talking_Points.md) · [Working in this Course](https://github.com/drdave-teaching/OPIM5641-notebooks/blob/main/Module1_Working_in_this_Course.md)*
