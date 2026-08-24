# 🧱 Deep-Dive Notes: Array Fundamentals & Memory Layout

---

## 1. What is an Array?

An **Array** is a linear data structure consisting of a collection of elements, each identified by at least one array index or key. In memory, an array is stored as a **single contiguous block of bytes**.

```
Memory Address:   0x1000   0x1004   0x1008   0x100C   0x1010
                 ┌────────┬────────┬────────┬────────┬────────┐
Array Elements:  │   10   │   25   │   30   │   45   │   90   │
                 └────────┴────────┴────────┴────────┴────────┘
Index:               0        1        2        3        4
```

---

## 2. The Mechanics of $O(1)$ Random Access

Why can we access `arr[i]` in strictly **$O(1)$ constant time**, regardless of how large the array is?

Because of **Direct Memory Address Calculation**:

$$\text{Address}(\text{arr}[i]) = \text{Base Address} + (i \times \text{Size of Element in Bytes})$$

### Example:
For an integer array (`int` = 4 bytes) starting at base address `0x1000`:
- $\text{Address}(\text{arr}[0]) = 0x1000 + (0 \times 4) = 0x1000$
- $\text{Address}(\text{arr}[3]) = 0x1000 + (3 \times 4) = 0x1000 + 12 = 0x100C$

The CPU executes a single addition and multiplication in hardware—no iteration needed.

---

## 3. CPU Cache Locality & Spatial Locality

Arrays are dramatically faster in real-world performance compared to Linked Lists because of **CPU Caching**:
- When the CPU fetches `arr[0]` from RAM, the hardware memory controller fetches an entire **Cache Line** (typically **64 contiguous bytes**) into L1/L2/L3 cache.
- When your loop moves to `arr[1]`, `arr[2]`, `arr[3]`, they are already sitting in the blazing-fast L1 cache (**Cache Hit**, latency $\approx 1$ ns).
- Linked lists scatter nodes randomly across the heap, causing frequent **Cache Misses** (RAM latency $\approx 50\text{--}100$ ns).

```
RAM (Contiguous Array Elements):
[ arr[0] | arr[1] | arr[2] | arr[3] | arr[4] | arr[5] | ... ]
    │
    ▼ Loaded in ONE 64-byte burst into L1 Cache Line
[ L1 Cache: arr[0], arr[1], arr[2], arr[3], arr[4], arr[5] ]  --> Instant Access!
```

---

## 4. Static Arrays vs. Dynamic Arrays

| Feature | Static Array (`int arr[N]`) | Dynamic Array (`std::vector`, `ArrayList`, `list`) |
| :--- | :--- | :--- |
| **Size** | Fixed at compile time | Grows dynamically at runtime |
| **Location** | Stack (or static memory) | Elements live on the Heap, metadata on Stack |
| **Growth Strategy** | Cannot grow | Capacity doubling ($1 \to 2 \to 4 \to 8 \to 16...$) |
| **Insertion at End**| $O(1)$ (if within bounds) | **$O(1)$ Amortized** ($O(N)$ during resize) |

### 🔍 Proof of $O(1)$ Amortized Insertion
When a dynamic array runs out of capacity:
1. Allocates a new array of size $2 \times \text{Capacity}$.
2. Copies all $N$ existing elements to the new array.
3. Deallocates the old array.

**Cost Analysis over $N$ insertions:**
- Total copy operations: $1 + 2 + 4 + 8 + \dots + N = 2N - 1 < 2N$.
- Total insertions: $N$.
- Amortized cost per insertion = $\frac{\text{Total Cost}}{N} = \frac{N + 2N}{N} = \mathbf{O(1)}$.

---

## 5. Core Array Operations & Complexities

| Operation | Beginning | Middle (Index $k$) | End |
| :--- | :---: | :---: | :---: |
| **Access (`arr[i]`)** | $O(1)$ | $O(1)$ | $O(1)$ |
| **Search (Unsorted)** | $O(N)$ | $O(N)$ | $O(N)$ |
| **Search (Sorted)** | $O(\log N)$ | $O(\log N)$ | $O(\log N)$ |
| **Insert** | $O(N)$ (requires right shift) | $O(N - k)$ | $O(1)$ amortized |
| **Delete** | $O(N)$ (requires left shift) | $O(N - k)$ | $O(1)$ |

---

## 6. Fundamental Algorithmic Techniques on Arrays

### 6.1 In-Place Array Reversal
To reverse an array in $O(N)$ time and $O(1)$ space, use two pointers moving inward:

```
Step 0: [ 1, 2, 3, 4, 5 ]    L=0, R=4 -> Swap 1 and 5
Step 1: [ 5, 2, 3, 4, 1 ]    L=1, R=3 -> Swap 2 and 4
Step 2: [ 5, 4, 3, 2, 1 ]    L=2, R=2 -> Stop (L >= R)
```

```python
def reverse_array(arr, left, right):
    while left < right:
        arr[left], arr[right] = arr[right], arr[left]
        left += 1
        right -= 1
```

---

### 6.2 Array Rotation by $K$ Elements (3-Step Reversal Pattern)
To rotate `arr` to the right by $K$ steps ($K = K \pmod N$):
1. Reverse the entire array: `reverse(0, N - 1)`
2. Reverse the first $K$ elements: `reverse(0, K - 1)`
3. Reverse the remaining $N - K$ elements: `reverse(K, N - 1)`

**Trace for `[1, 2, 3, 4, 5, 6, 7]`, $K = 3$:**
1. Reverse all: `[7, 6, 5, 4, 3, 2, 1]`
2. Reverse first 3 (`0` to `2`): `[5, 6, 7, 4, 3, 2, 1]`
3. Reverse last 4 (`3` to `6`): `[5, 6, 7, 1, 2, 3, 4]` ✅ *(Rotated by 3!)*

**Time Complexity**: $O(N)$  
**Space Complexity**: $O(1)$ (In-place, no extra buffer needed!)

---

### 6.3 Two Pointers: Slow & Fast (In-Place Overwrite)
Used for problems like **Remove Duplicates** (LeetCode #26) or **Move Zeroes** (LeetCode #283).

- **Slow Pointer (`write_idx`)**: Tracks the position where the next valid element should be placed.
- **Fast Pointer (`read_idx`)**: Scans through the entire array.

```python
def move_zeroes(nums):
    write_idx = 0
    # Pass 1: Write all non-zero elements forward
    for read_idx in range(len(nums)):
        if nums[read_idx] != 0:
            nums[write_idx] = nums[read_idx]
            write_idx += 1
            
    # Pass 2: Fill remaining positions with zero
    while write_idx < len(nums):
        nums[write_idx] = 0
        write_idx += 1
```
