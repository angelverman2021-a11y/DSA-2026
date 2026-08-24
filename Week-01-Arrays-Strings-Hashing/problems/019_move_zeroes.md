# 📌 LeetCode #283: Move Zeroes

- **Difficulty**: Easy
- **Topic**: Arrays, Two Pointers
- **Pattern**: Slow & Fast Pointers (In-Place Overwrite)
- **LeetCode Link**: [Move Zeroes](https://leetcode.com/problems/move-zeroes/)

---

## 📝 Problem Statement
Given an integer array `nums`, move all `0`'s to the end of it while maintaining the relative order of the non-zero elements.
**Note**: You must do this **in-place** without making a copy of the array.

---

## 💡 Intuition & Core Pattern: Slow & Fast Pointers
Maintain two pointers:
- `write_idx`: Position to place the next non-zero element.
- `read_idx`: Iterates through the entire array.

Whenever `nums[read_idx] != 0`, we swap or place it at `nums[write_idx]` and increment `write_idx`.

```
nums = [0, 1, 0, 3, 12]

read_idx=0 (val=0)  ──► Skip
read_idx=1 (val=1)  ──► Swap nums[0] & nums[1] ──► [1, 0, 0, 3, 12], write_idx=1
read_idx=2 (val=0)  ──► Skip
read_idx=3 (val=3)  ──► Swap nums[1] & nums[3] ──► [1, 3, 0, 0, 12], write_idx=2
read_idx=4 (val=12) ──► Swap nums[2] & nums[4] ──► [1, 3, 12, 0, 0],  write_idx=3 ✅
```

---

## 💻 Solutions

### Python 3
```python
class Solution:
    def moveZeroes(self, nums: list[int]) -> None:
        write_idx = 0
        for read_idx in range(len(nums)):
            if nums[read_idx] != 0:
                nums[write_idx], nums[read_idx] = nums[read_idx], nums[write_idx]
                write_idx += 1
```

### C++
```cpp
#include <vector>
#include <algorithm>

class Solution {
public:
    void moveZeroes(std::vector<int>& nums) {
        int write_idx = 0;
        for (int read_idx = 0; read_idx < nums.size(); ++read_idx) {
            if (nums[read_idx] != 0) {
                std::swap(nums[write_idx], nums[read_idx]);
                write_idx++;
            }
        }
    }
};
```

### Java
```java
class Solution {
    public void moveZeroes(int[] nums) {
        int writeIdx = 0;
        for (int readIdx = 0; readIdx < nums.length; readIdx++) {
            if (nums[readIdx] != 0) {
                int temp = nums[writeIdx];
                nums[writeIdx] = nums[readIdx];
                nums[readIdx] = temp;
                writeIdx++;
            }
        }
    }
}
```

---

## ⏱️ Complexity Analysis
- **Time Complexity**: $O(N)$ — Single pass through `nums`.
- **Space Complexity**: $O(1)$ — In-place swap without auxiliary memory.

---

## 📸 Submission Proof
Add your accepted screenshot here:
`../screenshots/leetcode-0283-move-zeroes.png`
