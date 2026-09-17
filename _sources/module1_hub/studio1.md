# Studio 1 — Sep 9 · Data ER + Retirement Monte Carlo

The in-person half of Module 1. The async carried the mechanics; the studio is where you apply them to problems nobody pre-chewed for you — the whole course thesis in one evening: *when you have data, explore it; when you don't, simulate it.* Bring a laptop that opens Colab, and have your GitHub repo ready (see [Working in this Course](working_in_course.md)).

📄 **[Tonight in 20 steps (PDF)](https://raw.githubusercontent.com/drdave-teaching/OPIM5641-notebooks/main/studio1/OPIM5641_Studio1_Tonight_in_20_Steps_BW.pdf)** — the one-page handout we follow in studio.

## Part 1 · Data ER: PPP loans in Connecticut (~40 min, pairs)

117,888 real SBA Paycheck Protection Program loans made to Connecticut businesses — public data, dirt included: missing industry codes, suspicious job counts, cities spelled three ways. Triage → describe the money → who got it, where, and how many dollars per job. Deliverable: **three findings**, each one plot or table plus two sentences, saved to YOUR repo.

- Starter: [Studio1_PPP_DataER_blank.ipynb](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/studio1/Studio1_PPP_DataER_blank.ipynb) · [GitHub](https://github.com/drdave-teaching/OPIM5641-notebooks/blob/main/studio1/Studio1_PPP_DataER_blank.ipynb) · [filled version](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/studio1/Studio1_PPP_DataER.ipynb) to catch up from
- The patient: [ppp_ct.csv](https://github.com/drdave-teaching/OPIM5641-notebooks/blob/main/studio1/ppp_ct.csv) *(loads automatically from the starter)*
- 📖 [Data dictionary](https://github.com/drdave-teaching/OPIM5641-notebooks/blob/main/studio1/ppp_data_dictionary.md) — official SBA descriptions for all 53 columns, plus which ones to distrust and why missing ≠ zero

## Part 2 · Retirement Monte Carlo (~35 min)

Your balance in 35 years is data you *don't* have. Build the simulation in three escalations — one 35-year path, then 10,000 futures with percentile lines and the spaghetti plot, then the twist: swap `np.random.normal(0.07, 0.20)` for a bootstrap of **98 years of real S&P 500 total returns** (`sp['sp500_total_return'].sample(n=years, replace=True)` — the M1.2 move) and watch what fat tails do to *P(you retire comfortably)*. Finish by answering a life question **with a probability**, not a single number.

- Starter: [Studio1_Retirement_MC_blank.ipynb](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/studio1/Studio1_Retirement_MC_blank.ipynb) · [GitHub](https://github.com/drdave-teaching/OPIM5641-notebooks/blob/main/studio1/Studio1_Retirement_MC_blank.ipynb) · [filled version](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/studio1/Studio1_Retirement_MC.ipynb)
- Real returns: [sp500_annual_returns.csv](https://github.com/drdave-teaching/OPIM5641-notebooks/blob/main/studio1/sp500_annual_returns.csv) — annual S&P 500 total returns 1928–2025, dividends included

## The GitHub habit (twice tonight)

Open the starter from the course repo in Colab → work → **File → Save a copy in GitHub** → your `opim5641-work` repo. Once after Part 1, once at wrap. That one loop — open from GitHub, work, save to *your* repo — is the portfolio habit for the whole course; nothing about branches tonight.

## The handwritten check

**Math Check #1** (California Housing descriptive stats — percentiles, mean vs. median by hand) is due this week: hand your paper in at the studio, or upload your scan to HuskyCT by **Friday, Sept 11**. From Studio 2 onward the math check is the walk-in ritual: sit down, pencil out, hand it over.

*The hook into next module: when you have data, you explore it. When you don't, you simulate it. When you must DECIDE... that's optimization.*
