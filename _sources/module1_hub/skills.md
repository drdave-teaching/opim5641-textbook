# Module 1 Skills Sheet — What You Can Do Now

**OPIM 5641 - Business Decision Modeling · Dr. Dave Wanik · University of Connecticut**

After the Module 1 lectures and notebooks, these are the skills you own. Not "watched a video about" - *own*. Every one of these is something you did with your own hands in a notebook, and every one of them shows up in real analytics jobs. Go down the list and check them off - if one feels shaky, the notebook to revisit is listed right there.

---

## 🐍 Python & Colab fundamentals
*Notebooks: `1_EDA_Intro/Practical_Python_Basics.ipynb` · `1_EDA_Intro/DataTypes_Tables_Wrangling.ipynb`*

- ☐ Open any course notebook in Google Colab from GitHub and run it top to bottom (**Runtime → Run all**)
- ☐ Save your own working copy (File → Save a copy in GitHub / in Drive) so your work survives
- ☐ Comment every line of code with *why* it's there - your future self is your most important reader
- ☐ Work with Python's core types (numbers, strings, booleans, lists) and know that Python counts from **zero**
- ☐ Load a table into a pandas DataFrame and poke at it with `.head()`, `.info()`, `.shape`, `.describe()`

## 🌐 Scraping real data from the web
*Notebook: `1_EDA_Intro/EDA_Wikipedia_Income.ipynb` (Step 1)*

- ☐ Scrape a live Wikipedia table with `requests` + `pd.read_html()`
- ☐ Diagnose an **HTTP 403 Forbidden** and fix it by sending a **User-Agent header** - and explain *why* the naive call fails (bot detection)
- ☐ Parse ALL the tables on a page, inspect their shapes, and pick the right one by looking - never by guessing
- ☐ Explain the difference between a status code of 200 and 403 without looking it up

## 🧹 Cleaning data you didn't create
*Notebook: `1_EDA_Intro/EDA_Wikipedia_Income.ipynb` (Step 2)*

- ☐ Hunt down **phantom rows** - summary lines (a whole-state row, a United States row, blanks) hiding inside a table - and show how they skew `.describe()` before you delete them
- ☐ Filter rows by **exact name matching** and explain why sloppy `str.contains()` matching is dangerous (it would delete New York County along with New York state!)
- ☐ Convert dollars-stored-as-text (`\$46,920`) into real numbers with `.str.replace()` + `pd.to_numeric()`
- ☐ Count your NaNs after coercion so you know exactly what you threw away
- ☐ Check `dtypes` before doing math - and know what happens if you don't

## 📊 Describing & visualizing
*Notebook: `1_EDA_Intro/EDA_Wikipedia_Income.ipynb` (Steps 3-4)*

