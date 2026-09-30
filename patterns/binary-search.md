# Binary search

Binary search is one of the most powerful and fundamental algorithms to master for coding challenges 
(like LeetCode or HackerRank). Whenever you see a sorted collection and need to find an element efficiently,
binary search should be your go-to technique.

Instead of scanning every element one by one (linear search)
which takes $O(n)$ time, binary search cuts the search space in half with every single step, 
dropping the time complexity down to $O(\log n)$.

## How It Works (The Core Logic)
Binary search requires your array or list to be sorted. It uses three pointers:
1. `low` (or `left`): Points to the start of the search range.
2. `high` (or `right`): Points to the end of the search range.
3. `mid`: The middle index between `low` and `high`.

At each step, you compare your target value to the element at `mid`:
- If the target matches `mid`, you’ve found it! Return the index.
- If the target is smaller than `mid`, it must be in the left half, so move `high` to `mid - 1`.
- If the target is larger than `mid`, it must be in the right half, so move `low` to `mid + 1`.

## C# Implementation (From Scratch)
Here is a standard, robust iterative implementation in C#:
```csharp
public class BinarySearchDemo
{
    public static int Search(int[] nums, int target)
    {
        int low = 0;
        int high = nums.Length - 1;

        while (low <= high)
        {
            // Prevent potential integer overflow for very large arrays
            int mid = low + (high - low) / 2;

            if (nums[mid] == target)
            {
                return mid; // Target found
            }
            else if (nums[mid] < target)
            {
                low = mid + 1; // Discard left half
            }
            else
            {
                high = mid - 1; // Discard right half
            }
        }

        return -1; // Target not found
    }
}
```


## Pro-Tips for Coding Challenges
1. Beware Integer Overflow: In languages like C++, doing `int mid = (low + high) / 2` can overflow if `low + high` exceeds the maximum integer limit. While less common in modern C# with standard array sizes, writing `low + (high - low) / 2` is a great safety habit.
2. Binary Search on Answers: Binary search isn't just for searching sorted arrays! It can also be used to search a range of possible answers (e.g., "Find the minimum capacity to ship packages within D days"). If you can write a helper function that validates whether a specific answer works, and the condition is monotonic (fails below a threshold, succeeds above it), you can binary search the answer space.
