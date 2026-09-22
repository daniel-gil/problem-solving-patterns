# Problem Solving Patterns
Problem-solving patterns are reusable templates or strategies used to solve classes of similar, recurring problems efficiently.

## The core patterns
| Priority | Pattern                              | Typical clue in the problem                                          | Typical complexity      |
| -------: | ------------------------------------ | -------------------------------------------------------------------- | ----------------------- |
|     🥇 1 | **Hash Map / Hash Set**              | "seen before", duplicates, frequency, find a pair, grouping          | O(n)                    |
|     🥇 2 | **Two Pointers**                     | sorted array, pair, palindrome, compare from both ends               | O(n)                    |
|     🥇 3 | **Sliding Window**                   | contiguous substring/subarray, longest/shortest, "at most K"         | O(n)                    |
|     🥇 4 | **Binary Search**                    | sorted data, find position/boundary, minimum/maximum possible value  | O(log n) or O(n log n)  |
|     🥇 5 | **Stack / Monotonic Stack**          | matching/nesting, next greater/smaller, previous greater/smaller     | O(n)                    |
|     🥇 6 | **DFS / BFS**                        | explore connected nodes/cells, traversal, reachability               | O(V + E)                |
|     🥇 7 | **Sorting + Greedy**                 | scheduling, maximize/minimize, make locally optimal decisions        | O(n log n)              |
|     🥇 8 | **Intervals**                        | overlapping ranges, meetings, merging intervals                      | O(n log n)              |
|     🥇 9 | **Heap / Priority Queue**            | Top K, Kth largest/smallest, repeatedly get min/max                  | O(n log k) / O(n log n) |
|    🥇 10 | **Prefix Sum**                       | repeated range sums, subarray sums, cumulative values                | O(n)                    |
|    🥈 11 | **Backtracking**                     | "generate all", permutations, combinations, subsets, choices         | Exponential             |
|    🥈 12 | **Linked List / Fast-Slow Pointers** | reverse, cycle, middle, merge linked lists                           | O(n)                    |
|    🥈 13 | **Trees**                            | depth, height, paths, subtree, level order, BST                      | O(n)                    |
|    🥈 14 | **Graphs / Topological Sort**        | dependencies, prerequisites, connections, directed graph             | O(V + E)                |
|    🥈 15 | **Dynamic Programming**              | number of ways, min/max result, repeated subproblems, optimal result | Varies                  |
|    🥉 16 | **Union-Find (DSU)**                 | connectivity, grouping, merging components                           | ~O(n)                   |
|    🥉 17 | **Dijkstra**                         | shortest path with weighted edges                                    | O((V + E) log V)        |
|    🥉 18 | **Trie**                             | prefixes, autocomplete, dictionary/string prefix search              | O(length)               |

## The complete problem-solving flow
```
┌──────────────────────────────────────────────┐
│              READ THE PROBLEM                │
└───────────────────────┬──────────────────────┘
                        ↓
┌──────────────────────────────────────────────┐
│ 1. WHAT IS THE DATA STRUCTURE?               │
│                                              │
│ Array / String / Linked List / Tree / Graph  │
│ Grid / Matrix / Other                        │
└───────────────────────┬──────────────────────┘
                        ↓
┌──────────────────────────────────────────────┐
│ 2. WHAT ARE THEY ASKING FOR?                 │
│                                              │
│ Find / Check / Count / Min / Max / Generate  │
│ Shortest / Longest / Frequency / Ordering    │
└───────────────────────┬──────────────────────┘
                        ↓
┌──────────────────────────────────────────────┐
│ 3. WHAT WORDS/CONCEPTS ARE CLUES?            │
│                                              │
│ sorted? contiguous? pair? top K?             │
│ dependency? connected? prefix?               │
│ next greater? shortest path?                 │
│ all combinations? repeated subproblems?      │
└───────────────────────┬──────────────────────┘
                        ↓
┌──────────────────────────────────────────────┐
│ 4. WHAT PATTERN DOES THAT SUGGEST?           │
│                                              │
│ Hash Map       Two Pointers   Sliding Window │
│ Binary Search  Stack          DFS/BFS        │
│ Heap           Prefix Sum     Backtracking   │
│ Greedy         DP             Graph          │
│ Union-Find     etc.                          │
└───────────────────────┬──────────────────────┘
                        ↓
┌──────────────────────────────────────────────┐
│ 5. WHY DOES BRUTE FORCE FAIL?                │
│                                              │
│ Identify the repeated work / bottleneck.     │
└───────────────────────┬──────────────────────┘
                        ↓
┌──────────────────────────────────────────────┐
│ 6. CHECK CONSTRAINTS                         │
│                                              │
│ Can O(n²) work? O(2ⁿ)? Need O(n log n)?      │
└───────────────────────┬──────────────────────┘
                        ↓
┌──────────────────────────────────────────────┐
│ 7. IMPLEMENT THE KNOWN TEMPLATE              │
│                                              │
│ C# Dictionary / HashSet / Queue / Stack      │
│ PriorityQueue / recursion / sorting / etc.   │
└───────────────────────┬──────────────────────┘
                        ↓
┌──────────────────────────────────────────────┐
│ 8. VERIFY                                    │
│                                              │
│ Edge cases + time complexity + space         │
└──────────────────────────────────────────────┘
```

