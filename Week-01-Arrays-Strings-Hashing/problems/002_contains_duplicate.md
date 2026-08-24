# 📌 LeetCode #217: Contains Duplicate

- **Difficulty**: Easy
- **Topic**: Arrays, Hashing
- **Pattern**: Hash Set / Set Membership
- **LeetCode Link**: [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)

---

## 📝 Problem Statement
Given an integer array `nums`, return `true` if any value appears **at least twice** in the array, and return `false` if every element is distinct.

---

## 💡 Intuition & Core Pattern
- **Approach 1 (Sorting)**: Sort `nums` in $O(N \log N)$ and check adjacent elements `nums[i] == nums[i+1]`. Space: $O(1)$ or $O(N)$ depending on sort.
- **Approach 2 (Hash Set - Optimal)**: Maintain a `seen` set. As we iterate through `nums`:
  - If `num` is already in `seen`, return `True` immediately (early exit).
  - Else, insert `num` into `seen`.
  - If we finish the loop, return `False`.

---

## 💻 Solutions

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
```

### C++
```cpp
#include <vector>
#include <unordered_set>

class Solution {
public:
    bool containsDuplicate(std::vector<int>& nums) {
        std::unordered_set<int> seen;
        for (int num : nums) {
            if (seen.find(num) != seen.end()) {
                return true;
            }
            seen.insert(num);
        }
        return false;
    }
};
```

### Java
```java
import java.util.HashSet;
import java.util.Set;

class Solution {
    public boolean containsDuplicate(int[] nums) {
        Set<Integer> seen = new HashSet<>();
        for (int num : nums) {
            if (!seen.add(num)) {
                return true; // add() returns false if already present
            }
        }
        return false;
    }
}
```

---

## ⏱️ Complexity Analysis
- **Time Complexity**: $O(N)$ — Single pass; each set lookup and insertion takes average $O(1)$ time.
- **Space Complexity**: $O(N)$ — Stores up to $N$ unique elements.

---

## 📸 Submission Proof
Add your accepted screenshot here:
`../screenshots/leetcode-0217-contains-duplicate.png`
