# 🗓️ Week 01: Arrays, Strings & Hashing

Welcome to **Week 01** of your 8-Week DSA Journey! This week lays the essential foundation of data structures and algorithms by mastering contiguous memory, amortized analysis, prefix sums, Kadane's algorithm, two-pointer traversals, and hash map indexing.

---

## 🎯 Week 1 Objectives
- **Target Problems**: 35 Problems (15 Easy, 18 Medium, 2 Hard)
- **Core Concepts Mastered**:
  - Memory layout of arrays, cache locality & $O(1)$ random access address formula.
  - In-place modifications and two-pointer traversal strategies.
  - Prefix Sum arrays & 2D Prefix Sum matrices for $O(1)$ range queries.
  - Kadane's algorithm for maximum contiguous subarray sums.
  - Hash Tables: collision resolution, frequency mapping, complement lookups, and prefix sum + hash map integration.

---

## 📅 Daily Study & Practice Schedule

```
┌─────────┬─────────────────────────────────────────────────┬───────────────────────┐
│ Day     │ Focus Topic & Theory                           │ Target Practice       │
├─────────┼─────────────────────────────────────────────────┼───────────────────────┤
│ Day 01  │ Array Basics, Traversal & In-Place Shifts       │ Problems 019, 020, 021│
│ Day 02  │ Array Inversion, Rotation & Running Extremes    │ Problems 010, 018, 022│
│ Day 03  │ Prefix Sum & Difference Arrays                  │ Problems 013, 014, 015│
│ Day 04  │ Kadane's Algorithm & Subarray Products          │ Problems 008, 009, 023│
│ Day 05  │ Hashing Foundations, Sets & Anagrams            │ Problems 001, 002, 003│
│ Day 06  │ Frequency Maps & Subarray Sum with Hashing      │ Problems 004, 005, 011│
│ Day 07  │ String Patterns, Boyer-Moore & Hard Drill       │ Problems 006, 016, 035│
└─────────┴─────────────────────────────────────────────────┴───────────────────────┘
```

---

## 📚 In-Depth Conceptual Notes

1. **[01. Array Fundamentals & In-Place Manipulation](./notes/01_array_fundamentals.md)**:
   - Memory layout, contiguous memory, base address calculation.
   - Static vs Dynamic Arrays (Amortized $O(1)$ vector expansion).
   - Traversal, Insertion, Deletion, Reversal, and 3-step Array Rotation.
