# Hash Map / Hash Set

Mental trigger:
- Seen before:
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

- Frequency:
> "How many times does each thing occur?"

```csharp
var frequency = new Dictionary<int, int>();

foreach (var x in nums)
{
    frequency[x] = frequency.GetValueOrDefault(x) + 1;
}
```

Typical problems:
- Two Sum
- Contains Duplicate
- Valid Anagram
- Group Anagrams
- Top K Frequent Elements

## Important sub-pattern

Frequency map → sort by frequency
```csharp
var ordered = frequency
    .OrderByDescending(x => x.Value)
    .ToList();
```
