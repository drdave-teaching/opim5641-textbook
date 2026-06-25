# OPIM 5641 — *Business Decision Modeling: Optimization with Python* (textbook)

A casual-but-rigorous, code-first **optimization textbook** built from Dr. Wanik's OPIM 5641
lecture transcripts and Pyomo course notebooks.

## View it (local, nothing public)
```
C:\Users\dww05002\kaltura\OPIM5641-textbook\_build\html\index.html
```

## Rebuild after edits
```bash
python -c "import sys; from jupyter_book.cli.main import main; sys.argv=['jupyter-book','build','.']; main()"
```

## Chapters
1. **Foundations** — building blocks, brute force, Monte Carlo
2. **Linear Programming** — graphical method & Simplex
3. **LP in Pyomo & Sensitivity Analysis** — shadow prices, reduced costs
4. **Nonlinear Optimization** — facility location, portfolio, regression-as-optimization
5. **Network Optimization** — min-cost flow, assignment, shortest path, transshipment
6. **Integer Programming** — set covering, activation variables, logical constraints

Weaves transcript narrative + real **Pyomo** code (from `OPIM5641`) + math callouts (MathJax).
A `.github/workflows/deploy.yml` is included to publish to GitHub Pages (public repo) when ready.
**Kept LOCAL per request.** Sources: `opim5641-transcripts/scripts` (57), code `OPIM5641` (93 nb).