2. **[02. Prefix Sum & Kadane's Algorithm](./notes/02_prefix_sum_and_kadane.md)**:
   - 1D & 2D Prefix Sums, range queries in $O(1)$ time.
   - Difference array for batch updates.
   - Kadane's state transition and max product subarrays.
3. **[03. Hashing, Frequency Maps & Two Pointers](./notes/03_hashing_and_two_pointers.md)**:
   - Hash table mechanics, load factor, collisions.
   - Complement lookup pattern (Two Sum).
   - Prefix Sum + Hash Map pattern (Subarray Sum equals K).

---

## 📋 Week 01 Curated Problem List (35 Problems)

| # | Problem Name | Difficulty | Core Pattern | LeetCode Link | Solution Notes | Screenshot Proof | Status |
| :-: | :--- | :---: | :--- | :---: | :---: | :---: | :---: |
| 001 | Two Sum | Easy | Hash Map (Complement) | [LeetCode #1](https://leetcode.com/problems/two-sum/) | [View](./problems/001_two_sum.md) | [Proof](./screenshots/leetcode-0001-two-sum.png) | 🟢 |
| 002 | Contains Duplicate | Easy | Hash Set | [LeetCode #217](https://leetcode.com/problems/contains-duplicate/) | [View](./problems/002_contains_duplicate.md) | [Proof](./screenshots/leetcode-0217-contains-duplicate.png) | 🟢 |
| 003 | Valid Anagram | Easy | Frequency Array | [LeetCode #242](https://leetcode.com/problems/valid-anagram/) | [View](./problems/003_valid_anagram.md) | [Proof](./screenshots/leetcode-0242-valid-anagram.png) | 🟢 |
| 004 | Group Anagrams | Medium | Hash Categorization | [LeetCode #49](https://leetcode.com/problems/group-anagrams/) | [View](./problems/004_group_anagrams.md) | [Proof](./screenshots/leetcode-0049-group-anagrams.png) | 🟢 |
| 005 | Top K Frequent Elements | Medium | Frequency + Bucket Sort | [LeetCode #347](https://leetcode.com/problems/top-k-frequent-elements/) | [View](./problems/005_top_k_frequent_elements.md) | [Proof](./screenshots/) | ⚪ |
| 006 | Product of Array Except Self | Medium | Prefix & Suffix | [LeetCode #238](https://leetcode.com/problems/product-of-array-except-self/) | [View](./problems/006_product_of_array_except_self.md) | [Proof](./screenshots/) | ⚪ |
| 007 | Longest Consecutive Sequence | Medium | Hash Set Expansion | [LeetCode #128](https://leetcode.com/problems/longest-consecutive-sequence/) | [View](./problems/007_longest_consecutive_sequence.md) | [Proof](./screenshots/) | ⚪ |
| 008 | Maximum Subarray | Medium | Kadane's Algorithm | [LeetCode #53](https://leetcode.com/problems/maximum-subarray/) | [View](./problems/008_maximum_subarray.md) | [Proof](./screenshots/) | ⚪ |
| 009 | Maximum Product Subarray | Medium | Kadane's Min/Max | [LeetCode #152](https://leetcode.com/problems/maximum-product-subarray/) | [View](./problems/009_maximum_product_subarray.md) | [Proof](./screenshots/) | ⚪ |
| 010 | Best Time to Buy and Sell Stock | Easy | Running Minimum | [LeetCode #121](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/) | [View](./problems/010_best_time_to_buy_and_sell_stock.md) | [Proof](./screenshots/) | ⚪ |
| 011 | Subarray Sum Equals K | Medium | Prefix Sum + Hash Map | [LeetCode #560](https://leetcode.com/problems/subarray-sum-equals-k/) | [View](./problems/011_subarray_sum_equals_k.md) | [Proof](./screenshots/) | ⚪ |
| 012 | Continuous Subarray Sum | Medium | Prefix Sum Modulo | [LeetCode #523](https://leetcode.com/problems/continuous-subarray-sum/) | [View](./problems/012_continuous_subarray_sum.md) | [Proof](./screenshots/) | ⚪ |
| 013 | Range Sum Query - Immutable | Easy | Prefix Sum Array | [LeetCode #303](https://leetcode.com/problems/range-sum-query-immutable/) | [View](./problems/013_range_sum_query_immutable.md) | [Proof](./screenshots/) | ⚪ |
| 014 | Range Sum Query 2D - Immutable | Medium | 2D Prefix Sum Matrix | [LeetCode #304](https://leetcode.com/problems/range-sum-query-2d-immutable/) | [View](./problems/014_range_sum_query_2d_immutable.md) | [Proof](./screenshots/) | ⚪ |
| 015 | Find Pivot Index | Easy | Total Sum vs Prefix | [LeetCode #724](https://leetcode.com/problems/find-pivot-index/) | [View](./problems/015_find_pivot_index.md) | [Proof](./screenshots/) | ⚪ |
| 016 | Majority Element | Easy | Boyer-Moore Voting | [LeetCode #169](https://leetcode.com/problems/majority-element/) | [View](./problems/016_majority_element.md) | [Proof](./screenshots/) | ⚪ |
| 017 | Majority Element II | Medium | Extended Boyer-Moore | [LeetCode #229](https://leetcode.com/problems/majority-element-ii/) | [View](./problems/017_majority_element_ii.md) | [Proof](./screenshots/) | ⚪ |
| 018 | Rotate Array | Medium | 3-Step Reversal | [LeetCode #189](https://leetcode.com/problems/rotate-array/) | [View](./problems/018_rotate_array.md) | [Proof](./screenshots/) | ⚪ |
| 019 | Move Zeroes | Easy | Two Pointers (Slow/Fast) | [LeetCode #283](https://leetcode.com/problems/move-zeroes/) | [View](./problems/019_move_zeroes.md) | [Proof](./screenshots/leetcode-0283-move-zeroes.png) | 🟢 |
| 020 | Remove Duplicates from Sorted Array | Easy | Two Pointers (Slow/Fast) | [LeetCode #26](https://leetcode.com/problems/remove-duplicates-from-sorted-array/) | [View](./problems/020_remove_duplicates_from_sorted_array.md) | [Proof](./screenshots/leetcode-0026-remove-duplicates-from-sorted-array.png) | 🟢 |
| 021 | Remove Element | Easy | In-Place Partitioning | [LeetCode #27](https://leetcode.com/problems/remove-element/) | [View](./problems/021_remove_element.md) | [Proof](./screenshots/) | ⚪ |
| 022 | Merge Sorted Array | Easy | 3-Pointer Backwards Write | [LeetCode #88](https://leetcode.com/problems/merge-sorted-array/) | [View](./problems/022_merge_sorted_array.md) | [Proof](./screenshots/) | ⚪ |
| 023 | Squares of a Sorted Array | Easy | Two Pointers (Inward) | [LeetCode #977](https://leetcode.com/problems/squares-of-a-sorted-array/) | [View](./problems/023_squares_of_a_sorted_array.md) | [Proof](./screenshots/) | ⚪ |
| 024 | Valid Sudoku | Medium | 3 Hash Sets (Row/Col/Box) | [LeetCode #36](https://leetcode.com/problems/valid-sudoku/) | [View](./problems/024_valid_sudoku.md) | [Proof](./screenshots/) | ⚪ |
| 025 | Encode and Decode Strings | Medium | Length-Prefix Framing | [LeetCode #271](https://leetcode.com/problems/encode-and-decode-strings/) | [View](./problems/025_encode_and_decode_strings.md) | [Proof](./screenshots/) | ⚪ |
| 026 | Longest Common Prefix | Easy | Character Matching | [LeetCode #14](https://leetcode.com/problems/longest-common-prefix/) | [View](./problems/026_longest_common_prefix.md) | [Proof](./screenshots/) | ⚪ |
| 027 | Reverse String | Easy | In-Place Swap | [LeetCode #344](https://leetcode.com/problems/reverse-string/) | [View](./problems/027_reverse_string.md) | [Proof](./screenshots/) | ⚪ |
| 028 | Reverse Words in a String | Medium | Word Tokenization | [LeetCode #151](https://leetcode.com/problems/reverse-words-in-a-string/) | [View](./problems/028_reverse_words_in_a_string.md) | [Proof](./screenshots/) | ⚪ |
| 029 | String to Integer (atoi) | Medium | State Machine | [LeetCode #8](https://leetcode.com/problems/string-to-integer-atoi/) | [View](./problems/029_string_to_integer_atoi.md) | [Proof](./screenshots/) | ⚪ |
| 030 | Isomorphic Strings | Easy | Dual Mapping | [LeetCode #205](https://leetcode.com/problems/isomorphic-strings/) | [View](./problems/030_isomorphic_strings.md) | [Proof](./screenshots/) | ⚪ |
| 031 | Word Pattern | Easy | Bijective Hash Mapping | [LeetCode #290](https://leetcode.com/problems/word-pattern/) | [View](./problems/031_word_pattern.md) | [Proof](./screenshots/) | ⚪ |
| 032 | First Unique Character in a String | Easy | 26-element Frequency | [LeetCode #387](https://leetcode.com/problems/first-unique-character-in-a-string/) | [View](./problems/032_first_unique_character_in_a_string.md) | [Proof](./screenshots/) | ⚪ |
| 033 | Valid Palindrome | Easy | Alphanumeric Two Pointers | [LeetCode #125](https://leetcode.com/problems/valid-palindrome/) | [View](./problems/033_valid_palindrome.md) | [Proof](./screenshots/) | ⚪ |
| 034 | Insert Delete GetRandom O(1) | Medium | Array + Hash Map Index | [LeetCode #380](https://leetcode.com/problems/insert-delete-getrandom-o1/) | [View](./problems/034_insert_delete_getrandom_o1.md) | [Proof](./screenshots/) | ⚪ |
| 035 | First Missing Positive | Hard | In-Place Index Mapping | [LeetCode #41](https://leetcode.com/problems/first-missing-positive/) | [View](./problems/035_first_missing_positive.md) | [Proof](./screenshots/) | ⚪ |

---

## 📸 Attaching Your Solution Screenshots

When you solve any problem from the table above:
1. Save your screenshot as:
   `Week-01-Arrays-Strings-Hashing/screenshots/leetcode-<problem-number>-<name>.png`
2. Update the status in this file and in `PROGRESS_TRACKER.md` from `⚪` to `🟢`.
