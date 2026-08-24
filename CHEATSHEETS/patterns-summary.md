# 🧩 Algorithmic Patterns Cheat Sheet

A mental decision matrix for quickly mapping problem keywords and constraints to optimal algorithmic patterns.

---

## 🎯 The "If You See... Think..." Decision Guide

| Problem Clue / Keyword | Candidate Pattern / Data Structure | Why? |
| :--- | :--- | :--- |
| **"Find pair/triplet with target sum in sorted array"** | **Two Pointers (Opposite Ends)** | Incremental narrowing from left & right in $O(N)$. |
| **"Longest/shortest continuous subarray / substring satisfying a condition"** | **Sliding Window** | Expands right pointer until invalid, contracts left pointer until valid in $O(N)$. |
| **"Subarray sum equals $K$ / Multiple of $K$"** | **Prefix Sum + Hash Map** | $sum(i, j) = prefix[j] - prefix[i-1] = K \implies prefix[i-1] = prefix[j] - K$. |
| **"Maximum / contiguous subarray sum"** | **Kadane's Algorithm** | Deciding whether to extend the current sum or start fresh at index $i$. |
| **"Array with numbers in range $[1, N]$ or $[0, N]$"** | **Cyclic Sort** | Place value $x$ at index $x - 1$ in $O(N)$ time and $O(1)$ extra space. |
| **"Find next greater / smaller element"** or **"Histogram area"** | **Monotonic Stack** | Maintains elements in strictly increasing/decreasing order. |
| **"Sliding window maximum / minimum in $O(N)$"** | **Monotonic Deque** | Evicts elements smaller than current from back, drops out-of-bounds from front. |
| **"Sorted array / search rotated array / find minimum capacity"** | **Binary Search** | Search space is monotonic or can be modeled with a predicate function `check(mid)`. |
| **"Find duplicate number without extra space in $[1, N]$"** | **Floyd's Tortoise and Hare (Cycle Detection)** | Treat array values as pointers: $i \to nums[i]$. |
| **"Find all permutations / combinations / subsets / valid board configurations"** | **Backtracking / DFS** | Depth-first search with state choice $\to$ recursive call $\to$ state backtrack. |
| **"Shortest path in unweighted graph / Level-by-level traversal"** | **Breadth-First Search (BFS) with Queue** | Explores equidistant nodes tier by tier. |
| **"Prerequisites / Task scheduling with dependencies"** | **Topological Sort (Kahn's / Indegree BFS)** | Resolves DAG ordering by processing nodes with indegree 0. |
| **"Connected components / dynamic connectivity / cycle in undirected graph"** | **Disjoint Set Union (Union-Find)** | Near $O(1)$ `find` and `union` operations. |
| **"Shortest path with non-negative edge weights"** | **Dijkstra's Algorithm (Min-Heap)** | Greedily expands minimum distance node in $O((V+E)\log V)$. |
| **"Find top $K$ largest / smallest elements"** | **Min/Max-Heap (Priority Queue) OR Quickselect** | Maintains heap of size $K$ in $O(N \log K)$ or average $O(N)$ quickselect. |
| **"Optimal substructure + Overlapping subproblems (Max profit, Min cost, Count ways)"** | **Dynamic Programming** | Caching subproblem states (Memoization / Tabulation). |

---

## 🛠️ Essential Code Snippet Templates

### 1. Two Pointers (Opposite Direction)
```python
def two_pointers(arr, target):
    left, right = 0, len(arr) - 1
    while left < right:
        current_sum = arr[left] + arr[right]
        if current_sum == target:
            return [left, right]
        elif current_sum < target:
            left += 1
        else:
            right -= 1
    return []
```

### 2. Sliding Window (Dynamic / Variable Size)
```python
def dynamic_sliding_window(s):
    left = 0
    window_state = {}
    best_result = 0
    
    for right in range(len(s)):
        # 1. Expand window
        window_state[s[right]] = window_state.get(s[right], 0) + 1
        
        # 2. Shrink window while invalid
        while condition_is_violated(window_state):
            window_state[s[left]] -= 1
            left += 1
            
        # 3. Update optimal result
        best_result = max(best_result, right - left + 1)
        
    return best_result
```

### 3. Binary Search on Answer
```python
def binary_search_answer(low, high, check_fn):
    ans = -1
    while low <= high:
        mid = low + (high - low) // 2
        if check_fn(mid):
            ans = mid
            high = mid - 1  # minimize answer, or low = mid + 1 to maximize
        else:
            low = mid + 1
    return ans
```
