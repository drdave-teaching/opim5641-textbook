# Studio 2 — Sep 23 · Feel the Explosion + Messy Constraints

:::{admonition} 🚧 Draft plan
:class: note
The run-of-show below is the working plan; details may shift before Sep 23. The materials links go live the week of the studio.
:::

The in-person half of Module 2. You've watched brute force grind, drawn feasible regions, and pivoted tableaus — tonight you *feel* why each method exists. Bring a laptop, **a pencil and a ruler**, and your GitHub repo habit from Studio 1.

## The walk-in ritual · Math check (~10 min)

From this studio on, the handwritten math check is how we open: sit down, work it by hand, hand it over. This week's check draws on Module 2 — expect to formulate a small LP from a word problem and walk the graphical recipe (plot, shade with a test point, corners, plug and chug).

## Part 1 · Feel the Explosion: the Stamford delivery tour (~45 min)

You run deliveries out of UConn Stamford: visit every stop once, come back, drive the fewest miles.
In pairs, on two teams with two different maps: **Team A** heads west (Greenwich, Cos Cob, Port Chester,
Rye, Armonk) and **Team B** heads north and east (Darien, New Canaan, Norwalk, Westport, Ridgefield).
The distances are real driving miles.

1. **On paper:** 3 stops, all 6 orders, find the shortest loop.
2. ✅ **The success:** 5 stops is 120 routes. Brute force is instant and guaranteed to find the best.
3. **The ramp:** add one stop at a time and time it. 10 stops is 3.6 million routes, and you'll wait.
4. ❌ **The wall:** all 12 stops. Estimate before you run: about half an hour. 20 stops: hundreds of thousands of years.
5. **The escape hatch:** always drive to the nearest unvisited stop. Instant, but not the best route. How much worse?

At the wrap the two teams compare: different maps, **same cliff**. The explosion is about *how many*
stops, not *where* they are.

📓 Notebook: `studio2/Studio2_DeliveryTour_blank.ipynb` in the course notebooks repo.

## Part 2 · Messy constraints (~40 min)

Real problems arrive with rules that fight. In pairs, you get a formulation with something wrong in it — a redundant constraint doing no work, a pair of constraints that leave no feasible region, an unbounded direction — and your job is the diagnosis: *which rule is the problem, and what would you say in the meeting?* This is the graphical method as a debugging tool, which is how you'll actually use it after this course.

## Wrap (~10 min)

Save your work to your `opim5641-work` repo (the loop from Studio 1 — it's a habit now). Preview of the next async: **the Simplex method** — the graphical picture becomes algebra, and the corners get checked for you.

## The weekly handwritten check

Practice worksheets with fully-worked keys live in [opim-math](https://github.com/drdave-teaching/opim-math) — the graphical-method and simplex sheets are the ones to drill for this stretch of the course.

*The hook: you now know three ways to solve an LP by hand, and exactly what each one costs. Next module you hire a machine — and you'll know precisely what it's doing for you.*
