# 🚀 DSA-2026: 8-Week Data Structures & Algorithms Mastery

[![Target Problems](https://img.shields.io/badge/Target%20Problems-250--300-brightgreen.svg)](#-master-roadmap)
[![Duration](https://img.shields.io/badge/Duration-8%20Weeks-orange.svg)](#-master-roadmap)
[![Focus](https://img.shields.io/badge/Focus-Patterns%20%26%20Intuition-blue.svg)](#-core-patterns-covered)
[![Platforms](https://img.shields.io/badge/Platforms-LeetCode%20%7C%20CodeChef%20%7C%20GFG-yellow.svg)](#-submission-proofs)

Welcome to **DSA-2026**, an intensive 8-week structured roadmap engineered to build deep algorithmic problem-solving intuition, master all essential data structures, and solve **250–300 quality problems** across LeetCode, CodeChef, and GeeksforGeeks.

---

## 📌 Philosophy: Patterns Over Memorization

Instead of memorizing hundreds of ad-hoc solutions, this repository classifies problems into repeatable **algorithmic patterns**:

```
[ Problem Statement ] ──► [ Pattern Identification ] ──► [ Invariant & State ] ──► [ Optimal Solution (O(1) / O(N)) ]
```

---

## 🗓️ Master 8-Week Roadmap

| Week | Core Focus Area | Core Patterns & Topics | Target Problems | Status |
| :---: | :--- | :--- | :---: | :---: |
| [**Week 01**](./Week-01-Arrays-Strings-Hashing/) | **Arrays, Strings & Hashing** | Contiguous Memory, Prefix Sum, Kadane's Algorithm, Frequency Hash Maps, Two-Sum Patterns | 35 | 🟢 Active |
| [**Week 02**](./Week-02-TwoPointers-SlidingWindow-Sorting/) | **Two Pointers, Sliding Window & Sorting** | Opposite/Fast-Slow Pointers, Fixed & Variable Sliding Window, Cyclic Sort, Dutch National Flag | 35 | ⚪ Upcoming |
| [**Week 03**](./Week-03-BinarySearch-BitManipulation/) | **Binary Search & Bit Manipulation** | Search Space Monotonicity, Search-on-Answer, 2D Matrix Search, Bitwise XOR/Masking | 35 | ⚪ Upcoming |
| [**Week 04**](./Week-04-Recursion-Backtracking-LinkedList/) | **Recursion, Backtracking & Linked Lists** | Decision Trees, Pruning, State Space Search, Floyd's Cycle Detection, In-place List Reversal | 35 | ⚪ Upcoming |
| [**Week 05**](./Week-05-Stack-Queue-Monotonic/) | **Stacks, Queues & Monotonic Structures** | Next Greater Element, Monotonic Queue/Deque, Min-Stack, Sliding Window Max | 35 | ⚪ Upcoming |
| [**Week 06**](./Week-06-Trees-BST-Heaps/) | **Binary Trees, BST & Priority Queues** | Tree DFS/BFS Traversals, LCA, Diameter, BST Properties, Top-K Elements, K-Way Merge | 40 | ⚪ Upcoming |
| [**Week 07**](./Week-07-Greedy-Graphs/) | **Greedy Algorithms & Graph Theory** | Interval Scheduling, BFS/DFS Traversal, Topological Sort (Kahn's), Dijkstra, DSU | 40 | ⚪ Upcoming |
| [**Week 08**](./Week-08-DynamicProgramming-Advanced/) | **Dynamic Programming & Systematized Review** | 1D/2D DP, 0/1 Knapsack, Longest Common Subsequence, LIS, Interval DP, Hard Problem Drill | 45 | ⚪ Upcoming |
| **Total** | | | **~300** | |

---

## 📊 Global Progress Tracker

Track daily progress, problem difficulty distribution, and links to your code and screenshots in [`PROGRESS_TRACKER.md`](./PROGRESS_TRACKER.md).

```
Total Problems Target: [ 300 ]
Solved:                [  0  ]
Easy:                  [  0  ] / ~100
Medium:                [  0  ] / ~170
Hard:                  [  0  ] / ~30
```

---

## 📂 Repository Directory Layout

```
DSA-2026/
├── README.md                                    <-- You are here
├── PROGRESS_TRACKER.md                          <-- Interactive problem checklist
├── CHEATSHEETS/                                 <-- Big-O & Pattern Quick-Reference Guides
│   ├── time-space-complexity.md
│   └── patterns-summary.md
├── Week-01-Arrays-Strings-Hashing/              <-- Week 1: Foundations
│   ├── README.md                                <-- Theory, Visual Diagrams & Problem Table
│   ├── notes/                                   <-- Detailed conceptual explanations
│   │   ├── 01_array_fundamentals.md
│   │   ├── 02_prefix_sum_and_kadane.md
│   │   └── 03_hashing_and_two_pointers.md
│   ├── problems/                                <-- Problem solutions (C++, Java, Python)
│   └── screenshots/                             <-- LeetCode / CodeChef submission proofs
├── Week-02-TwoPointers-SlidingWindow-Sorting/
├── Week-03-BinarySearch-BitManipulation/
├── Week-04-Recursion-Backtracking-LinkedList/
├── Week-05-Stack-Queue-Monotonic/
├── Week-06-Trees-BST-Heaps/
├── Week-07-Greedy-Graphs/
└── Week-08-DynamicProgramming-Advanced/
```

---

## 📸 How to Document LeetCode / CodeChef Screenshots

Whenever you solve a problem on LeetCode, CodeChef, or HackerRank:
1. Take a screenshot of the **Accepted / Green Verdict** screen (showing runtime/memory percentiles).
2. Save the image into the corresponding week's `screenshots/` directory:
   `Week-XX-.../screenshots/<platform>-<problem-number>-<problem-title>.png`
   *(Example: `Week-01-Arrays-Strings-Hashing/screenshots/leetcode-0001-two-sum.png`)*
3. Add or link the screenshot in the problem table in `Week-XX-.../README.md` and `PROGRESS_TRACKER.md`.

---

## 🧠 Core Patterns Matrix

| # | Pattern Name | Time Target | Archetypal Problem |
| :-: | :--- | :---: | :--- |
| 1 | **Two Pointers (Opposite Direction)** | $O(N)$ | Valid Palindrome, Two Sum II |
| 2 | **Two Pointers (Same Direction / Fast & Slow)** | $O(N)$ | Remove Duplicates, Linked List Cycle |
| 3 | **Sliding Window (Fixed)** | $O(N)$ | Maximum Sum Subarray of Size K |
| 4 | **Sliding Window (Variable / Dynamic)** | $O(N)$ | Longest Substring Without Repeating Characters |
| 5 | **Prefix Sum & Difference Array** | $O(N)$ / $O(1)$ query | Range Sum Query, Subarray Sum Equals K |
| 6 | **Kadane's Algorithm** | $O(N)$ | Maximum Subarray |
| 7 | **Cyclic Sort** | $O(N)$ | Find Missing Number, First Missing Positive |
| 8 | **Monotonic Stack** | $O(N)$ | Next Greater Element, Daily Temperatures |
| 9 | **Monotonic Deque** | $O(N)$ | Sliding Window Maximum |
| 10 | **Binary Search on Answer** | $O(N \log M)$ | Koko Eating Bananas, Capacity to Ship Packages |
| 11 | **Fast & Slow Pointer (Floyd's Cycle)** | $O(N)$ | Find the Duplicate Number |
| 12 | **Depth-First Search (DFS) / Backtracking** | $O(V+E)$ / $O(2^N)$ | Subsets, Word Search, N-Queens |
| 13 | **Breadth-First Search (BFS) / Level-Order** | $O(V+E)$ | Binary Tree Level Order, Shortest Path in Binary Matrix |
| 14 | **Topological Sort (Kahn's Algorithm)** | $O(V+E)$ | Course Schedule I & II |
| 15 | **Top-K Elements / Priority Queue** | $O(N \log K)$ | Kth Largest Element, Top K Frequent Elements |
| 16 | **Disjoint Set Union (Union-Find)** | $O(N \cdot \alpha(N))$ | Number of Connected Components, Redundant Connection |
| 17 | **Dynamic Programming (1D / 2D / Knapsack)** | $O(N \cdot W)$ | Coin Change, 0/1 Knapsack, Edit Distance |

---

## ⚡ Quick Start: Getting Started with Week 1

Ready to begin? Head straight to **[Week 01: Arrays, Strings & Hashing](./Week-01-Arrays-Strings-Hashing/README.md)**!
