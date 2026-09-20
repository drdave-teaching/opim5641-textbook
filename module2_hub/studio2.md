# Studio 2 — Sep 23 · Feel the Explosion + Messy Constraints

:::{admonition} 🚧 Draft plan
:class: note
The run-of-show below is the working plan; details may shift before Sep 23. The materials links go live the week of the studio.
:::

The in-person half of Module 2. You've watched brute force grind, drawn feasible regions, and pivoted tableaus — tonight you *feel* why each method exists. Bring a laptop, **a pencil and a ruler**, and your GitHub repo habit from Studio 1.

## The walk-in ritual · Math check (~10 min)

From this studio on, the handwritten math check is how we open: sit down, work it by hand, hand it over. This week's check is a short loop trace: read a nested `for` loop and write down exactly what it prints. It is the same loop shape we use minutes later to search every production plan.

## Part 1 · One problem, two methods (~60 min)

We take **Flair's Furniture** — the tables-and-chairs example from the M2.2 videos — and solve it twice.

First, on paper with your partner: name the pieces. What are the **decision variables**? What is the
**objective function**, and what do its **coefficients** actually mean? Write every **constraint** with its
units, and don't forget non-negativity. Every LP for the rest of the course has these same parts; only the
story changes.

Then the same problem, two ways:

1. **Brute force.** A nested loop over every production plan — 481,401 of them — keeping the best legal one.
   It is the same loop shape you traced by hand in the warm-up, with something useful inside.
2. **The graphical method.** Draw the four constraints, shade the feasible region, and evaluate the five
   **corner points**.

Both answer **320 tables and 360 chairs, $4,040**. One checked half a million plans; the other checked five.
That contrast *is* the lesson: the corner-point property means the winner can only ever be at a corner.

The closing question writes itself: the graphical method only works with **two** decision variables.
What would you do with ten products, when there is no picture to draw? That gap is exactly what the
Simplex method fills.

📓 Notebook: `studio2/Studio2_TwoWays_blank.ipynb` in the course notebooks repo.

## Part 2 · Messy constraints (~40 min)

Real problems arrive with rules that fight. In pairs, you get a formulation with something wrong in it — a redundant constraint doing no work, a pair of constraints that leave no feasible region, an unbounded direction — and your job is the diagnosis: *which rule is the problem, and what would you say in the meeting?* This is the graphical method as a debugging tool, which is how you'll actually use it after this course.

## Wrap (~10 min)

Save your work to your `opim5641-work` repo (the loop from Studio 1 — it's a habit now). Preview of the next async: **the Simplex method** — the graphical picture becomes algebra, and the corners get checked for you.

## The weekly handwritten check

Practice worksheets with fully-worked keys live in [opim-math](https://github.com/drdave-teaching/opim-math) — the graphical-method and simplex sheets are the ones to drill for this stretch of the course.

*The hook: you now know three ways to solve an LP by hand, and exactly what each one costs. Next module you hire a machine — and you'll know precisely what it's doing for you.*
