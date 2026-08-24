# 📌 LeetCode #26: Remove Duplicates from Sorted Array

- **Difficulty**: Easy
- **Topic**: Arrays, Two Pointers
- **Pattern**: Slow & Fast Pointers (Unique Boundary Tracking)
- **LeetCode Link**: [Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

---

## 📝 Problem Statement
Given an integer array `nums` sorted in **non-decreasing order**, remove the duplicates **in-place** such that each unique element appears only once. The relative order of the elements should be kept the same. Then return the number of unique elements in `nums`.

---

## 💡 Intuition & Core Pattern: Slow & Fast Pointers
Because the array is already **sorted**, duplicate elements are guaranteed to be adjacent.

- `slow = 0`: Index of the last placed unique element.
- `fast = 1`: Scans forward.
- When `nums[fast] != nums[slow]`:
  - Increment `slow += 1`
  - Overwrite `nums[slow] = nums[fast]`
- Return `slow + 1` (the length of the unique prefix).

```
nums = [0, 0, 1, 1, 1, 2, 2, 3, 3, 4]

slow=0, fast=1 (0 == 0) ──► Skip
slow=0, fast=2 (1 != 0) ──► slow=1, nums[1]=1 ──► [0, 1, ...]
slow=1, fast=3 (1 == 1) ──► Skip
slow=1, fast=4 (1 == 1) ──► Skip
slow=1, fast=5 (2 != 1) ──► slow=2, nums[2]=2 ──► [0, 1, 2, ...]
...
Result: k = 5 unique elements: [0, 1, 2, 3, 4]
```

---

## 💻 Solutions

### Python 3
```python
class Solution:
    def removeDuplicates(self, nums: list[int]) -> int:
        if not nums:
            return 0
            
        slow = 0
        for fast in range(1, len(nums)):
            if nums[fast] != nums[slow]:
                slow += 1
                nums[slow] = nums[fast]
                
        return slow + 1
```

### C++
```cpp
#include <vector>

class Solution {
public:
    int removeDuplicates(std::vector<int>& nums) {
        if (nums.empty()) return 0;
        
        int slow = 0;
        for (int fast = 1; fast < nums.size(); ++fast) {
            if (nums[fast] != nums[slow]) {
                slow++;
                nums[slow] = nums[fast];
            }
        }
        return slow + 1;
    }
};
```

### Java
```java
class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums.length == 0) return 0;
        
        int slow = 0;
        for (int fast = 1; fast < nums.length; fast++) {
            if (nums[fast] != nums[slow]) {
                slow++;
                nums[slow] = nums[fast];
            }
        }
        return slow + 1;
    }
}
```

---

## ⏱️ Complexity Analysis
- **Time Complexity**: $O(N)$ — Single pass where `fast` traverses $N$ elements.
- **Space Complexity**: $O(1)$ — In-place updates without extra arrays.

---

## 📸 Submission Proof
Add your accepted screenshot here:
`../screenshots/leetcode-0026-remove-duplicates-from-sorted-array.png`
