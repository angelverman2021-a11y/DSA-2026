# 📌 LeetCode #1: Two Sum

- **Difficulty**: Easy
- **Topic**: Arrays, Hashing
- **Pattern**: Hash Map (Complement Lookup)
- **LeetCode Link**: [Two Sum](https://leetcode.com/problems/two-sum/)
- **Verdict**: Accepted (Runtime: 0 ms ⚡)

---

## 📝 Problem Statement
Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to `target`.
You may assume that each input would have exactly one solution, and you may not use the same element twice.

---

## 💡 Intuition & Core Pattern
- **Brute Force ($O(N^2)$)**: Check every pair $(i, j)$ with two nested loops.
- **Optimal ($O(N)$)**: As we traverse each element $x$ at index $i$, the number we need to reach `target` is:
  $$\text{complement} = \text{target} - x$$
  If `complement` is already stored in our hash map, we found our pair! Otherwise, we record $x \to i$ in the map and keep moving.

```
nums = [2, 7, 11, 15], target = 9

i=0, num=2  ──► Needed: (9 - 2) = 7. Map: {}              ──► Store {2: 0}
i=1, num=7  ──► Needed: (9 - 7) = 2. Map: {2: 0} (FOUND!) ──► Return [0, 1] ⚡
```

---

## 💻 Solutions

### C++ (Optimal 0 ms Solution)
```cpp
#include <vector>
#include <unordered_map>

using namespace std;

class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> seen;
        for (int i = 0; i < nums.size(); ++i) {
            int complement = target - nums[i];
            if (seen.find(complement) != seen.end()) {
                return {seen[complement], i};
            }
            seen[nums[i]] = i;
        }
        return {};
    }
};
```

### Python 3
```python
class Solution:
    def twoSum(self, nums: list[int], target: int) -> list[int]:
        seen = {}
        for i, num in enumerate(nums):
            complement = target - num
            if complement in seen:
                return [seen[complement], i]
            seen[num] = i
        return []
```

### Java
```java
import java.util.HashMap;
import java.util.Map;

class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> seen = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];
            if (seen.containsKey(complement)) {
                return new int[] { seen.get(complement), i };
            }
            seen.put(nums[i], i);
        }
        return new int[0];
    }
}
```

---

## 🔍 Dry-Run Table

Input: `nums = [3, 2, 4]`, `target = 6`

| Step | Index $i$ | Value `num` | `complement = 6 - num` | Map Before Check | Found? | Action |
| :-: | :-: | :-: | :-: | :-: | :-: | :--- |
| 1 | 0 | 3 | 3 | `{}` | No | Insert `{3: 0}` |
| 2 | 1 | 2 | 4 | `{3: 0}` | No | Insert `{2: 1}` |
| 3 | 2 | 4 | 2 | `{3: 0, 2: 1}` | **Yes!** (at idx 1) | **Return `[1, 2]`** |

---

## ⏱️ Complexity Analysis
- **Time Complexity**: $O(N)$ — Single pass through `nums`, each hash map lookup/insertion takes average $O(1)$.
- **Space Complexity**: $O(N)$ — Hash map stores at most $N$ elements.

---

## 🧠 Key Learnings & Mental Models to Remember

1. **Trade Space for Time**:
   - By allocating $O(N)$ memory for an associative map, we eliminate the inner loop, dropping the runtime from $O(N^2)$ to $O(N)$.
2. **One-Pass Look-Behind Pattern**:
   - Rather than scanning ahead for what comes next, we keep an associative memory of where we've already been.
   - Inserting elements *after* checking ensures we never use the same element twice (e.g., $nums[i] * 2 == target$).
   - Handles identical values naturally (e.g. `[3, 3]`, target `6` finds the first 3 when at the second 3).
3. **When to Apply in the Future**:
   - **3Sum ($a + b + c = 0$)**: Fix one element $a$, then run Two Sum on the remaining subarray.
   - **Subarray Sum Equals K**: Generalizes Two Sum with prefix sums ($\text{prefix}[j] - \text{prefix}[i] = K$).
   - **Sorted Array**: If `nums` is already sorted, use **Two Pointers** (left & right) to solve it in $O(N)$ time with $O(1)$ space.

---

## 📸 Submission Proof

![LeetCode #1 Two Sum Accepted Proof](../screenshots/leetcode-0001-two-sum.png)
