# Two Pointers
The Two Pointers pattern is a fundamental algorithmic technique used to search through linear data structures—like arrays, 
strings, or linked lists—typically when they are already sorted or organized in a specific way.

Instead of using nested loops that result in an inefficient $O(n^2)$ time complexity, 
this pattern uses two reference variables (pointers) that traverse the data structure simultaneously, 
often reducing the time complexity to $O(n)$.

## How the Pattern Works
Depending on the problem, the two pointers move in different directions or at different speeds:
- **Opposite Ends (Shrinking Window)**: One pointer starts at the beginning (`left`) and the other at the end (`right`). They move toward each other until they meet. Ideal for sorted arrays/strings.
- **Same Direction (Fast & Slow)**: Both pointers start at the beginning, but move at different speeds or conditions. Ideal for in-place array modifications or cycle detection.

## Mental trigger
> "I'm looking at two positions in an array/string."

### Especially when:
- array is sorted
- looking for a pair
- palindrome
- comparing from both ends

### Classic Example: Two Sum II (Sorted Array)
**Problem**: Given a 1-indexed array of integers already sorted in non-decreasing order, find two numbers such that they add up to a specific target number.

```
L →              ← R
 [1  3  4  5  7  11]
```

```csharp
public class Solution {
    public int[] TwoSum(int[] numbers, int target) {
        int left = 0;
        int right = numbers.Length - 1;

        while (left < right) {
            int sum = numbers[left] + numbers[right];

            if (sum == target) {
                // Return 1-indexed positions
                return new int[] { left + 1, right + 1 };
            } 
            else if (sum < target) {
                left++; // We need a larger sum, move the left pointer up
            } 
            else {
                right--; // We need a smaller sum, move the right pointer down
            }
        }

        return new int[0]; // Fallback if no solution exists
    }
}
```

## Key Scenarios for Two Pointers
- **Searching Pairs**: Finding elements that meet a specific condition (e.g., target sum, closest pair).
- **Reversing or Palindromes**: Checking if a string reads the same forwards and backwards, or reversing an array in-place.
- **Removing Duplicates**: Using a slow pointer to track the position of unique elements while a fast pointer scans ahead.
- **Partitioning**: Separating elements based on a condition (like moving all zeroes to the end of an array).

## Why Use It?
- **Optimal Performance**: Reduces time complexity from $O(n^2)$ to $O(n)$.
- **Constant Space**: Operates in-place, requiring $O(1)$ extra memory because it only uses pointer variables.
  
> **Note**: The most critical **prerequisite** for the opposite-ends variation is that the underlying collection is usually **sorted**.
> If the input isn't sorted and sorting is allowed, remember to factor in the $O(n \log n)$ sorting time.

### Variants
- opposite-direction pointers
- same-direction pointers
- fast/slow pointers
