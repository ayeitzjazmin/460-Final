# The Torchbearer

**Student Name:** Jazmin Gallegos
**Student ID:** 828116114
**Course:** CS 460 – Algorithms | Spring 2026

> This README is your project documentation. Write it the way a developer would document
> their design decisions , bullet points, brief justifications, and concrete examples where
> required. You are not writing an essay. You are explaining what you built and why you built
> it that way. Delete all blockquotes like this one before submitting.

---

## Part 1: Problem Analysis

> Document why this problem is not just a shortest-path problem. Three bullet points, one
> per question. Each bullet should be 1-2 sentences max.

- **Why a single shortest-path run from S is not enough:**
   _A single shortest path run from S only gives the cheapest distance from the entrance to each node. It can't decide the best order to visit the relic chambers._


- **What decision remains after all inter-location costs are known:**
    _The remaining decision is which order to collect the relics before traveling to the exit._


- **Why this requires a search over orders (one sentence):**
    _This problem requires a search over orders because different relic orders can produce different total fuel costs._


---

## Part 2: Precomputation Design

### Part 2a: Source Selection

> List the source node types as a bullet list. For each, one-line reason.

| Source Node Type | Why it is a source |
|---|---|
| Spawn node | The route always starts here, so we need shortest distances from the entrance to relics |
| Relic nodes | After collecting any relic, the route may need to travel to another relic or to the exit |

### Part 2b: Distance Storage

> Fill in the table. No prose required.

| Property | Your answer |
|---|---|
| Data structure name | Nested dictionary dist_table |
| What the keys represent | Outer keys are source nodes; inner keys are destination nodes |
| What the values represent | Shortest-path fuel costs from source to destination |
| Lookup time complexity | O(1) average case |
| Why O(1) lookup is possible | Python dictionaries support average-case constant-time key lookup |

### Part 2c: Precomputation Complexity

> State the total complexity and show the arithmetic. Two to three lines max.

- **Number of Dijkstra runs:** _k + 1_
- **Cost per run:** _O(m log n)_
- **Total complexity:** _O((k + 1)m log n)_
- **Justification (one line):** _The algorithm runs Dijkstra once from the spawn and once from each relic_

---

## Part 3: Algorithm Correctness

> Document your understanding of why Dijkstra produces correct distances.
> Bullet points and short sentences throughout. No paragraphs.

### Part 3a: What the Invariant Means

> Two bullets: one for finalized nodes, one for non-finalized nodes.
> Do not copy the invariant text from the spec.

- **For nodes already finalized (in S):**
  _Their shortest distances from the source are confirmed and will not improve later._

- **For nodes not yet finalized (not in S):**
  _Their current distances are the best discovered estimates using already finalized nodes as internal path steps_

### Part 3b: Why Each Phase Holds

> One to two bullets per phase. Maintenance must mention nonnegative edge weights.

- **Initialization : why the invariant holds before iteration 1:**
  _The source starts with distance 0 and all other nodes start at infinity, so the initial estimates are valid_

- **Maintenance : why finalizing the min-dist node is always correct:**
  _Dijkstra chooses the non finalized node with the smallest current distance. Because all edge weights are nonnegative, a later path through another non finalized node cannot produce a cheaper distance_

- **Termination : what the invariant guarantees when the algorithm ends:**
  _Every reachable node has its true shortest path distance from the source, and unreachable nodes remain infinity_

### Part 3c: Why This Matters for the Route Planner

> One sentence connecting correct distances to correct routing decisions.

_Correct shortest path distances are necessary because the route planner uses them to compare relic orders and choose the minimum fuel route_

---

## Part 4: Search Design

### Why Greedy Fails

> State the failure mode. Then give a concrete counter-example using specific node names
> or costs (you may use the illustration example from the spec). Three to five bullets.

- **The failure mode:** _Greedy can fail because the cheapest next relic may lead to a worse total route_
- **Counter-example setup:** _In the spec example, S -> B` costs 1, S -> C costs 2, and later relic-to-relic costs make the total order important_
- **What greedy picks:** _A greedy strategy might pick the cheapest immediate next relic without comparing the full remaining route_
- **What optimal picks:** _The optimal route from the spec is S -> B -> D -> C -> T with total fuel cost 4_
- **Why greedy loses:** _Greedy loses because it makes a local decision instead of searching all possible relic orders_

### What the Algorithm Must Explore

> One bullet. Must use the word "order."

- _The algorithm must explore each possible relic collection order to find the minimum total fuel route_

---

## Part 5: State and Search Space

### Part 5a: State Representation

> Document the three components of your search state as a table.
> Variable names here must match exactly what you use in torchbearer.py.

| Component | Variable name in code | Data type | Description |
|---|---|---|---|
| Current location | current_loc | node | The node where the search currently is |
| Relics already collected | relics_visited_order | list | The relics collected so far, in order |
| Fuel cost so far | cost_so_far | float/int | The total fuel used so far |

### Part 5b: Data Structure for Visited Relics

> Fill in the table.

| Property | Your answer |
|---|---|
| Data structure chosen | |
| Operation: check if relic already collected | Time complexity: O(1) average case|
| Operation: mark a relic as collected | Time complexity: O(1) average case  |
| Operation: unmark a relic (backtrack) | Time complexity: O(1) average case |
| Why this structure fits | A set gives fast membership, removal, and re-adding during recursive backtracking |

### Part 5c: Worst-Case Search Space

> Two bullets.

- **Worst-case number of orders considered:** _k!_
- **Why:** _There are k relics, and the algorithm may need to consider every permutation of their collection order_

---

## Part 6: Pruning

### Part 6a: Best-So-Far Tracking

> Three bullets.

- **What is tracked:** _The algorithm tracks the best total fuel cost found so far and the relic order that produced it_
- **When it is used:** _It is used during recursion before exploring deeper branches_
- **What it allows the algorithm to skip:** _It allows the algorithm to skip any branch whose current cost is already at least as large as the best known route_

### Part 6b: Lower Bound Estimation

> Three bullets.

- **What information is available at the current state:** _The current location, remaining relics, cost so far exit node and precomputed shortest-path distances are available_
- **What the lower bound accounts for:** _The implemented lower bound accounts for the fuel already spent_
- **Why it never overestimates:** _Since all future travel costs are nonnegative the current fuel cost is never greater than the final cost of completing that branch_

### Part 6c: Pruning Correctness

> One to two bullets. Explain why pruning is safe.

- _Pruning is safe because if cost_so_far >= best[0], then adding more nonnegative travel costs cannot make that branch cheaper than the best route already found_

---

## References

> Bullet list. If none beyond lecture notes, write that.

- _Lecture notes only_
