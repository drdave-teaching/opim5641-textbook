# Module 1 Video Guide — What Each Video Covers

**OPIM 5641 - Business Decision Modeling · Dr. Dave Wanik · University of Connecticut**

Eleven videos, four notebooks, one arc: *when you have data, you explore it - when you don't, you simulate it.* Watch in order; each video drives one stretch of its notebook.

---

## Notebook 1 · `1_EDA_Intro/EDA_Wikipedia_Income.ipynb`
**The big ideas:** the EDA loop (question → load → clean → describe → visualize → insight) · scraping politely (the 403 / User-Agent story) · phantom rows that silently skew statistics · dollars stored as strings · counties vs. towns as units of analysis · maps as EDA (choropleths, and missing data made visible) · for loops that scale one state's code to six.

**Video 1 — Intro EDA with Wikipedia** *(3:51)*
The setup. Why Wikipedia's income-by-county table is a great first dataset: it's real, it's slightly tricky to access in 2026, and it's just messy enough. Geography refresher (towns → counties → state) and a preview of the two traps waiting in the data - delimiters that make numbers act like strings, and rows that aren't counties at all.

**Video 2 — Cleaning up quasi-clean data (numbers hiding as strings)** *(7:55)*
The scrape and the cleanup, live. `requests` with a User-Agent header (why the naive call 403s), parsing ALL the tables and picking the right one, the phantom rows highlighted in red (the Massachusetts row, the United States row with 311 *million* population, the blank) and what they do to `.describe()` before we delete them, then `$`/`,` stripping and `pd.to_numeric`.

**Video 3 — Make a map of MA data and CT data** *(9:00) · intro to geopandas*
Now that the dtypes are right, the payoff: sorted bar chart (Norfolk ≈ 2× Hampden), income-vs-population scatter (with a teaser: fitting that curve IS an optimization problem - coming later in the course), then geopandas: the shapefile as a 3,235-row table with a geometry column, subsetting by `STATEFP` vs `STATE_NAME`, merging, and choropleths - including the hatched Nantucket hole where Wikipedia has no data. Repeat for Connecticut with the 2020 boundary file (CT retired its counties!).

**Video 4 — Apply it!** *(5:29)*
The scale-up and the philosophy. One for loop runs the whole scrape-clean pipeline for six states (the URL is the only thing that changes; the code *finds* the county table on each page). Plus the teaching-in-2026 message: with Claude/ChatGPT/Gemini at your side you can go bigger, faster - as long as you keep a real understanding of what the code is doing.

---

## Notebook 2 · `2_MonteCarlo/Intro_to_Distributions.ipynb`
**The big ideas:** a distribution is a recipe that generates numbers with a personality · parameters ARE the shape (loc/scale; left/mode/right; low/high) · the empirical rule and percentiles as the language of risk · keyword vs. positional arguments · seeds and reproducibility (demo yes, inside the loop never) · the for-loop ladder (repeat → accumulate → nest) · your first full Monte Carlo simulation.

**Video 5 — What is a distribution??** *(5:47)*
The concept opener. Dave's consulting confession: half of data science is knowing what to do when you *don't* have data - like placing 10,000 storm outages on a wind-risk map. A distribution = a collection of numbers *with a flavor*, a recipe with knobs. The normal distribution and its mean/sd knobs, the empirical rule (68/95/~all within 1/2/3 sd), and why percentiles - not means - are how you describe risk in ANY distribution.

**Video 6 — Intro to creating your own dataset** *(10:31)*
From concept to keyboard. The bridge from the EDA videos ("an hour before the meeting, no data, you need a defensible estimate"), discrete vs. continuous, why most real-world data is NOT normal, mean/sd as the normal's reconstruction kit, percentiles as the engineering alternative - then `np.random.normal` hands-on: reading the numpy documentation (why the mean is called `loc`), drawing 3 values, then 10,000, and watching the KDE become the bell curve.

**Video 7 — Sampling from continuous distributions** *(9:03)*
The mechanics, sharpened. Random seeds (seed 5641 - the course number - makes randomness repeatable; use for debugging and demos, skip when you want genuine spread), keyword vs. positional arguments and how scrambled positions fail *silently*, the empirical rule confirmed by clicking the cell repeatedly, then the triangular distribution (continuous but CENSORED between bounds - perfect when the manufacturer knows costs stay between \$20 and \$26) and the uniform ("a candy bar" - every value between the endpoints equally likely).

**Video 8 — Some other useful distributions** *(3:42)*
The appendix tour, fast. Triangular recap, uniform recap, then the discrete crowd: binomial (flipping 10 quarters - you *expect* 5 heads but randomness says otherwise; n and p; the normal approximation as n grows), uniform integers, and Poisson (lambda morphs the shape; the classic for counts and waiting times).

**Video 9 — Intro to for loops** *(10:12) · transcript pending*
The engine of Monte Carlo, taught as a three-rung ladder from the notebook: (1) *repeat* - the loop variable takes each value in a list or `np.arange` (stop value excluded!); (2) *accumulate* - a variable created OUTSIDE the loop survives every pass, which is how money carries from year to year; (3) *nest* - a loop inside a loop, outer = trials, inner = years, with the "great exam question... what is c?" trace-it-by-hand challenge.

**Video 10 — Intro to MC simulation / retirement** *(9:31) · transcript pending*
The first full simulation - the retirement nest egg. State the assumptions out loud (\$2,500/month, 30 years, returns ~ Normal(8%, 17%), the balance handoff), get ONE year right, wrap it in the double loop for 10,000 careers, then read the output like a dataset: describe, the right-skewed histogram, and the percentile table that answers "how good could it get - and how bad?"

---

## Notebook 3 · `2_MonteCarlo/CellPhone_Manufacturing_MC.ipynb`
**The big ideas:** combining SEVERAL uncertain inputs into one answer · matching each input to its right distribution · profit = (price − cost) × quantity − fixed costs · answering real risk questions: expected profit, probability of a loss, maximum loss, the percentile view.

**Video 11 — MC Simulation / cell phones** *(11:58) · transcript pending*
The business capstone of the block (Powell Ch. 14 flavor): a consumer-electronics firm makes battery rechargers, and every input is uncertain - unit price (triangular), unit cost (uniform), quantity sold (normal), fixed costs (normal). Build the profit equation, run 10,000 factories, and answer the four questions a CFO actually asks: expected profit, the probability we LOSE money, the worst case, and the full percentile spread.

---

## Not yet recorded
**Video 12 candidate — Parametric vs. Nonparametric** · driver: `2_MonteCarlo/Parametric_vs_Nonparametric_MC.ipynb` (NEW - the focused head-to-head: same assumptions, same seed, same 10,000 trials, ONE line of code different; ~95 years of real S&P history feeds both; spaghetti + overlaid histograms; centers agree, tails diverge - and the when-to-choose-which verdict). The fuller `Big_Ideas_MC_Simulation.ipynb` remains as the deep-dive/studio companion.

---

*Companions: [Module1_Skills.md](https://github.com/drdave-teaching/OPIM5641-notebooks/blob/main/Module1_Skills.md) (what you can do now) · [Module1_Talking_Points.md](https://github.com/drdave-teaching/OPIM5641-notebooks/blob/main/Module1_Talking_Points.md) (the theory you should be able to explain).*
