# Problem Solving Patterns
Problem-solving patterns are reusable templates or strategies used to solve classes of similar, recurring problems efficiently.

## The core patterns
| Priority | Pattern                              | Typical clue in the problem                                          | Typical complexity      |
| -------: | ------------------------------------ | -------------------------------------------------------------------- | ----------------------- |
|     🥇 1 | **[Hash Map / Hash Set](https://github.com/daniel-gil/problem-solving-patterns/tree/main/patterns/hash.md)**              | "seen before", duplicates, frequency, find a pair, grouping          | O(n)                    |
|     🥇 2 | **[Two Pointers](https://github.com/daniel-gil/problem-solving-patterns/tree/main/patterns/two-pointers.md)**                     | sorted array, pair, palindrome, compare from both ends               | O(n)                    |
|     🥇 3 | **[Sliding Window](https://github.com/daniel-gil/problem-solving-patterns/tree/main/patterns/sliding-window.md)**                   | contiguous substring/subarray, longest/shortest, "at most K"         | O(n)                    |
|     🥇 4 | **[Binary Search](https://github.com/daniel-gil/problem-solving-patterns/blob/main/patterns/binary-search.md)**                    | sorted data, find position/boundary, minimum/maximum possible value  | O(log n) or O(n log n)  |
|     🥇 5 | **[Stack / Monotonic Stack](https://github.com/daniel-gil/problem-solving-patterns/blob/main/patterns/stack.md)**          | matching/nesting, next greater/smaller, previous greater/smaller     | O(n)                    |
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

## Big-O analysis 
**Big O notation** is a mathematical language used in computer science to analyze and describe how an algorithm's running **time** or **space** requirements grow as the input size (n) increases. 

It focuses on the worst-case scenario, providing an upper bound on time complexity, which helps developers **determine** the **efficiency** (performance) and **scalability** of **algorithms**.

| Complexity | Example |  |
| --- | --- | --- |
| O(1) | Hash lookup | **Constant Time:** The fastest time; runtime is independent of input size (e.g., accessing an array index). |
| O(log n) | Binary search
Heap | **Logarithmic Time:** Performance grows slowly, common in searching algorithms like binary search. |
| O(n) | Linear scan | **Linear Time:** Performance grows proportionally to input size (e.g., a simple loop). |
| O(n log n) | Sorting | **Log-Linear Time:** Common in efficient sorting algorithms like Merge Sort. |
| O(n²) | Nested loops | **Quadratic Time:** Performance is proportional to the square of the input size (e.g., nested loops). |
| O(2^n) |  | **Exponential Time:** Performance doubles with each addition to the input, becoming unusable for large . |

<img width="1180" height="720" alt="image" src="https://github.com/user-attachments/assets/c0bdc57d-a0cd-40d5-af1d-f6965ec7e614" />


### **O(1) Constant Time**

The size of the input doesn’t matter, the method will run always in constant time or O(1)

```csharp
public static int GetFirstElement(int[] array)
{
    // No matter how large the array is, this operation takes a single step.
    return array.Length > 0 ? array[0] : throw new InvalidOperationException();
}
```

### **O(N) Constant Time**

The cost of the algorithm grows linearly and in direct correlation with the size of the input. The run-time complexity is represented as O(n) where n represents the size of the input. 

```csharp
public static void PrintAllElements(int[] array)
{
    // If 'array' has 10 items, it loops 10 times. If 1,000,000 items, 1,000,000 times.
    foreach (var item in array)
    {
        Console.WriteLine(item);
    }
}
```
Notes: 
- If we have 2 for-loops it will be O(2n), but it is simplified to O(n) because it still represents a linear growth.
- Another case is when we have 2 input parameters, the complexity will be O(n+m) but it can be simplified to O(n) indicating it’s a linear growth.

### **O(N²) Quadratic Time**

In this example we have a nested loop.

```csharp
public static void PrintAllPairs(int[] array)
{
    // For every element in the outer loop, the inner loop runs N times.
    for (int i = 0; i < array.Length; i++)
    {
        for (int j = 0; j < array.Length; j++)
        {
            Console.WriteLine($"({array[i]}, {array[j]})");
        }
    }
}
```

NOTE: O(n+n^2) algorithm can be simplified to O(n^2), because n^2 grows much faster than n.

### **O(N³) Cubic Time**

Here an example of a complexity of O(n^3):

```csharp
public static void CubicExample(int[] array)
{
    int count = 0;
    // Three nested loops result in N * N * N operations.
    for (int i = 0; i < array.Length; i++)
    {
        for (int j = 0; j < array.Length; j++)
        {
            for (int k = 0; k < array.Length; k++)
            {
                count++;
            }
        }
    }
}
```

### **O(log n) Logarithmic Time**

The execution time increases logarithmically as the input size grows. Typically, this occurs in algorithms that divide the problem in half with each step, such as Binary Search on a sorted array.

EXAMPLE: **Binary Search** is a **searching algorithm** that operates on a sorted or monotonic search space, repeatedly dividing it into halves to find a target value or optimal answer in logarithmic time O(log N).

```csharp
public static int BinarySearch(int[] sortedArray, int target)
{
    int left = 0;
    int right = sortedArray.Length - 1;

    while (left <= right)
    {
        int mid = left + (right - left) / 2;

        if (sortedArray[mid] == target)
            return mid;

        if (sortedArray[mid] < target)
            left = mid + 1;
        else
            right = mid - 1;
    }

    return -1; // Not found
}
```

### **O(2^N) Exponential Time**

The exponential growth is the opposite of the logarithmic growth:

```csharp
public static int Fibonacci(int n)
{
    // Base cases
    if (n <= 1) return n;

    // Each call branches into two more recursive calls, leading to 2^n operations.
    return Fibonacci(n - 1) + Fibonacci(n - 2);
}
```
