# Sliding Window
The sliding window technique is an efficient algorithmic approach used to process sequential data—such as arrays 
or strings—by maintaining a subset of elements as a "window" and sliding it across the data structure.

Instead of recomputing results for overlapping segments from scratch (which often leads to a slow $O(n^2)$ brute-force solution), 
this technique lets you reuse previous computations, optimizing the time complexity to $O(n)$.

## How It Works
Imagine a window of a fixed or dynamic size moving from the left of an array to the right:
- **Initialize**: Set up the window using the first few elements.
- **Slide**: Move the window one step to the right by adding the new element entering the right side and removing the old element leaving the left side.
- **Update**: Keep track of the result (e.g., maximum sum, minimum length) at each step.

## Types of Sliding Windows
- **Fixed Size**: The window length ($k$) remains constant. You add the new element and subtract the element that falls out of the left side.
- **Dynamic Size**: The window grows or shrinks based on a specific condition (e.g., finding the longest substring with unique characters).

## Code Example (C#): Fixed-Size Window
**Problem**: Find the maximum sum of any contiguous subarray of size $k$.

```csharp
using System;

public class SlidingWindowExample
{
    public static int FindMaxSubarraySum(int[] arr, int k)
    {
        if (arr.Length < k) return -1;

        int maxSum = 0;
        int windowSum = 0;

        // 1. Compute the sum of the first window of size k
        for (int i = 0; i < k; i++)
        {
            windowSum += arr[i];
        }
        maxSum = windowSum;

        // 2. Slide the window across the rest of the array
        for (int i = k; i < arr.Length; i++)
        {
            // Add the new element entering the window on the right,
            // and subtract the element leaving the window on the left.
            windowSum += arr[i] - arr[i - k];
            
            maxSum = Math.Max(maxSum, windowSum);
        }

        return maxSum;
    }

    public static void Main()
    {
        int[] numbers = { 2, 1, 5, 1, 3, 2 };
        int k = 3;
        Console.WriteLine($"Max sum of size {k}: {FindMaxSubarraySum(numbers, k)}"); 
        // Output: 9 (subarray [5, 1, 3])
    }
}
```

## When to Use It
Look for these keywords and patterns in code challenges:
- Problem mentions contiguous subarrays or substrings.
- Involves computing a maximum, minimum, longest, shortest, or target value within a range ($k$ or a condition).
- The brute-force solution requires nested loops (checking every possible window independently).

> **Pro Tip**: If a problem allows the window size to change dynamically, you will typically use a `while` loop inside your main
> `for` loop to shrink the window from the left whenever the condition is violated.
