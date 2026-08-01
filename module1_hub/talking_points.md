# Module 1 Talking Points — The Theory You Should Be Able to Explain

**OPIM 5641 - Business Decision Modeling · Dr. Dave Wanik · University of Connecticut**

These are the *ideas* behind Module 1 - the things I say out loud in the lectures that you should be able to explain to a classmate (or an interviewer) without opening a notebook. Skills are what you can do; this sheet is what you *understand*. If you can teach each of these in two sentences, you've got the module.

---

## 1 · EDA and working with real data

**The EDA loop.** Every analysis in this course - and most of your career - follows one loop: **question → load → clean → describe → visualize → insight.** You never skip to the pretty chart. The order exists because each step protects the next one.

**Real data never arrives clean - and that's not an annoyance, it's the job.** The two "problems" we hit in week one (a website that blocks naive scrapers, phantom summary rows inside a table) weren't bad luck. Cleaning IS analytics. Budget most of your time for it.

**A 403 is the server saying "I see you, and no."** Websites detect bot-like requests by their missing User-Agent. Identifying yourself with a header is both the fix and a lesson: scraping is a conversation with someone else's server - be polite, and expect the rules to change under you (this exact call worked fine a couple of years ago!).

**Phantom rows: the most dangerous errors don't crash.** Wikipedia's county table quietly includes a whole-state row, a United States row, and a blank. Nothing errors - your `.describe()` is just *wrong* (a max "county" population of 311 million!). Lesson: validate row counts against reality (Massachusetts has 14 counties - why do I have 16 rows?).

**Filter by exact match, not by "contains."** `str.contains('New York')` would delete New York *County* (Manhattan!) along with New York state. Precision in your filters is precision in your answers.

**What's missing matters as much as what's there.** Wikipedia's Massachusetts table simply omits Nantucket - one of the wealthiest places in America. The `.describe()` never told us; the **map** did, as a hatched hole. Always ask what *should* be in the data and isn't.

**Codes vs. names (FIPS).** Government data ships with code columns (`STATEFP = '25'`) alongside names for a reason: names are for humans and easy to misspell ("Massachussets" returns zero rows, silently); codes are unambiguous. Explore with names, join on codes.