## Universal pattern-recognition model

```
                         ┌─────────────────────┐
                         │    READ THE PROBLEM │
                         └──────────┬──────────┘
                                    │
                                    ▼
                    ┌───────────────────────────┐
                    │ 1. WHAT IS THE STRUCTURE? │
                    └─────────────┬─────────────┘
                                  │
          ┌───────────────────────┼────────────────────────┐
          │                       │                        │
          ▼                       ▼                        ▼
     Array / String          Linked List              Tree / Graph
          │                       │                        │
          │                       │                 ┌──────┴──────┐
          │                       │                 │             │
          │                       │                 ▼             ▼
          │                       │                Tree         Graph
          │                       │
          └──────────────┬────────┴──────────────────────────────┐
                         │                                       │
                         ▼                                       ▼
                       Grid / Matrix                       Other / Custom
                         │
                         ▼
             ┌───────────────────────────┐
             │ 2. WHAT IS THE QUESTION?  │
             └─────────────┬─────────────┘
                           │
       ┌───────────────────┼────────────────────┐
       │                   │                    │
       ▼                   ▼                    ▼
    FIND / CHECK         COUNT               OPTIMIZE
       │                   │                    │
       │                   │                    │
       ▼                   ▼                    ▼
   existence?          how many?          min / max?
   pair?               frequency?         shortest?
   position?           ways?              longest?
   duplicate?          subarrays?         cheapest?
       │                   │                    │
       └───────────────────┼────────────────────┘
                           │
                           ▼
             ┌───────────────────────────┐
             │ 3. WHAT SPECIAL CLUE      │
             │    DOES THE STATEMENT     │
             │    GIVE YOU?              │
             └─────────────┬─────────────┘
                           │
       ┌───────────────────┼───────────────────────────┐
       │                   │                           │
       ▼                   ▼                           ▼
    "SORTED"          "CONTIGUOUS"                "DEPENDENCY"
       │                   │                           │
       ▼                   ▼                           ▼
  Binary Search      Sliding Window            Topological Sort
  Two Pointers       Prefix Sum                Graph
       │
       ▼
   "PAIR?"
       │
       ▼
   Two Pointers
   Hash Map


       ┌────────────────────────────────────────────────────────┐
       │                    OTHER CLUES                          │
       └────────────────────────────────────────────────────────┘

 "SEEN BEFORE?"          → Hash Set / Hash Map

 "FREQUENCY?"            → Hash Map

 "TOP K?"                → Heap / Priority Queue

 "NEXT GREATER?"         → Monotonic Stack

 "MATCHING / NESTED?"    → Stack

 "LONGEST SUBSTRING?"    → Sliding Window

 "SHORTEST SUBARRAY?"    → Sliding Window / Prefix Sum

 "RANGE SUM?"            → Prefix Sum

 "OVERLAPPING RANGES?"   → Sort + Intervals

 "GENERATE ALL?"         → Backtracking

 "ALL COMBINATIONS?"     → Backtracking

 "ALL PERMUTATIONS?"     → Backtracking

 "ALL SUBSETS?"          → Backtracking

 "EXPLORE EVERYTHING?"   → DFS / BFS

 "CONNECTED?"            → DFS / BFS / Union-Find

 "SHORTEST PATH?"
       │
       ├── unweighted     → BFS
       ├── weighted       → Dijkstra
       └── special weights→ specialized shortest-path algorithm

 "TREE DEPTH / HEIGHT?"  → DFS

 "TREE LEVELS?"           → BFS

 "BST ORDER?"             → In-order traversal

 "CYCLE IN LINKED LIST?" → Fast / Slow Pointers

 "REVERSE LINKED LIST?"   → Pointer manipulation

 "MERGE SORTED LISTS?"   → Two Pointers

 "PREREQUISITES?"         → Graph + Topological Sort

 "REPEATED SUBPROBLEMS?"  → Dynamic Programming

 "NUMBER OF WAYS?"       → DP / Backtracking (depends on constraints)

 "MIN / MAX RESULT?"     → DP / Greedy (depends on structure)

 "CAN I DO IT?"          → DP / Greedy / Binary Search (depends on monotonicity)

 "CONNECT COMPONENTS?"    → DFS/BFS / Union-Find

 "PREFIX OF WORDS?"        → Trie

 "CONTINUOUS MIN/MAX?"     → Sliding Window / Monotonic Queue

 "KTH SMALLEST/LARGEST?"   → Heap / Quickselect / Binary Search

 "SORT WITH CUSTOM RULE?"  → Sorting + IComparer/IComparison

 "DIVIDE INTO GROUPS?"    → Hash Map / Sorting / Greedy / DP

 "START FROM THE END?"    → Reverse iteration / Greedy / DP
```
