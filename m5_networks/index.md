# Chapter 5 — Network Optimization

:::{admonition} 🔗 Notebooks for this chapter
:class: seealso dropdown
Open in Colab and **Runtime → Run all** — data loads from a stable link, nothing to upload.

- **Network Bonner Electronics** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/Networks/0_Network_BonnerElectronics.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5641-notebooks/blob/main/Networks/0_Network_BonnerElectronics.ipynb)
- **Network Transshipment** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/Networks/0_Network_Transshipment.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5641-notebooks/blob/main/Networks/0_Network_Transshipment.ipynb)
- **TSP Pyomo** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/Networks/0_TSP_Pyomo.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5641-notebooks/blob/main/Networks/0_TSP_Pyomo.ipynb)
- **Network Transporting Coal** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/Networks/1_Network_TransportingCoal.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5641-notebooks/blob/main/Networks/1_Network_TransportingCoal.ipynb)
- **Paper Recycling Reduction Flow** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/Networks/1_PaperRecycling_ReductionFlow.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5641-notebooks/blob/main/Networks/1_PaperRecycling_ReductionFlow.ipynb)
- **TSP OR tools** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/Networks/1_TSP_OR_tools.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5641-notebooks/blob/main/Networks/1_TSP_OR_tools.ipynb)
- **Assignment Swim Team** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/Networks/2_Assignment_SwimTeam.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5641-notebooks/blob/main/Networks/2_Assignment_SwimTeam.ipynb)
- **Shortest Path Problem** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/Networks/2_Shortest_Path_Problem.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5641-notebooks/blob/main/Networks/2_Shortest_Path_Problem.ipynb)
- **Assignment Engineers** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/Networks/3_Assignment_Engineers.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5641-notebooks/blob/main/Networks/3_Assignment_Engineers.ipynb)
- **Matching Assignment Machine Scheduling** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/Networks/4_Matching_Assignment_MachineScheduling.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5641-notebooks/blob/main/Networks/4_Matching_Assignment_MachineScheduling.ipynb)
- **Assignment Alternative Model** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/Networks/5_Assignment_Alternative_Model.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5641-notebooks/blob/main/Networks/5_Assignment_Alternative_Model.ipynb)
- **Example Carpet** &nbsp; [![Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/drdave-teaching/OPIM5641-notebooks/blob/main/Networks/Example_Carpet.ipynb) &nbsp; [GitHub](https://github.com/drdave-teaching/OPIM5641-notebooks/blob/main/Networks/Example_Carpet.ipynb)
:::


A huge fraction of business problems are really **networks**: factories shipping to warehouses, people assigned to jobs, trucks routed through cities, inventory carried from one month to the next. Drawing the problem as **nodes and arcs** makes the structure obvious and the model almost write itself. This chapter covers the major network templates, all solved as linear (or integer) programs with CBC.

## 5.1 Minimum-cost flow

The workhorse is **minimum-cost flow**: ship product from **supply** nodes to **demand** nodes across **arcs** (one-way connections, each with a per-unit cost), at minimum total cost. Think Amazon moving inventory from factories to warehouses to meet demand on a FedEx/UPS cost table.

The key modeling device is the node's **flow balance**, captured by a value $b$ at each node:

```{admonition} The three node types and their $b$ values
:class: important
- **Supply node** (a factory): contributes flow → $b > 0$ (its capacity).
- **Demand node** (a warehouse): absorbs flow → $b < 0$ (the **negative** of its demand — the classic place students slip up).
- **Transshipment node** (a depot in the middle): neither makes nor keeps anything → $b = 0$.

Each arc has a **lower bound (0)**, an **upper bound** (capacity), and a **cost**. And you must be able to satisfy demand: assume **total supply ≥ total demand**, or the problem is infeasible without extra tricks.
```

The **Bonner Electronics** example ships from three plants (Minneapolis, Pittsburgh, Tucson) to four warehouses. Each plant's outflow must respect its **capacity** ("≤"), and each warehouse's inflow must **meet demand** ("≥"). In Pyomo this is a tidy pattern — store the costs/capacities in **dictionaries**, create one decision variable per arc, and build the balance constraints with a `ConstraintList` and a loop:

```python
from pyomo.environ import *

model = ConcreteModel()
model.x = Var(arcs, domain=NonNegativeReals)         # flow on each (plant, warehouse) arc

model.obj = Objective(                               # minimize total shipping cost
    expr = sum(cost[a] * model.x[a] for a in arcs), sense = minimize)

model.cons = ConstraintList()
for p in plants:                                     # supply: outflow ≤ capacity
    model.cons.add(sum(model.x[(p,w)] for w in warehouses) <= capacity[p])
for w in warehouses:                                 # demand: inflow ≥ demand
    model.cons.add(sum(model.x[(p,w)] for p in plants) >= demand[w])

SolverFactory('cbc').solve(model)
```

When the per-unit *production* cost differs by plant (the coal/power-plant variant), you just add those terms to the objective — the structure is identical, the objective gets one more sum.

## 5.2 Assignment problems

An **assignment problem** is a special network where *n* things map one-to-one to *n* jobs — four swimmers to four strokes, four machines to four print jobs — to minimize total time/cost. The decision variables are **binary** (person *i* does job *j*, or not), with two clean constraint families:

$$
\sum_j x_{ij} = 1 \;\;\forall i \quad(\text{each person does exactly one job}),\qquad
\sum_i x_{ij} = 1 \;\;\forall j \quad(\text{each job done by exactly one person})
$$

With four people you could eyeball it; with a hundred you can't, and the model handles either identically. (The **swim-team** relay — assign each swimmer the stroke that minimizes total team time — is the friendly version of industrial **machine scheduling**.)

## 5.3 Shortest path, transshipment, and multiperiod

The network template stretches naturally:

- **Shortest path** — find the cheapest route from an origin to a destination. Model it as min-cost flow with the origin as $b=+1$, the destination $b=-1$, every other node a transshipment ($b=0$), and arc costs = distances. (Specialized algorithms like **Dijkstra's** are faster for the vanilla problem, but the LP formulation wins when you need to bolt on extra constraints.)
- **Transshipment** — intermediate depots between sources and sinks; just transshipment nodes ($b=0$) in the middle of the flow.
- **Multiperiod / inventory** — let "time" be the network: each period is a node, **production** flows in, **demand** flows out, and **inventory arcs** carry leftover product to the next period. Modeling a schedule as a flow-through-time is a genuinely powerful idea.

```{admonition} Why bother formulating networks as LPs?
:class: tip
Specialized algorithms solve pure network problems fast — but the **LP/Pyomo formulation is flexible**. The moment the real business adds a wrinkle (a minimum shipment if you use a lane at all, a forbidden route, a budget across arcs), the formulation absorbs it with one more constraint, while a hand-tuned algorithm would have to be rewritten.
```

## Wrap-up

```{admonition} Key takeaways
:class: tip
- Draw business problems as **nodes and arcs**; the structure makes the model obvious.
- **Min-cost flow**: supply nodes ($b>0$), demand nodes ($b<0$, the *negative* of demand), transshipment ($b=0$); assume **supply ≥ demand**.
- The Pyomo pattern: arc dictionaries → one `Var` per arc → `ConstraintList` of supply ("≤") and demand ("≥") balances → CBC.
- **Assignment** = binary one-to-one matching (each row sums to 1, each column sums to 1).
- **Shortest path, transshipment, and multiperiod inventory** are all the same flow template with different $b$ values — and the LP form flexes when the real world adds constraints.
```


---

## 📌 Lecture key points

*Distilled takeaways from the video lectures behind this chapter — click each to expand.*


:::{admonition} Introduction to Network Problems
:class: note dropdown
- Networks = **nodes and arcs** with one-way flow; many supply-chain applications.
- Subtypes; this series starts with **minimum-cost flow** (min-cost shipping).
- Recall allocation (≤), covering (≥), blending models.
- Think in terms of **supply nodes** and **demand nodes**.
- Graphical intuition → the algebra of pairwise arcs.
:::

:::{admonition} Bonner Electronics — Min-Cost Flow — Parts 1–2
:class: note dropdown
- Ship from 3 plants to 4 warehouses at **minimum cost**; CBC solver.
- **Supply constraints "≤"** (capacity), **demand constraints "≥"** (meet demand).
- Assume **supply ≥ demand** (else a harder problem).
- Use **dictionaries** (key:value) + **tuples** for pairwise arcs; nested loops/list comprehension build the objective.
- Pyomo-Cookbook style: change values to solve any same-shape problem.
:::

:::{admonition} Description of Banana Inc.
:class: note dropdown
- Factories → **depots (transshipment)** → warehouses min-cost flow.
- Node value **b**: **+ for supply, 0 for transshipment, − (negative of demand) for demand** — the classic trap.
- Each arc has lower bound 0, an upper-bound capacity, and a per-unit cost.
- Supply (5,500) > demand (4,500) → production is the limiting factor.
- Maps the concepts (supply/demand/transshipment) onto a concrete graphic.
:::

:::{admonition} Lannon Project Revisited + Pyomo Model
:class: note dropdown
- Plants → distributors with **production + transportation** costs (minimize total).
- New twist: if you ship from Atlanta at all, ship **≥ 6,000** (a **multiple-range / fixed-charge**).
- Model with `x ≥ 6000·y` and `x ≤ 18000·y` (y binary) — if y=0 then x=0.
- Build bounds with a **function** indexed by arcs (order must match).
- Flow balance: + for supply, − for demand; equality on demand (minimization won't overship).
:::

:::{admonition} Min-Cost Flow — Transporting Coal
:class: note dropdown
- Objective includes **production cost AND shipping cost** (not just shipping).
- Production cost dwarfs shipping; can't decide by hand → need a model.
- 16 pairwise arcs (4 mines × 4 plants); naming `m11…m44`.
- Supply ("≤") and demand ("≥") constraints; CBC.
- Pyomo-Cookbook style with LaTeX-pretty formulas.
:::

:::{admonition} Solving Multiperiod Models
:class: note dropdown
- Model **time as a network**: each month a node, production in, demand out.
- **Inventory arcs (I)** carry leftover product to the next month.
- Fix demand by setting an arc's lower = upper bound (so it's constant).
- No inventory after the last month (production = total demand).
- All nodes become transshipment by this modeling trick.
:::

:::{admonition} Formulation of the Shortest Path Problem
:class: note dropdown
- Shortest path as min-cost flow: origin **b=+1**, destination **b=−1**, others transshipment.
- Arc cost = distance (or time/money); lower 0, **upper 1** per arc.
- Exercise: convince yourself every arc's upper bound is 1.
- **Dijkstra's** algorithm is faster for the vanilla problem...
- ...but the **LP formulation flexes** when you add constraints.
:::

:::{admonition} Assignment Problems — Swim Team
:class: note dropdown
- Assign *n* things to *n* jobs one-to-one (swimmers→strokes, machines→jobs).
- **Binary** variables; each person does one job, each job done by one person (equalities).
- Rows vs columns of the time matrix = the two constraint families.
- Generalizes to **machine scheduling**.
- Compact Pyomo-Cookbook form vs longhand; same answer, different tinkerability.
:::
