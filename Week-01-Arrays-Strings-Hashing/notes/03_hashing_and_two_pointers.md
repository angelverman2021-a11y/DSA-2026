# 🗝️ Deep-Dive Notes: Hashing Foundations & Two-Pointer Strategies

---

## 1. Hash Table Internal Mechanics

A **Hash Table** maps keys to values using a **Hash Function** to compute an index into an array of buckets.

```
Key ("apple") ──► Hash Function h("apple") ──► Hash Code (0x3A2B) ──► Index (0x3A2B % BucketCount) ──► Bucket [3]
```

### 1.1 Collision Resolution Techniques
When two distinct keys produce the same bucket index:

1. **Separate Chaining (Used in Java HashMap, C++ unordered_map)**:
   - Each bucket is a linked list (or balanced Red-Black tree if bucket length exceeds a threshold like 8 in Java 8+).
   - Time Complexity: Average $O(1)$, Worst $O(N)$ (or $O(\log N)$ with treeified buckets).

2. **Open Addressing (Linear Probing / Quadratic Probing / Double Hashing)**:
   - All elements reside directly in the bucket table.
   - If bucket $i$ is occupied, probe $i+1, i+2, \dots$ until an empty slot is found.

### 1.2 Load Factor & Dynamic Rehashing
$$\text{Load Factor } (\alpha) = \frac{\text{Number of Stored Elements } (N)}{\text{Number of Buckets } (M)}$$

- Default threshold is usually **$\alpha = 0.75$**.
- When $\alpha > 0.75$, the hash table **rehashes**: doubles the bucket array size ($2M$) and re-inserts all keys to maintain $O(1)$ lookup guarantees.

---

## 2. Core Hashing Problem Patterns

### Pattern A: The Complement Lookup (Two Sum Pattern)
Instead of checking all $O(N^2)$ pairs $(a, b)$ to see if $a + b = \text{target}$, for each element $x$, we check if its complement $(\text{target} - x)$ already exists in the Hash Map.

```
For nums = [2, 7, 11, 15], target = 9:
i = 0, num = 2  --> Need (9 - 2) = 7. Seen map: {2: 0}
i = 1, num = 7  --> Need (9 - 7) = 2. Found in map at index 0! Return [0, 1] ⚡
```

---

### Pattern B: Frequency Counting & Categorization
Count character or number frequencies to verify anagrams, palindromes, or majority elements.

**Memory Optimization Tip:**
- If keys are lowercase English letters (`'a'` to `'z'`), use a **fixed-size array of size 26** instead of a heavy Hash Map:
  $$\text{index} = \text{char} - \text{'a'}$$
  This avoids heap allocations and provides $O(1)$ time and $O(1)$ space with zero overhead.

---

### Pattern C: Prefix Sum + Hash Map Integration
Used in **Subarray Sum Equals K** (LeetCode #560).

**Mathematical Invariant:**
Let $\text{prefix}[j] = \sum_{k=0}^j \text{nums}[k]$.  
A subarray $\text{nums}[i \dots j]$ has sum $K$ if and only if:

$$\text{prefix}[j] - \text{prefix}[i-1] = K \iff \mathbf{\text{prefix}[i-1] = \text{prefix}[j] - K}$$

```python
def subarraySum(nums: list[int], k: int) -> int:
    prefix_count = {0: 1}  # Base case: a prefix sum of 0 has occurred once
    current_sum = 0
    total_subarrays = 0
    
    for num in nums:
        current_sum += num
        # Check how many previous prefixes equal (current_sum - k)
        needed = current_sum - k
        if needed in prefix_count:
            total_subarrays += prefix_count[needed]
            
        prefix_count[current_sum] = prefix_count.get(current_sum, 0) + 1
        
    return total_subarrays
```

---

## 3. Two Pointers Master Patterns

```
Pattern 1: Opposite Direction (Inward)     Pattern 2: Same Direction (Fast & Slow)
    L ────────►       ◄──────── R                Slow ──►      Fast ────►
[  1,   3,   5,   8,  11,  15,  20 ]        [  0,   1,   0,   3,  12 ]
(Used in Two Sum Sorted, Palindromes)      (Used in Remove Duplicates, Move Zeroes)
```

| Type | Pointer Movement | Typical Use Cases |
| :--- | :--- | :--- |
| **Opposite Ends** | `left` increments, `right` decrements | Sorted Two Sum, Container with Most Water, Palindrome verification |
| **Fast & Slow** | `slow` writes on valid condition, `fast` scans all | In-place removal, Linked list cycle detection, Duplicate detection |
| **Sliding Window** | `right` expands, `left` contracts | Substring with distinct chars, Min window substring |
