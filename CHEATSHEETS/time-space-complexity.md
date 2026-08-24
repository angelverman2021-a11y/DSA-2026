# ⏱️ Time & Space Complexity Master Cheatsheet

Understanding Big-O complexity and constraints is the #1 superpower in technical interviews and competitive programming.

---

## 🧭 Input Constraints vs. Target Time Complexity

When you read a problem statement, **always look at $N$ (the input size)** first. It tells you the algorithm to design:

| Constraint on $N$ | Expected Time Complexity | Typical Algorithms / Approaches |
| :--- | :--- | :--- |
| $N \le 10$ to $12$ | $O(N!)$ or $O(N^2 \cdot 2^N)$ | Permutations, Traveling Salesperson, Brute-force Recursion |
| $N \le 20$ to $25$ | $O(2^N)$ | Subsets, Backtracking, Meet-in-the-Middle |
| $N \le 100$ | $O(N^4)$ or $O(N^3)$ | 2D/3D Grid DP, Floyd-Warshall, Matrix Multiplication |
| $N \le 500$ | $O(N^3)$ | All-Pairs Shortest Path, Interval DP |
| $N \le 2\,000$ to $5\,000$ | $O(N^2)$ | Nested Loops, 2D DP, Insertion/Selection Sort, Brute-force pairs |
| $N \le 10^5$ to $10^6$ | $O(N \log N)$ or $O(N)$ | Sorting, Binary Search, Heaps, Sliding Window, Two Pointers, Prefix Sum, Trees, Graphs (BFS/DFS) |
| $N \le 10^8$ to $10^9$ | $O(\log N)$ or $O(\sqrt{N})$ | Binary Search, Sqrt Decomposition, Math / Number Theory, GCD |
| $N > 10^9$ | $O(1)$ or $O(\log N)$ | Closed-form formulas, Matrix Exponentiation, Fast Power |

> ⚡ **Golden Rule of 1 Second**: Most online judges (LeetCode, CodeChef, Codeforces) allow **$\approx 10^8$ operations per second**.

---

## 📊 Data Structure Complexities

| Data Structure | Access | Search | Insertion | Deletion | Space |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Array (Static)** | $O(1)$ | $O(N)$ | $O(N)$ | $O(N)$ | $O(N)$ |
| **Dynamic Array (std::vector / ArrayList / list)** | $O(1)$ | $O(N)$ | $O(1)$ amortized | $O(N)$ | $O(N)$ |
| **Singly Linked List** | $O(N)$ | $O(N)$ | $O(1)$ (with pointer) | $O(1)$ (with pointer) | $O(N)$ |
| **Doubly Linked List** | $O(N)$ | $O(N)$ | $O(1)$ | $O(1)$ | $O(N)$ |
| **Hash Table / Hash Map** | N/A | $O(1)$ avg / $O(N)$ worst | $O(1)$ avg / $O(N)$ worst | $O(1)$ avg / $O(N)$ worst | $O(N)$ |
| **Binary Search Tree (Balanced / AVL / Red-Black)** | $O(\log N)$ | $O(\log N)$ | $O(\log N)$ | $O(\log N)$ | $O(N)$ |
| **Binary Heap (Priority Queue)** | $O(1)$ (find min/max) | $O(N)$ | $O(\log N)$ | $O(\log N)$ (extract) | $O(N)$ |
| **Trie (Prefix Tree)** | $O(L)$ | $O(L)$ | $O(L)$ | $O(L)$ | $O(N \cdot L \cdot \Sigma)$ |
| **Disjoint Set Union (DSU with Path Compression + Rank)** | N/A | $O(\alpha(N)) \approx O(1)$ | $O(\alpha(N)) \approx O(1)$ | N/A | $O(N)$ |

*($L = \text{length of word}, \Sigma = \text{alphabet size}, \alpha = \text{Inverse Ackermann function}$)*

---

## 🔄 Sorting Algorithms Complexities

| Algorithm | Best Time | Average Time | Worst Time | Space Complexity | Stable? | In-Place? |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **Quick Sort** | $O(N \log N)$ | $O(N \log N)$ | $O(N^2)$ | $O(\log N)$ (stack) | No | Yes |
| **Merge Sort** | $O(N \log N)$ | $O(N \log N)$ | $O(N \log N)$ | $O(N)$ | Yes | No |
| **Heap Sort** | $O(N \log N)$ | $O(N \log N)$ | $O(N \log N)$ | $O(1)$ | No | Yes |
| **Counting Sort** | $O(N + K)$ | $O(N + K)$ | $O(N + K)$ | $O(K)$ | Yes | No |
| **Cyclic Sort** | $O(N)$ | $O(N)$ | $O(N)$ | $O(1)$ | No | Yes |
| **Insertion Sort** | $O(N)$ | $O(N^2)$ | $O(N^2)$ | $O(1)$ | Yes | Yes |
