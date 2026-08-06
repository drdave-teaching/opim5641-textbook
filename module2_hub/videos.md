# Module 2 Video Guide — Brute Force & the Graphical Method

**OPIM 5641 - Business Decision Modeling · Dr. Dave Wanik · University of Connecticut**

Module 1 ended with *"when you have data you explore it; when you don't, you simulate it."* Module 2 adds the third verb: **when you have to decide, you optimize.** This half of Async 2 is brute force - the dumbest, most honest optimization method there is, and the one that makes you *want* the smarter methods coming next.

Watch in order; each video drives one stretch of its notebook. The 🔴 markers inside the notebooks show exactly where each video starts.

:::note
**Recorded 2026-08-04 and 2026-08-06.** Fifteen videos are in the can - titles below match what's in Kaltura (tagged `(BDM_hybrid)`). Transcripts and polished scripts live in `opim5641-transcripts/hybrid_fall2026/async2_module2/`.
:::

## Video 0 · Introduction to Module 2 *(3:58)*
The bridge out of Module 1. You can already describe data you have and simulate data you don't - now we add the third verb: **decide**. The move from **descriptive** analytics ("what's going on?") through Monte Carlo's "what's possible?" to **prescriptive** analytics ("what should I do?"). Brute force is where we start, because it's 100% transparent - you can see every rule, it's built out of the for loops you already know, and its only real sin is being slow.

---

## Notebook 1 · `3_BruteForce/Password_Cracking_Warmup.ipynb`
**The big ideas:** brute force = N decisions → N nested for loops · enumeration order decides your luck · widening the alphabet multiplies the work, adding length multiplies it harder · a password has ONE right answer, a business has thousands of workable plans - which is why optimization needs an objective.

