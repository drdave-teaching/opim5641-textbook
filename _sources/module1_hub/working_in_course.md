# Working in this Course — Colab, GitHub, and Saving Your Work

**OPIM 5641 - Business Decision Modeling · Dr. Dave Wanik · University of Connecticut**

Five minutes now saves you a semester of "wait, where did my work go?" Here's the whole workflow.

---

## 1 · Where everything lives

- **Notebooks (this repo):** [github.com/drdave-teaching/OPIM5641-notebooks](https://github.com/drdave-teaching/OPIM5641-notebooks) - every lecture notebook, organized by topic folder. Public - no GitHub account needed just to *view*.
- **The ebook:** [drdave-teaching.github.io/opim5641-textbook](https://drdave-teaching.github.io/opim5641-textbook/) - chapter prose + links back to the notebooks.
- **Module guides:** [Skills](https://github.com/drdave-teaching/OPIM5641-notebooks/blob/main/Module1_Skills.md) · [Talking Points](https://github.com/drdave-teaching/OPIM5641-notebooks/blob/main/Module1_Talking_Points.md) · [Video Guide](https://github.com/drdave-teaching/OPIM5641-notebooks/blob/main/Module1_Video_Guide.md) - what you can do, what you should understand, what each video covers.
- **HuskyCT:** announcements, gradebook, and the weekly schedule. When in doubt, start there.

## 2 · Open a notebook (10 seconds)

Every notebook has an **"Open in Colab" badge** at the top. Click it → the notebook opens in Google Colab, running against the live version in the class repo. All you need is a free Google account - no installs, ever.

First time you run a cell, Colab shows: **"Warning: This notebook was not authored by Google."** That's expected - it's loaded from our GitHub. Click **Run anyway**.

## 3 · Run it

**Runtime → Run all** (or Ctrl+F9). Every course notebook is built to run top-to-bottom with zero setup - data loads from stable URLs, nothing to upload, no Drive mounting. If a fresh notebook does NOT run top-to-bottom cleanly, that's a bug - tell me.

## 4 · Save your work - THE part people get wrong

Here's the catch: the notebook you opened is **read-only against the class repo**. You can edit and run all you like, but if you close the tab, *your changes are gone*. Colab even warns you - "Save in GitHub to keep changes." So before you do real work:

**Option A - Save a copy in Drive (easiest):**
`File → Save a copy in Drive`. Done - your copy lives in your Google Drive under "Colab Notebooks." Good enough for homework-along.

**Option B - Save a copy in GitHub (do this - it's the habit that pays):**
1. Create a **free GitHub account** ([github.com/signup](https://github.com/signup)) if you don't have one.
2. Create one repository for the course - call it **`opim5641-work`** (public or private, your call).
3. In Colab: `File → Save a copy in GitHub`. The first time, GitHub asks you to authorize Colab - one click, one time.
4. Pick your `opim5641-work` repo, write a commit message ("finished EDA notebook + on-your-owns"), check **"Include a link to Colab"** so your copy stays one-click runnable, and save.

That's a *commit* - a timestamped snapshot. Do it every work session and you get version history for free, a portfolio you can show an employer, and zero "my laptop died" stories.

**Why GitHub and not just Drive?** Because the final project in this course IS a GitHub repo, and because in 2026 "I keep my analysis in version control" is table stakes for every data job. Start the habit in week 1 when the stakes are low.

## 5 · The rhythm of the course

- **Async weeks:** watch the videos, run the notebooks alongside, do the **On your own** prompts in YOUR copy, save to your repo.
- **Studio weeks (in person):** bring a laptop that can open Colab. We build on the async - the studio assumes you've watched.
- **Weekly handwritten check:** ~15 minutes, by hand, drawn from the week's core skill (corner points, a percentile read, one pivot...). The by-hand worksheets in [opim-math](https://github.com/drdave-teaching/opim-math) are the practice bank.

## 6 · When something breaks

| Symptom | Fix |
|---|---|
| "Not authored by Google" warning | Expected. **Run anyway.** |
| Runtime disconnected / variables gone | Colab idles out. **Runtime → Run all** again - notebooks are built for it. |
| My edits disappeared | You edited the class copy without saving. See §4 - save a copy FIRST, then work. |
| A data URL won't load | Tell me - stable URLs are my job, not yours. |
| Cell order confusion (`NameError`) | You ran cells out of order. **Runtime → Restart and run all.** |

*Pssst... you also have Claude, ChatGPT, or Gemini at your side. Use them to explain code and debug - then make sure YOU can explain what the code does. The understanding is the deliverable; the tools are the accelerant.*