- ☐ Produce and *read* a five-number summary (`.describe()`)
- ☐ Rank observations with `.sort_values()` and answer "who's on top, who's on the bottom?"
- ☐ Build a sorted horizontal bar chart - and explain why it beats a histogram when you have 13 labeled rows
- ☐ Build a scatterplot with a **log scale** and explain when and why you need one
- ☐ Put titles and axis labels on every plot (unlabeled plots don't count - here or at work)

## 🗺️ Mapping (geospatial basics)
*Notebook: `1_EDA_Intro/EDA_Wikipedia_Income.ipynb` (Map it + Apply to Connecticut)*

- ☐ Load a Census Bureau shapefile straight from a URL with `geopandas` and treat it like any other table (it's rows + a geometry column)
- ☐ Subset a national file to one state **two ways** - by FIPS code (`STATEFP == '25'`) and by name (`STATE_NAME == 'Massachusetts'`) - and explain the tradeoff (names are readable; codes can't be misspelled)
- ☐ Check join keys with `.unique()` on BOTH sides *before* merging
- ☐ Merge data onto shapes and build a **choropleth** map, colored by a numeric column
- ☐ Use `how='left'` + missing-data hatching so gaps in your data show up as visible holes (hello, Nantucket) instead of silently vanishing
- ☐ Repeat an entire scrape-clean-map pipeline for a second state (Connecticut) - including knowing that CT's legacy counties need the 2020 boundary file

## 🎲 Distributions
*Notebook: `2_MonteCarlo/Intro_to_Distributions.ipynb`*

- ☐ Draw samples from the **normal**, **triangular**, and **uniform** distributions with numpy - one value or 10,000
- ☐ Match a distribution to a real-world quantity (a stock return, a best/most-likely/worst estimate, a "completely unknown between two bounds")
- ☐ Use keyword arguments (`loc=`, `scale=`, `size=`) and explain how scrambled *positional* arguments fail silently
- ☐ Turn the knobs (mean, sd, left/mode/right, low/high) and predict how the shape changes before you plot it
- ☐ Visualize a sample with a KDE plot and a histogram, and mark the mean/percentiles on it
- ☐ Read percentiles off a **CDF** - and recognize the standard CDF orientation (value on x, cumulative probability on y)
- ☐ Reach for the appendix distributions (binomial, uniform integers, Poisson) when the quantity is a *count*

## 🌱 Seeds & reproducibility
*Notebooks: `2_MonteCarlo/Intro_to_Distributions.ipynb` · `Big_Ideas_MC_Simulation.ipynb`*

- ☐ Use `np.random.seed()` to make a random cell reproduce the same draw every run
- ☐ Prove that two different-looking expressions draw from the same distribution (same seed → same number)
- ☐ Explain why you seed a *demo* but **never seed inside the simulation loop** - a seed inside the loop collapses your 10,000 futures into one

## 🔁 For loops (the engine)
*Notebook: `2_MonteCarlo/Intro_to_Distributions.ipynb` (3-example ladder)*

- ☐ Loop over a list or `np.arange()` range - and remember the stop value is NOT included
- ☐ Use the **accumulator pattern**: a variable created *outside* the loop that survives and grows across every pass
- ☐ Trace a **nested loop** by hand and predict its output BEFORE running it (outer = trials, inner = years)
- ☐ Recognize the handoff line (`current_value = ...` → next iteration) as the thing that turns 30 separate calculations into one 30-year career

## 🎰 Monte Carlo simulation
*Notebooks: `2_MonteCarlo/Intro_to_Distributions.ipynb` (Simple MC) · `Big_Ideas_MC_Simulation.ipynb` · `CellPhone_Manufacturing_MC.ipynb`*

- ☐ State your **assumptions in a table before you code** (horizon, starting value, contributions, the distribution and its parameters, what you're ignoring)
- ☐ Get ONE trial right, then wrap it in a loop and run 10,000
- ☐ Build the retirement simulation: yearly contribution + random growth + balance handoff, 10,000 careers
- ☐ Build the cell-phone profit simulation: combine FOUR uncertain inputs (triangular price, uniform cost, normal quantity, normal fixed costs) into one profit distribution
- ☐ Choose between **parametric** sampling (draw from a named distribution) and **nonparametric** sampling (resample real history with `.sample(replace=True)`) - and defend the choice
- ☐ Analyze the output like a dataset: `.describe()`, histogram, `.quantile()`
- ☐ Draw a **spaghetti plot** of every simulated path with median / mean / 5th / 25th / 75th / 95th percentile overlays
- ☐ Answer real risk questions from the output: expected profit, **probability of a loss**, maximum loss, the percentile view
- ☐ Explain why the **mean lands above the median** in a right-skewed outcome distribution - and why you lead with the median and percentiles when you present

---

## The one-sentence version

> **You can take data you don't control (scraped, messy, or missing), make it trustworthy, and when there's no data at all - simulate it, 10,000 times, and tell a decision-maker what might happen and how bad it could get.**

That's not a homework skill. That's the job.
