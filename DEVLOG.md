# Development Log – The Torchbearer

**Student Name:** ___________________________
**Student ID:** ___________________________

> Instructions: Write at least four dated entries. Required entry types are marked below.
> Two to five sentences per entry is sufficient. Write entries as you go, not all in one
> sitting. Graders check that entries reflect genuine work across multiple sessions.
> Delete all blockquotes before submitting.

---

## Entry 1 – [Date]: Initial Plan

> Required. Write this before writing any code. Describe your plan: what you will
> implement first, what parts you expect to be difficult, and how you plan to test.

_My plan was to first understand the problem and map it to known algorithms. I decided to implement Dijkstra’s algorithm first for computing shortest paths, since everything depends on correct distance values. After that, I planned to implement the search over relic orders using recursion and pruning. I expected the hardest part to be designing the recursive search and ensuring pruning does not remove the optimal solution. I planned to test using the provided test cases after each function was completed.
_

---

## Entry 2 – [Date]: [Short description]

> Required. At least one entry must describe a bug, wrong assumption, or design change
> you encountered. Describe what went wrong and how you resolved it.

_While implementing Dijkstra’s algorithm, I initially forgot to check whether a popped node from the priority queue had an outdated distance. This caused incorrect updates and repeated processing of nodes. I fixed this by adding a condition to skip processing if the current distance is greater than the stored distance. After fixing this, the distance results became correct and consistent with expectations.
_

---

## Entry 3 – [Date]: [Short description]

_I implemented the recursive search for visiting relics and noticed that the number of possibilities grows very quickly. Initially, I did not include pruning, which made the search inefficient. I added a best-so-far check to stop exploring branches that already exceed the current best cost. This significantly improved performance and still produced correct results.
_

---

## Entry 4 – [Date]: Post-Implementation Reflection

> Required. Written after your implementation is complete. Describe what you would
> change or improve given more time.

_If I had more time, I would improve the lower bound used for pruning to make the search more efficient. Right now, the pruning only checks the current cost, but it could include estimated future costs. I would also consider using bitmasking instead of sets for relic tracking to improve performance. Overall, the solution works correctly but could be optimized further.
_

---

## Final Entry – [Date]: Time Estimate

> Required. Estimate minutes spent per part. Honesty is expected; accuracy is not graded.

| Part | Estimated Hours |
|---|---|
| Part 1: Problem Analysis | 30 mins|
| Part 2: Precomputation Design | 1 |
| Part 3: Algorithm Correctness | 1 |
| Part 4: Search Design | 1n|
| Part 5: State and Search Space | 1hr 30mins |
| Part 6: Pruning | 1 |
| Part 7: Implementation | 1 |
| README and DEVLOG writing | 1 |
| **Total** | 9 |
