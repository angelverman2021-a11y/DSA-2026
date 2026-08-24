# 📌 LeetCode #53: Maximum Subarray

- **Difficulty**: Medium
- **Topic**: Arrays, Dynamic Programming
- **Pattern**: Kadane's Algorithm
- **LeetCode Link**: [Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)

---

## 📝 Problem Statement
Given an integer array `nums`, find the subarray with the largest sum, and return its sum.

---

## 💡 Intuition & Core Pattern: Kadane's Algorithm
At each index $i$, we ask: *"Is it better to add `nums[i]` to our current ongoing subarray sum, or discard all previous elements and start a brand new subarray from `nums[i]`?"*

$$\text{current\_sum} = \max(\text{nums}[i], \text{current\_sum} + \text{nums}[i])$$
$$\text{max\_sum} = \max(\text{max\_sum}, \text{current\_sum})$$

If `current_sum` drops below zero, adding it to the next number would only hurt our future sum, so we reset/start fresh.

---

## 💻 Solutions

### Python 3
```python
class Solution:
    def maxSubArray(self, nums: list[int]) -> int:
        current_sum = nums[0]
        max_sum = nums[0]
        
        for num in nums[1:]:
            current_sum = max(num, current_sum + num)
            max_sum = max(max_sum, current_sum)
            
        return max_sum
```

### C++
```cpp
#include <vector>
#include <algorithm>

class Solution {
public:
    int maxSubArray(std::vector<int>& nums) {
        int current_sum = nums[0];
        int max_sum = nums[0];
        
        for (size_t i = 1; i < nums.size(); ++i) {
            current_sum = std::max(nums[i], current_sum + nums[i]);
            max_sum = std::max(max_sum, current_sum);
        }
        
        return max_sum;
    }
};
```

### Java
```java
class Solution {
    public int maxSubArray(int[] nums) {
        int currentSum = nums[0];
        int maxSum = nums[0];
        
        for (int i = 1; i < nums.length; i++) {
            currentSum = Math.max(nums[i], currentSum + nums[i]);
            maxSum = Math.max(maxSum, currentSum);
        }
        
        return maxSum;
    }
}
```

---

## ⏱️ Complexity Analysis
- **Time Complexity**: $O(N)$ — Single pass through `nums`.
- **Space Complexity**: $O(1)$ — Only two scalar accumulator variables (`current_sum`, `max_sum`).

---

## 📸 Submission Proof
Add your accepted screenshot here:
`../screenshots/leetcode-0053-maximum-subarray.png`
