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

## Code Example (C#): Dynamic Window
Problem: Find the length of the longest substring without repeating characters.

```csharp
using System;
using System.Collections.Generic;

public class DynamicWindowExample
{
    public static int LengthOfLongestSubstring(string s)
    {
        int maxLength = 0;
        int left = 0;
        HashSet<char> windowChars = new HashSet<char>();

        // Outer loop controls the RIGHT pointer, expanding the window
        for (int right = 0; right < s.Length; right++)
        {
            // Inner while loop controls the LEFT pointer, shrinking the window 
            // if we encounter a duplicate character.
            while (windowChars.Contains(s[right]))
            {
                windowChars.Remove(s[left]);
                left++; // Shrink from the left
            }

            // Add the new character and update max length
            windowChars.Add(s[right]);
            maxLength = Math.Max(maxLength, right - left + 1);
        }

        return maxLength;
    }

    public static void Main()
    {
        string text = "abcabcbb";
        Console.WriteLine($"Longest unique substring length: {LengthOfLongestSubstring(text)}"); 
        // Output: 3 ("abc")
    }
}
```

## Code Example (C#): Fixed-Size Window

**Problem**: Find the maximum sum of any contiguous subarray of size $k$.


### Using Two Sequential Loops
Separates the initialization phase (building the first window) from the sliding phase. It requires zero if checks inside the loop, making it slightly faster in terms of raw CPU instructions.


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

### Using Single-Loop Fixed Window
Keeps all array traversal inside one unified block of code, which can feel cleaner to read.

```csharp
public static int FindMaxSubarraySumSingleLoop(int[] arr, int k)
{
    if (arr.Length < k) return -1;

    int maxSum = 0;
    int windowSum = 0;

    for (int i = 0; i < arr.Length; i++)
    {
        // 1. Add the new element entering the window on the right
        windowSum += arr[i];

        // 2. Once we pass index k-1, subtract the element leaving from the left
        if (i >= k)
        {
            windowSum -= arr[i - k];
        }

        // 3. Once the first window is fully formed, start tracking the max
        if (i >= k - 1)
        {
            maxSum = Math.Max(maxSum, windowSum);
        }
    }

    return maxSum;
}
```


### Summary of Window Patterns
- **Fixed-Size Window**: Needs no nested loops at all—just a single loop sliding a fixed range.
- **Dynamic-Size Window**: Uses a for loop (right) combined with a nested while loop (left) to adjust bounds.


## When to Use It
Look for these keywords and patterns in code challenges:
- Problem mentions contiguous subarrays or substrings.
- Involves computing a maximum, minimum, longest, shortest, or target value within a range ($k$ or a condition).
- The brute-force solution requires nested loops (checking every possible window independently).

> **Pro Tip**: If a problem allows the window size to change dynamically, you will typically use a `while` loop inside your main
> `for` loop to shrink the window from the left whenever the condition is violated.
