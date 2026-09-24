# Hash Map / Hash Set

The Hash Map / Hash Set pattern is one of the most powerful techniques in coding interviews. It allows you to trade space complexity for time complexity, dropping lookup, insertion, and deletion times down to an average of $O(1)$.

In C#, this pattern is implemented using `HashSet<T>` for tracking unique elements and `Dictionary<TKey, TValue>` for mapping keys to values.

## Core Use Cases
- Existence Checking (`HashSet<T>`): Instantly check if an element has been seen before, such as finding duplicates or detecting cycles.
- Frequency Counting (`Dictionary<TKey, TValue>`): Track occurrences of items to solve problems like anagrams or top-k elements.
- Complement Lookup (`Dictionary<TKey, TValue>`): Store previously visited numbers and their indices to find pairs (e.g., the classic Two Sum problem).


## C# Code Example: Two Sum

**Problem**: Given an array of integers **NOT** sorted, find two numbers such that they add up to a specific target number.

Here is how a Hash Map transforms an $O(N^2)$ brute-force search into an efficient $O(N)$ solution:

```csharp
public int[] TwoSum(int[] nums, int target) {
    Dictionary<int, int> map = new Dictionary<int, int>();
    
    for (int i = 0; i < nums.Length; i++) {
        int complement = target - nums[i];
        
        // O(1) average lookup time
        if (map.ContainsKey(complement)) {
            return new int[] { map[complement], i };
        }
        
        map[nums[i]] = i;
    }
    
    return new int[0];
}
```

### Pro Tips for C# Developers
- Use TryGetValue: Instead of calling ContainsKey followed by a lookup, use map.TryGetValue(key, out var value) to perform both actions in a single step and improve performance.
- Mind the Space Complexity: While your time complexity improves to $O(N)$, your space complexity will also be $O(N)$ because you are storing elements in memory.

  

## Mental trigger
> "Have I seen this before?"
> 
```csharp
var seen = new HashSet<int>();

foreach (var x in nums)
{
    if (!seen.Add(x))
        return true;
}
```

> "How many times does each thing occur?" (frequency)

```csharp
var frequency = new Dictionary<int, int>();

foreach (var x in nums)
{
    frequency[x] = frequency.GetValueOrDefault(x) + 1;
}
```

### Typical problems:
- Two Sum
- Contains Duplicate
- Valid Anagram
- Group Anagrams
- Top K Frequent Elements

### Important sub-pattern

Frequency map → sort by frequency
```csharp
var ordered = frequency
    .OrderByDescending(x => x.Value)
    .ToList();
```
