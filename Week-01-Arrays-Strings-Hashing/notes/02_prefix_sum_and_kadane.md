# 📊 Deep-Dive Notes: Prefix Sum, Difference Arrays & Kadane's Algorithm

---

## 1. The Prefix Sum Pattern

### 1.1 Intuition & Core Formula
When answering multiple range sum queries $[L, R]$ on an immutable array, a naive loop takes $O(N)$ per query ($O(Q \cdot N)$ total).

With a **Prefix Sum Array**, preprocessing takes $O(N)$ once, and every subsequent range sum query takes **$O(1)$ constant time**!

$$\text{Prefix}[i] = \sum_{j=0}^{i} \text{arr}[j] = \text{Prefix}[i-1] + \text{arr}[i]$$

To find the sum of elements from index $L$ to $R$:

$$\text{Sum}(L, R) = \text{Prefix}[R] - \text{Prefix}[L-1] \quad (\text{if } L > 0)$$

```
Index:       0    1    2    3    4    5
Array:     [ 2,   4,   1,   7,   3,   5 ]
Prefix:    [ 2,   6,   7,  14,  17,  22 ]

Sum(2, 4) = arr[2] + arr[3] + arr[4] = 1 + 7 + 3 = 11
Using Prefix: Prefix[4] - Prefix[1] = 17 - 6 = 11  ⚡ (O(1) calculation!)
```

---

### 1.2 2D Prefix Sum (Matrix Range Sum Query)
For an $M \times N$ 2D matrix, to compute the sum of submatrix $(r_1, c_1)$ to $(r_2, c_2)$:

#### Construction ($O(M \times N)$):
$$\text{Prefix}[r][c] = \text{Matrix}[r][c] + \text{Prefix}[r-1][c] + \text{Prefix}[r][c-1] - \text{Prefix}[r-1][c-1]$$

#### Query ($O(1)$):
$$\text{Sum} = \text{Prefix}[r_2][c_2] - \text{Prefix}[r_1-1][c_2] - \text{Prefix}[r_2][c_1-1] + \text{Prefix}[r_1-1][c_1-1]$$

```
Matrix Region Decomposition:
┌──────────────┬──────────────────┐
│              │                  │
│   (r1-1, c1-1)│     (r1-1, c2)   │
│              │                  │
├──────────────┼──────────────────┤
│              │                  │
│   (r2, c1-1) │   Target [r1..r2]│
│              │          [c1..c2]│
└──────────────┴──────────────────┘
```

---

## 2. Difference Array (Range Updates in $O(1)$)

If you need to perform $Q$ operations of the type: *"Add value $V$ to all elements in range $[L, R]$"*, and then query the final array:
- Naive: $O(Q \cdot N)$
- **Difference Array**: $O(Q + N)$

### How it works:
1. Define $\text{Diff}[i] = \text{arr}[i] - \text{arr}[i-1]$ (with $\text{Diff}[0] = \text{arr}[0]$).
2. To update range $[L, R]$ with $+V$:
   - $\text{Diff}[L] += V$
   - $\text{Diff}[R+1] -= V$ (if $R+1 < N$)
3. Compute the running prefix sum of $\text{Diff}$ to reconstruct the final updated array in $O(N)$!

---

## 3. Kadane's Algorithm (Maximum Subarray Problem)

### 3.1 The Fundamental Question
Given an integer array `nums`, find the contiguous subarray with the largest sum and return its sum.

### 3.2 Dynamic Programming Intuition
At every index $i$, we face a binary choice:
1. **Extend** the current running subarray sum: `current_sum + nums[i]`
2. **Start fresh** with a new subarray starting at `nums[i]`: `nums[i]`

$$\text{current\_sum}_i = \max(\text{nums}[i], \text{current\_sum}_{i-1} + \text{nums}[i])$$
$$\text{max\_sum} = \max(\text{max\_sum}, \text{current\_sum}_i)$$

### 3.3 Visual Dry-Run

Array: `[-2, 1, -3, 4, -1, 2, 1, -5, 4]`

| Index | Value | `current_sum = max(x, current_sum + x)` | `max_so_far` | Decision |
| :---: | :---: | :---: | :---: | :--- |
| 0 | -2 | -2 | -2 | Start at -2 |
| 1 | 1 | $\max(1, -2 + 1) = \mathbf{1}$ | 1 | Start fresh at 1 |
| 2 | -3 | $\max(-3, 1 + (-3)) = \mathbf{-2}$ | 1 | Extend with -3 |
| 3 | 4 | $\max(4, -2 + 4) = \mathbf{4}$ | 4 | Start fresh at 4 |
| 4 | -1 | $\max(-1, 4 + (-1)) = \mathbf{3}$ | 4 | Extend with -1 |
| 5 | 2 | $\max(2, 3 + 2) = \mathbf{5}$ | 5 | Extend with 2 |
| 6 | 1 | $\max(1, 5 + 1) = \mathbf{6}$ | **6** | Extend with 1 (Max subarray `[4, -1, 2, 1]`) |
| 7 | -5 | $\max(-5, 6 + (-5)) = \mathbf{1}$ | 6 | Extend with -5 |
| 8 | 4 | $\max(4, 1 + 4) = \mathbf{5}$ | 6 | Extend with 4 |

**Result**: $6$  
**Time Complexity**: $O(N)$  
**Space Complexity**: $O(1)$

```python
def maxSubArray(nums: list[int]) -> int:
    current_sum = nums[0]
    max_sum = nums[0]
    
    for num in nums[1:]:
        current_sum = max(num, current_sum + num)
        max_sum = max(max_sum, current_sum)
        
    return max_sum
```
