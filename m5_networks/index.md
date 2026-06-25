# Chapter 5 — Network Optimization

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
