# 📌 LeetCode #217: Contains Duplicate

- **Difficulty**: Easy
- **Topic**: Arrays, Hashing
- **Pattern**: Hash Set / Set Membership
- **LeetCode Link**: [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)
- **Verdict**: Accepted (80 / 80 testcases passed ⚡)

---

## 📝 Problem Statement
Given an integer array `nums`, return `true` if any value appears **at least twice** in the array, and return `false` if every element is distinct.

### Examples
- **Example 1**:
  - **Input**: `nums = [1, 2, 3, 1]`
  - **Output**: `true`
  - **Explanation**: `1` appears at index `0` and `3`.
- **Example 2**:
  - **Input**: `nums = [1, 2, 3, 4]`
  - **Output**: `false`
  - **Explanation**: All elements are distinct.
- **Example 3**:
  - **Input**: `nums = [1, 1, 1, 3, 3, 4, 3, 2, 4, 2]`
  - **Output**: `true`

---

## 💡 What Is Happening Under The Hood?

### 1. The Core Invariant: Set Membership
A hash set is backed by an array of buckets where each key is mapped to a bucket via a hash function:
$$\text{bucket\_index} = \text{hash}(x) \pmod{\text{capacity}}$$

When we iterate through `nums`:
1. For each `num`, we query the hash set: *"Has this key already been hashed and inserted into a bucket?"*
2. **If YES**: We found our duplicate! We immediately exit and return `true`.
3. **If NO**: We place `num` into its corresponding bucket and continue.
4. If the loop ends without any duplicate found, all elements are unique; return `false`.

```
nums = [1, 2, 3, 1]

Step 1: num = 1 ──► seen.find(1) == seen.end() ──► seen.insert(1) ──► seen = {1}
Step 2: num = 2 ──► seen.find(2) == seen.end() ──► seen.insert(2) ──► seen = {1, 2}
Step 3: num = 3 ──► seen.find(3) == seen.end() ──► seen.insert(3) ──► seen = {1, 2, 3}
Step 4: num = 1 ──► seen.find(1) != seen.end() ──► DUPLICATE FOUND! Return true ⚡
```

### 2. Comparison of the 3 Standard Approaches

| Approach | Time Complexity | Space Complexity | Pros / Cons |
| :--- | :---: | :---: | :--- |
| **Brute Force** | $O(N^2)$ | $O(1)$ | Nested loops compare every pair $(i, j)$. Unacceptable on $N = 10^5$. |
| **In-Place Sorting** | $O(N \log N)$ | $O(1)$ | Sort array first, then check if `nums[i] == nums[i+1]`. Ideal if extra space is prohibited. |
| **Hash Set (Optimal)** | $O(N)$ | $O(N)$ | Single pass with average $O(1)$ lookup and early termination. Fast and standard. |

---

## 💻 Solutions

### C++ (Your Accepted Solution)
```cpp
#include <vector>
#include <unordered_set>

using namespace std;

class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        unordered_set<int> seen;
        
        for (int num : nums) {
            // If already present in our set, duplicate found
            if (seen.find(num) != seen.end()) {
                return true;
            }
            seen.insert(num);
        }
        
        return false;
    }
};
```

> [!TIP]
> **C++ Pro-Tip (Single Lookup Insertion)**:  
> In C++, `std::unordered_set::insert()` returns a `std::pair<iterator, bool>`. The `bool` is `false` if the item was **already** in the set!  
> You can combine the lookup and insert into a single operation:
> ```cpp
> for (int num : nums) {
>     if (!seen.insert(num).second) return true;
> }
> ```

### Python 3
```python
class Solution:
    def containsDuplicate(self, nums: list[int]) -> bool:
        seen = set()
        for num in nums:
            if num in seen:
                return True
            seen.add(num)
        return False

    # One-liner Python alternative:
    # return len(nums) != len(set(nums))
```

### Java
```java
import java.util.HashSet;
import java.util.Set;

class Solution {
    public boolean containsDuplicate(int[] nums) {
        Set<Integer> seen = new HashSet<>();
        for (int num : nums) {
            // Set.add() returns false if element already exists
            if (!seen.add(num)) {
                return true;
            }
        }
        return false;
    }
}
```

---

## 🔍 Dry-Run Table

Input: `nums = [1, 2, 3, 1]`

| Step | Current `num` | `seen.find(num) != seen.end()` | `seen` Set After Step | Early Exit? |
| :-: | :-: | :-: | :--- | :-: |
| **1** | `1` | ❌ No | `{1}` | No |
| **2** | `2` | ❌ No | `{1, 2}` | No |
| **3** | `3` | ❌ No | `{1, 2, 3}` | No |
| **4** | `1` | ✅ **Yes!** (already in set) | `{1, 2, 3}` | **Return `true`** ⚡ |

---

## ⏱️ Complexity Analysis
- **Time Complexity**:
  - **Average Case**: $O(N)$ — We traverse `nums` at most once, and each hash set lookup/insertion takes $O(1)$ average time.
  - **Best Case**: $O(1)$ — If the first two elements are identical (e.g., `[2, 2, ...]`), the algorithm returns `true` immediately after 2 steps.
  - **Worst Case**: $O(N)$ — When all elements are unique or the duplicate is at the very end.
- **Space Complexity**: $O(N)$
  - In the worst case (all elements unique), `seen` stores all $N$ elements.

---

## 🧠 Key Learnings & Mental Models to Remember

1. **Early Exit vs Full Traversal**:
   - Unlike problems that require calculating global counts or indices (like Two Sum), existence queries allow **early exit**. Never keep iterating once the condition has been proven true.
2. **Set vs. Hash Map**:
   - Use a **Hash Map** when you need to associate keys with values (such as value $\to$ index in Two Sum).
   - Use a **Hash Set** when you only care about binary membership (*"Have I seen this before?"*).
3. **The Duplicate Detection Pattern Across DSA**:
   - **Contains Duplicate II (Within distance $k$)**: Combine a Hash Set with a **Sliding Window of size $k$** (evict `nums[i - k]` as the window moves).
   - **Find the Duplicate Number (Immutable, $O(1)$ space)**: Use **Floyd's Tortoise and Hare (Cycle Detection)** treating values as pointers.
   - **First Missing Positive**: In-place array indexing / cyclic placement.

---

## 📸 Submission Proof

![LeetCode #217 Contains Duplicate Accepted Proof](../screenshots/leetcode-0217-contains-duplicate.png)
