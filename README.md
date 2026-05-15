# The Torchbearer

**Student Name:** __Eduardo Valdovinos_________________________
**Student ID:** ___________________________
**Course:** CS 460 – Algorithms | Spring 2026

---

## Part 1: Problem Analysis

- **Why a single shortest-path run from S is not enough:**

Dijkstra handles shortest paths from S, but it does not 
determine the best order of relic chambers to visit.

- **What decision remains after all inter-location costs are known:**

We still have to figure out the order in which we have to collect the relics.

- **Why this requires a search over orders (one sentence):**
Different collection orders yield different total fuel costs.
---

## Part 2: Precomputation Design

### Part 2a: Source Selection

| Source Node Type | Why it is a source |
|---|---|
| _Spawn_ | _We need a start node to get shortest path from it to each relic chamber_ |
| _Relic Chambers_ | _Need a way for the bearer to move in between chambers_ |
| _Exit Node_ | _Need a way to to tell the total distance from start to finish_ |


### Part 2b: Distance Storage

| Property | Your answer |
|---|---|
| Data structure name |dist_table|
| What the keys represent |Outer keys: source nodes, Inner Keys: destination nodes. |
| What the values represent |The cheapest fuel cost from source to destination node. |
| Lookup time complexity |Average case of O(1) |
| Why O(1) lookup is possible |Via hashing in python, dist_table[u][v] has an avg constant time look up |

### Part 2c: Precomputation Complexity

- **Number of Dijkstra runs:** _k + 2, where k = |M|_
- **Cost per run:** _O(m log n)_
- **Total complexity:** _O((k + 2) * m log n))_
- **Justification (one line):** _Dijstra's algorithm runs once at the start, at each relic, and at the exit._

---

## Part 3: Algorithm Correctness

### Part 3a: What the Invariant Means

- **For nodes already finalized (in S):**
  
  - Already locked in with best possible distance from source.
  - No need to revisit them with dijkstra.

- **For nodes not yet finalized (not in S):**
  
  - Only contain the best estimates found so far, can still
    be overwritten if better option is found.

### Part 3b: Why Each Phase Holds

- **Initialization : why the invariant holds before iteration 1:**
  
- The source initializes as 0, while every other node starts at infinity. 
  This satisfies the requirement of no paths being explored yet.

- **Maintenance : why finalizing the min-dist node is always correct:**
  
  - Any path found later would add to the cost, and it's impossible for it to become cheaper. This is because there are no negative edge weights.

- **Termination : what the invariant guarantees when the algorithm ends:**
  
  - The invariant guarantees that when all reachable nodes have their final shortest distances, any node that is still inifnity is not reachable from the source.

### Part 3c: Why This Matters for the Route Planner

Correct distances for shortest paths matters because we use those values to compare relic collection orders to choose the cheapest route.

---

## Part 4: Search Design

### Why Greedy Fails

- **The failure mode:** 

If we use the greedy method to choose the next relic, we risk causing a more
expensive route because best local choice doesn't mean best general choice.

- **Counter-example setup:** 

From the spec example:
- Entrance: S
- Relics: B, C, D
- Exit: T


- **What greedy picks:** 

- Greedy picks the nearest relic choice from S =, in this case B for minimum cost.

- **What optimal picks:** 

 Optimal route: S --> B --> D --> C --> T (Total fuel cost 4)

- **Why greedy loses:**

The best route is the one with the best relic collection order. The greedy choice only looks at the cheapest move.

### What the Algorithm Must Explore

- The algorithm must explore different collection orders, as each can yield a different total cost.

---

## Part 5: State and Search Space

### Part 5a: State Representation

| Component | Variable name in code | Data type | Description |
|---|---|---|---|
| Current location | current_loc | node | The room currently being searched |
| Relics already collected | relics_visited_order | list[node] | Relics collected so far in order |
| Fuel cost so far | cost_so_far | float | Total fuel used by the route still in progress |

### Part 5b: Data Structure for Visited Relics

| Property | Your answer |
|---|---|
| Data structure chosen | The set relics_remaining |
| Operation: check if relic already collected | Time complexity: Avg of O(1) |
| Operation: mark a relic as collected | Time complexity: Avg of O(1) |
| Operation: unmark a relic (backtrack) | Time complexity: Avg of O(1) |
| Why this structure fits | A set is faster for tracking which relics haven't been vistied yet |

### Part 5c: Worst-Case Search Space

- **Worst-case number of orders considered:** _k!, k = |M|_
- **Why:** _The algorithm may have to try every possible order of k relics._

---

## Part 6: Pruning

### Part 6a: Best-So-Far Tracking

- **What is tracked:** _The best route found so far._
- **When it is used:** _Used when checking if cost_so_far is too expensive before exploring._
- **What it allows the algorithm to skip:** _We can skip the routes that are more expensive than the best current cost._

### Part 6b: Lower Bound Estimation

- **What information is available at the current state:** 

 - current_loc, relics_remainig, relics_visited_order, cost_so_far are all available info.

- **What the lower bound accounts for:** 
 - It accounts for the fuel already spent: cost_so_far.

- **Why it never overestimates:** 
 - All remaining costs are nonnegative. This means that it is impossible for the final
   route to ne cheaper than cost_so_far.

### Part 6c: Pruning Correctness

Pruning is safe because:
- All edge weights are nonnegative, so the route branch can't be the most optimal if
 it already reached best[0].

---

## References

Lecture notes only
