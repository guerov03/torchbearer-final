# Development Log – The Torchbearer

**Student Name:** Eduardo Valdovinos
**Student ID:** 127403871

---

## Entry 1 – [05/12/2026]: Initial Plan

- First, I will implement Dijsktra's algorithm for finding shortest paths while heeding the warning from the readme part 1.

- I plan to first fill out the read me part 1 to make sure I understand the problem and fill out the first part of the python file with my read me content.

- I predict that the coding of the search will be difficult and making sure that pruning doesn't skip the optimal route.

- I plan to use the built in tests after each section, from which I will then check for small cases.


---

## Entry 2 – [05/13/2026]: [Short description]

_Implemented first actual code in part 2: _

- Implemented the selecting of important source nodes and running Dijkstra from each

- Made sure to match the readme portion that mentions dist_table[source][destination] should give the smallest fuel cost.

- The provided tests failing were unexpected at first until I noticed that the route search functions aren't finished yet. It at least helped me make sure syntax and other things were working fine before proceeding.


---

## Entry 3 – [05/14/2026]: [Short description]

Implemented solve(), fixed bugs, and tested

_While testing the route search, I encountered some bugs, luckily I Was able to found the indentation error 
quickly_

- new_cost was outside of the neigbor loop in run_dikkstra()
- choose, recursive search, and backtrack was not inside of the relic loop
- All tests passed after correcting these

---

## Entry 4 – [05/14/2026]: Post-Implementation Reflection

- After implementing solve(), all tests passed

Given more time:
- Clean up comments sp that the code has better readibility.
- Keep testing for bugs, maybe by adding more tests for spcific cases.

Reflection:

Although all tests passed, I would have liked to comment my code better and to add tests
to find possible bugs in specific cases. My favorite part of this project was that I got to understand 
how Dijkstra's algorithm can be used with backtracking to solve a larger problem. I enjoyed the assignment, as it was in a language that I am not used to, and it pushed me out of my comfort zone. 
I appreciate the learning experience.

---

## Final Entry – [05/14/2026]: Time Estimate

| Part | Estimated Hours |
|---|---|
| Part 1: Problem Analysis |1.5 Hours reading the entire assignment and making sense of the work plan|
| Part 2: Precomputation Design | 2.5 Hours getting used to the plan structure and implementing |
| Part 3: Algorithm Correctness | 1 Hour |
| Part 4: Search Design | 1.5 Hours|
| Part 5: State and Search Space |1.5 Hours  |
| Part 6: Pruning | 1.5 Hours |
| Part 7: Implementation | 1 Hour |
| README and DEVLOG writing |2.5 Hours |
| **Total** | 13 Hours ( X _ X) |