**Join keys are guilty until proven innocent.** Before any merge, print `.unique()` on both sides. When a merge comes back short, the key is almost always the culprit - different spellings, stray suffixes ("Capitol Region" vs "Capitol"), or a vintage mismatch (Connecticut retired its counties in 2022; we matched Wikipedia's legacy counties to the 2020 boundary file on purpose).

**A shapefile is just a table with a geometry column.** Nothing mystical - 3,235 rows, one per US county, EDA it like anything else. A choropleth is a merge plus a color scale.

**Insight = one sentence, backed by a number, that a smart non-technical person would care about.** "Norfolk County's per capita income is nearly double Hampden's" is an insight. "Living near Boston causes higher income" is an **over-claim** - EDA shows association, never causation.

**For loops pay off when structure repeats.** Six states, one loop - but only because we found the part that repeats (the county summary table) and taught the code to *find* it. Half of scraping at scale is discovering what actually repeats.

---

## 2 · Distributions

**A distribution is a shape of possibility.** Instead of one number ("the return will be 8%"), a distribution says what's likely, what's rare, and how wrong you might be. Choosing to model with a distribution is choosing to be honest about uncertainty.

**Parameters ARE the shape.** Normal: `loc` (mean) centers it, `scale` (sd) widens it. Triangular: left/mode/right literally draw the triangle - stretch `right` from 20 to 200 and watch the tail go. Uniform: everything between low and high is equally likely. You should be able to sketch each from its parameters alone.

**Match the distribution to the real-world quantity.**
- **Normal** - sums of many small effects: returns, demand, measurement noise.
- **Triangular** - expert judgment: "best case / most likely / worst case." The workhorse of business modeling when you have opinions but not data.
- **Uniform** - genuine "no idea between these bounds."
- **Binomial / Poisson / integer-uniform** (appendix) - *counts*: successes out of n, arrivals per hour, die rolls.

**Percentiles are positional truth.** The 10th percentile is the value with 10% of outcomes at or below it. They describe the extremes far better than the mean does - and the extremes are where risk lives.

**The CDF is the percentile machine.** The standard picture puts the value on x and cumulative probability on y; read across and down and you can answer "what's the chance of X or less?" for free. (Its mirror image, the quantile function, answers the reverse: give a probability, get a value.)

**Seeds pin randomness.** `np.random.seed()` makes the next draw reproducible - same seed, same "random" number. Two different-looking formulas that share a seed and land on the same number are *provably* the same distribution. Seed your demos and your debugging. **Never seed inside a simulation loop** - you'd hand every trial identical returns and your 10,000 futures would collapse into one.

---

## 3 · For loops (the engine of simulation)

**Three rungs on the ladder.** (1) *Repeat*: the loop variable takes each value, the indented block runs once per value. (2) *Accumulate*: a variable created **outside** the loop survives every pass - that's how money carries from year to year. (3) *Nest*: a loop inside a loop; for every outer pass, the inner loop runs completely. Our simulations are exactly rung 3: **outer = trials, inner = years.**

**The handoff is the whole game.** `current_value = (current_value + contribution) * rate` then next year starts from that value. One line turns 30 disconnected calculations into a career.

**`np.arange(start, stop, step)` excludes the stop.** `np.arange(0,5,1)` is 0,1,2,3,4. Every off-by-one bug you'll ever write is hiding in that sentence.

**Predict before you run.** With nested loops especially - trace the values by hand first, then run to check. (No credit for running first and "predicting" second.)

---

## 4 · Monte Carlo simulation

**The whole recipe in one line:** *describe uncertainty with a distribution → get ONE trial right → loop it thousands of times → read the distribution of outcomes.* Every simulation in this course is this pattern wearing a different costume - retirement savings, cell-phone profits, and beyond.

**Why simulate instead of multiply averages?** Because outcomes have *shape*. Average return × 30 years gives one number and hides the risk. Ten thousand simulated careers give you the spread, the skew, the tail - the stuff decisions actually hinge on.

**Write your assumptions down BEFORE you code.** Horizon, starting balance, contributions, the distribution and its parameters, what you're ignoring (taxes, fees, inflation). A model's assumptions aren't fine print - they ARE the model. Change one and the answer changes; that's not a bug, that's what a model is. Your job is to make them defensible and visible.

**You are the modeler - parametric vs. nonparametric is your call.** Parametric: assume a named distribution (Normal with mean 7.86%, sd 19%) - smooth, lets you reason beyond history. Nonparametric: resample actual history with replacement - no distributional assumption, but you can never draw a year worse than the worst year that already happened. Neither is automatically right; your judgment makes the model believable.

**Mean vs. median: the skew story.** Retirement outcomes are right-skewed - a minority of lucky compounding runs drag the **mean** far above the **median**. When you report to a client, lead with the median and the percentiles, not the mean. (The spaghetti plot is the picture of this: histogram = the destination, spaghetti = the journey.)

**Percentiles are client language.** "There's a 5% chance you retire with less than \$X, and a 5% chance with more than \$Y" beats any single point estimate. Nobody plans a life - or a factory - on the average.

**Risk questions the output can answer directly** (the cell-phone factory): expected profit (the mean), **probability of a loss** (share of trials below zero), maximum loss (the worst trial), and the full percentile view. Counting bad trials out of 10,000 IS estimating a probability.

**Silent bugs are the real bugs.** A simulation that skips the \$100K starting balance runs perfectly and produces confident, wrong answers. There's no error message for "your assumptions and your code disagree" - only the habit of checking one against the other.

**Compare fairly: change one thing at a time.** Our parametric and nonparametric runs also differed in contribution schedule - so the comparison isn't pure. When you A/B two models, vary one assumption per comparison or you can't attribute the difference.

---

## The bridge to the rest of the course

Monte Carlo tells you what *might happen* under uncertainty. Optimization - where we're headed next - tells you what you *should do*. Different tools, different questions: first we simulate to understand the world, then we optimize to act in it. When you have data, you explore it (Module 1). When you don't, you simulate it (Module 1). When you must *decide* - that's Module 2 and beyond.
