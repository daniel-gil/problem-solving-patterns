# Stack and Monotonic Stack

The Stack and Monotonic Stack are fundamental algorithmic patterns used to solve problems involving nested structures, 
tracking state, and finding nearest greater/smaller elements in linear time $O(n)$.

## Pattern 1: Stack for Matching & Nesting
### Core Concept
Used when processing linear input that has hierarchical,
nested, or symmetrical relationships (e.g., matching parentheses, validating HTML tags, evaluating postfix expressions).
- **Mechanism**: Push elements as you go. When a matching closing condition is met, pop and validate.
- **Time Complexity**: $O(n)$ time | Space Complexity: $O(n)$ space.

### C# Template: Valid Parentheses / Matching
```csharp
public bool IsValid(string s) 
{
    Stack<char> stack = new();
    Dictionary<char, char> matchingMap = new() 
    {
        { ')', '(' },
        { ']', '[' },
        { '}', '{' }
    };

    foreach (char c in s) 
    {
        if (matchingMap.ContainsKey(c)) // Closing bracket
        {
            // If stack is empty or top element doesn't match the required open bracket
            if (stack.Count == 0 || stack.Pop() != matchingMap[c]) 
            {
                return false;
            }
        } 
        else // Opening bracket
        {
            stack.Push(c);
        }
    }

    return stack.Count == 0;
}
```

## Pattern 2: Monotonic Stack
### Core Concept
A Monotonic Stack maintains its elements in either strictly increasing or decreasing order. 
It is the go-to pattern for finding the Next/Previous Greater/Smaller element in $O(n)$ time 
instead of brute-forcing in $O(n^2)$.
- **Monotonic Decreasing Stack**: Keeps values in descending order (top of stack is the smallest). 
Used for finding Next Greater Element.
- **Monotonic Increasing Stack**: Keeps values in ascending order (top of stack is the largest). 
Used for finding Next Smaller Element.Key Insight

### Key Insight
Store indices instead of values in the stack. Storing indices lets you calculate distances, 
access original values via nums[index], and handle duplicates accurately.

### Monotonic Stack Variant Matrix
| Problem Goal | Stack Order | Loop Direction | Pop Condition (nums[i] vs nums[stack.Peek()]) |
| -------- | ------- | -------- | -------|
| Next Greater Element | Decreasing | Left to Right (0→n−1) | nums[i] > nums[stack.Peek()] |
| Next Smaller Element | Increasing | Left to Right (0→n−1) | nums[i] < nums[stack.Peek()] |
| Previous Greater Element | Decreasing | Right to Left (n−1→0) | nums[i] > nums[stack.Peek()] |
| Previous Smaller Element | Increasing | Right to Left (n−1→0) | nums[i] < nums[stack.Peek()] |

### C# Implementation: Next Greater Element
#### Problem
Given an array nums, return an array result where result[i] is the next element to the right that is 
strictly greater than nums[i]. If no such element exists, set result[i] = -1.

```csharp
public int[] NextGreaterElement(int[] nums) 
{
    int n = nums.Length;
    int[] result = new int[n];
    Array.Fill(result, -1);
    
    // Stores indices, keeping values in monotonic DECREASING order
    Stack<int> stack = new(); 

    for (int i = 0; i < n; i++) 
    {
        // Maintain decreasing order: pop elements smaller than the current element
        while (stack.Count > 0 && nums[i] > nums[stack.Peek()]) 
        {
            int poppedIndex = stack.Pop();
            result[poppedIndex] = nums[i]; // Current element is the Next Greater for popped index
        }
        
        stack.Push(i);
    }

    return result;
}
```

#### C# Universal Template (Flexible for all 4 Variants)
```csharp
public int[] MonotonicStackPattern(int[] nums, string type) 
{
    int n = nums.Length;
    int[] result = new int[n];
    Array.Fill(result, -1);
    Stack<int> stack = new();

    for (int i = 0; i < n; i++) 
    {
        // Change comparison condition depending on the problem type
        while (stack.Count > 0 && ShouldPop(nums[i], nums[stack.Peek()], type)) 
        {
            int poppedIndex = stack.Pop();
            result[poppedIndex] = nums[i];
        }
        
        stack.Push(i);
    }

    return result;
}

private bool ShouldPop(int currentValue, int stackTopValue, string type) => type switch 
{
    "NextGreater"    => currentValue > stackTopValue,
    "NextSmaller"    => currentValue < stackTopValue,
    _ => throw new ArgumentException("Invalid type")
};
```

### Common Problem Examples
- Daily Temperatures (LeetCode 739): Next Greater Element distance calculation (i - stack.Pop()).
- Next Greater Element I & II (LeetCode 496, 503): Circular array traversal using i % n.
- Largest Rectangle in Histogram (LeetCode 84): Finds both Previous Smaller and Next Smaller boundaries using a monotonic stack.
- Trapping Rain Water (LeetCode 42): Uses a monotonic stack to find bounded valleys.