**Watch and read alongside notebook 1:**
- 📺 [This Toy Can Open Any Garage](https://www.youtube.com/watch?v=CNodxp9Jy4A) (Veritasium) — the garage-door opener from class: brute force in hardware, sweeping the whole frequency spectrum until a door opens.
- 📖 [Python `for` loops: `break` and `continue`](https://www.w3schools.com/python/gloss_python_for_break.asp) (W3Schools) — short and practical; we lean on `break` hard here and meet `continue` in the notebooks that follow.

**Video 1 — Brute force warm-up: cracking passwords** *(6:52)*
The 1980s garage-door opener that sweeps the whole frequency spectrum and opens anybody's door - that's brute force in one image. The pivot out of Module 1: *is there a distribution of values for your password, or is there one password?* One. That's simulation versus optimization in a sentence. Then the 5-digit PIN with five nested loops (cracked on attempt **12,346** - a PIN's value IS its position in the enumeration), and finally the quiz question you've threatened in class for years: loop a-to-z five deep, **when do you hit `apple`?** Answer: **274,071 guesses**, only 2.3% into the space, because `a` is early - where `zebra` would cost 11.5 million.

**Video 2 — Why IT makes you use letters and numbers** *(3:41)*
The explosion, measured rather than asserted: the notebook times its own guess rate, then shows that widening the alphabet from 26 → 52 multiplies the work **32x**, and 26 → 62 multiplies it **77x** - same five characters. Then the bigger lever: keep the alphabet at lowercase and go from 5 characters to 8, and it's a **17,576x** jump - five seconds becomes most of a day. Closes on the table that maps password cracking onto Veerman Furniture, one row at a time, ending on the row that matters: *one right answer vs. many feasible answers.*

---

## Notebook 2 · `3_BruteForce/The Brute Force Method.ipynb`
**The big ideas:** the four building blocks of EVERY optimization model · brute force as enumerate-filter-score · the incumbent pattern (best-so-far outside the loop) · keeping data separate from the model · why the running time explodes and what that costs you.

**Video 3 — Intro to the Veerman furniture example** *(4:31)*
Every optimization problem, however fancy, is the same four pieces: **decision variables, an objective, constraints, and data.** Spot all four in Veerman Furniture (chairs, desks, tables across fabrication/assembly/shipping) before writing a line of code. Then the thesis: brute force is wildly inefficient but foolproof - you get the right answer *and* you see why.

**Video 4 — Python warm-up for brute-force** *(5:47)*
The on-ramp for rusty Python - and the real point is **soft coding**: data lives in dictionaries, the model lives in the loop. Plant the seed here that this exact data/model split is what Pyomo formalizes in Module 3. Skippable if your students did Module 1.

**Video 5 — A full walk-through of brute-force for Veerman Furniture** *(9:10)*
Initialize the incumbent, loop everything, keep the winner. Nested integer for-loops, clear upper bounds, **every constraint in ONE readable `if`**, print the answer - this is the house style and the style the weekly checks use. The `best_*` variables live outside the loops, which is the same accumulator pattern that carried your balance forward in Monte Carlo; here it carries the champion. Answer: **\$8,400** at 0 chairs, 275 desks, 100 tables, after grinding 10,974,761 combinations (~6-10 seconds on camera).

**Video 6 — Runtimes exploding nonlinearly (17s to 2 min when we double the data)** *(2:47)*
Same code, double the data - and *only* the data changes, which is the soft-coding payoff on screen. 11 million combinations becomes **87 million**, and the runtime goes up about **9x**. ⏱️ *Camera note: this cell takes 60-90 seconds. Have patter ready - it's the perfect window for the red-tape point (adding constraints can never improve the objective) and for planting Studio 2 ("we'll feel this explosion by hand - bring a pencil").* Closes on when brute force IS the right tool (sanity checks, small or weird one-off problems) and the handoff: *the graphical method draws a picture instead.*

---

## Notebook 3 · `3_BruteForce/BruteForce_Wyndor Glass.ipynb`
**The big ideas:** turning a word problem into a formal LP (decision variables → objective → constraints) · feasible vs. infeasible vs. optimal · the resource-allocation pattern · Wyndor as the course's Rosetta Stone.

**Video 7 — Wyndor with brute force** *(5:13)*
The Hillier & Lieberman classic, and the one problem we deliberately solve **three ways** - brute force now, graphically next, then Simplex. Say "Rosetta Stone" on camera. You're the analyst in the management meeting: pull the pieces out of the story (2 products, 3 plants, hours, profits), define $x_1$ and $x_2$, write $Z = 3000x_1 + 5000x_2$, and translate each plant's capacity into an inequality. Formulation finished, no code yet.

**(folded into Video 7 on recording day)** — brute-forcing Wyndor
Dictionaries for the data, loops for the model, one big `if`. 41 × 41 = **1,681 combinations** - and note the zero counts, because making none of a product is a perfectly valid plan. Vocabulary lands here: **feasible / infeasible / optimal**. The answer: **\$36,000 per week at (2, 6)**. Closes on the contrast that sets up everything: 1,681 was instant, 87 million was not - so next we draw a picture instead of looping.

---

## Notebook 4 · `3_BruteForce/Monte Carlo Simulation and Brute Force.ipynb`
**The big ideas:** the deterministic optimum is a **ceiling**, not a promise · uncertainty in the objective (demand) vs. uncertainty in the constraints (hours) · optimization gives you the plan, Monte Carlo tells you how much to trust it.

**Video 8 (not yet recorded) — Monte Carlo meets brute force** *(~9 min)*
The bridge that ties both modules together. Re-run the search for the deterministic plan (0 chairs, 275 desks, 100 tables, \$8,400), then admit we never actually knew demand - jitter it ±10% and re-score the *same* plan 10,000 times. The punchline: the average lands **below** \$8,400 and never above it. Then the sharper second act - jitter the available *hours* instead, and the plan isn't merely less profitable, it can be **infeasible** (about half the time, and always fabrication). Closes: *optimization hands you the plan; Monte Carlo tells you how much to trust it.*

---

## The graphical method (Async 2, part 2) — recorded 2026-08-06

**The big ideas:** every constraint is the equation of a line · shade with a **test point**, never a guess · the **feasible region** is the leftover white space · the **corner point property** collapses millions of candidates into five · solve the hard corners by scaling-and-subtracting · plug and chug · and the hard ceiling at two decision variables.

### Notebook 5 · `4_Graphical/BigIdeas_Graphical.ipynb` → `a_GraphicalMethod_Maximize.ipynb`

**Video 9 — Welcome / intro to the graphical method**
The second stop on the optimization journey. Recap of what brute force did (nested loops, incumbent, 10 million combinations, completely transparent and completely slow), then the pitch: write the constraints as **lines on a graph**, and the interesting solutions live at the *extreme values* of the feasible region. Ten million candidates become five.

**Video 10 — Flair's furniture intro / writing the mathematical model**
The word problem: tables and chairs, carpentry and painting hours, a demand ceiling on chairs and a floor on tables. Work out loud through *what am I maximizing*, *what do I get to decide*, then write $Max\ Z = 7T + 5C$ and every constraint underneath it. Ends on the grade-school reveal: strip the inequality and $3T + 4C = 2400$ **is the equation of a line** — so we're going to Flatland to draw it. Includes the "use your own neural network and do it on paper" pitch.

**Video 11 — Draw the constraints on the graph**
Start with the end in mind (show the finished plot), then build it from scratch. Easy constraints first ($C \le 450$, $T \ge 100$ — flat lines), then the two-variable ones by setting each variable to zero: carpentry gives $(0,600)$ and $(800,0)$. The **test point** trick — try $(1,1)$, see if the inequality holds, shade the other side. Dave literally grabs a piece of paper on camera. Exam advice: bring a ruler, label every constraint.

**Video 12 — The feasible region / corner points / intersection of constraints** *(8:22)*
The heart of it. The feasible region is the unshaded space; the optimum is **at a corner**, because anything inside is a suboptimal linear combination. Three of the five corners you read straight off the axes. The other two need algebra — scale, subtract to cancel a variable, back-substitute — giving $(200, 450)$ and the hard one, $(320, 360)$. Plug and chug: **\$4,040** wins. Plus the teaser that the objective climbs around the region and then falls off — *"I'll pay that off later in the Simplex video."*

### Notebook 6 · `4_Graphical/b_GraphicalMethod_Minimize.ipynb`

**Video 13 — Finding the corner points and evaluating them in a minimization problem** *(3:43)*
Same machinery, opposite direction — the corner point property doesn't care. Turkey feed: solve the three interesting corners, evaluate $Min\ Z = 0.10A + 0.15B$, and land on **\$0.78 per turkey** at 4.2 bags of A and 2.4 of B. Closes on the judgment lesson: the trail-mix optimizer that returns coconut flakes and two raisins, and the furniture plan that makes zero chairs. **Optimal is not the same as sensible.**

### Notebook 7 · `4_Graphical/c_GraphicalMethod_Redundant.ipynb` + `d_GraphicalMethod_Infeasible.ipynb`

**Video 14 — Infeasible constraints and redundant constraints** *(2:44)*
The two edge cases, both obvious in 2-D. Flip the table constraint to a maximum and carpentry and painting stop mattering — **redundant**. Push it to $T \ge 600$ and the feasible region vanishes entirely — **infeasible**, which is the error message students will meet most often later, and it means your constraints are fighting each other.

### Notebook 8 · `4_Graphical/g_GraphicalMethod_Wyndor.ipynb`

**Video 15 — Wyndor example with graphical method** *(3:02)*
The Rosetta Stone closes its second loop. Same problem you brute-forced, now drawn: pick which variable goes on which axis, plot the two single-variable constraints as flat lines, solve the slanted one by intercepts, find the corners, and evaluate $Max\ Z = 3000x_1 + 5000x_2$. Answer: **(2, 6) for \$36,000** — exactly what 1,681 brute-force combinations produced.

---

## Reference notebooks (no video — read on your own)
Two more edge cases live in the folder as self-study. They follow the same recipe, so you can work them yourself:
- **Alternate optimal solutions** — `4_Graphical/e_GraphicalMethod_AlternateOptimalSolutions.ipynb` — when the objective line is parallel to a binding constraint, an entire *edge* is optimal, not one point.
- **Unbounded solutions** — `4_Graphical/f_GraphicalMethod_UnboundedSolutions.ipynb` — when the feasible region runs off to infinity in the direction you're optimizing.
- **Practice problems** — `4_Graphical/GraphicalMethod_PracticeProblems_Advanced.ipynb`

## Coming next
**Simplex** — the algebraic extension of the graphical method, walking the same corners in any number of dimensions (objective row on the **bottom**). Notebooks in `5_Simplex/`; that's Async 3.

## Also in the folder
- `Introduction to Optimization_DW.ipynb` (+ blank twin) — the original long-form version of the Veerman material; `The Brute Force Method.ipynb` is the polished lecture cut.
- `BruteForce_Wyndor Glass_blank.ipynb`, `a_GraphicalMethod_Maximize_guided_blank.ipynb` — blank twins for students.
- `Week4_MCRefresh_BruteForce.ipynb` — the live-class driver from Fall 2025.

---

*Companions: [Module2_Skills.md](https://github.com/drdave-teaching/OPIM5641-notebooks/blob/main/Module2_Skills.md) · [Module2_Talking_Points.md](https://github.com/drdave-teaching/OPIM5641-notebooks/blob/main/Module2_Talking_Points.md) · [Working in this Course](https://github.com/drdave-teaching/OPIM5641-notebooks/blob/main/Module1_Working_in_this_Course.md)*
