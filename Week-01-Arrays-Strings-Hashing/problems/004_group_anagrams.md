# 📌 LeetCode #49: Group Anagrams

- **Difficulty**: Medium
- **Topic**: Arrays, Strings, Hashing
- **Pattern**: Categorization via Canonical Hash Key
- **LeetCode Link**: [Group Anagrams](https://leetcode.com/problems/group-anagrams/)
- **Verdict**: Accepted (15 ms ⚡, Beats 73.99% Runtime, Beats 93.73% Memory 🔥)

---

## 📝 Problem Statement
Given an array of strings `strs`, group the **anagrams** together. You can return the answer in any order.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, using all the original letters exactly once.

### Examples
- **Example 1**:
  - **Input**: `strs = ["eat","tea","tan","ate","nat","bat"]`
  - **Output**: `[["bat"],["nat","tan"],["ate","eat","tea"]]`
- **Example 2**:
  - **Input**: `strs = [""]`
  - **Output**: `[[""]]`
- **Example 3**:
  - **Input**: `strs = ["a"]`
  - **Output**: `[["a"]]`

---

## 💡 What Is Happening Under The Hood?

### 1. Equivalence Partitioning via Canonical Keys
Two strings belong to the same anagram group if and only if they share the exact same multiset of characters. To group them without comparing every pair ($O(N^2)$), we map each string to a **canonical key**:

$$\text{sort}(\text{"eat"}) = \text{"aet"}$$
$$\text{sort}(\text{"tea"}) = \text{"aet"}$$
$$\text{sort}(\text{"ate"}) = \text{"aet"}$$

By using this sorted string as a hash map key:
```
Key: "aet" ──► Value: ["eat", "tea", "ate"]
Key: "ant" ──► Value: ["tan", "nat"]
Key: "abt" ──► Value: ["bat"]
```

### 2. Why Your Solution Beat 93.73% Memory: `std::move`
Notice this critical line in your C++ code:
```cpp
for (auto& pair : anagramMap) {
    result.push_back(move(pair.second));
}
```
In standard C++, `result.push_back(pair.second)` performs a **deep copy** of every vector of strings (allocating new memory and copying character buffers).  
By utilizing **`std::move(pair.second)`**, you transferred ownership of the internal vector pointer in $\mathcal{O}(1)$ without reallocating any heap memory. That micro-optimization is why your memory usage was in the top tier!

---

## 💻 Solutions

### C++ (Your Optimal Accepted Solution - 15 ms)
```cpp
#include <vector>
#include <string>
#include <unordered_map>
#include <algorithm>

using namespace std;

class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        unordered_map<string, vector<string>> anagramMap;
        
        // Group each word by its sorted canonical key
        for (const string& s : strs) {
            string key = s;
            sort(key.begin(), key.end());
            anagramMap[key].push_back(s);
        }
        
        // Move grouped vectors into result without deep copies
        vector<vector<string>> result;
        for (auto& pair : anagramMap) {
            result.push_back(move(pair.second));
        }
        return result;
    }
};
```

### Python 3
```python
from collections import defaultdict

class Solution:
    def groupAnagrams(self, strs: list[str]) -> list[list[str]]:
        groups = defaultdict(list)
        for s in strs:
            key = "".join(sorted(s))
            groups[key].append(s)
        return list(groups.values())
```

### Java
```java
import java.util.*;

class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        Map<String, List<String>> map = new HashMap<>();
        for (String s : strs) {
            char[] chars = s.toCharArray();
            Arrays.sort(chars);
            String key = new String(chars);
            map.computeIfAbsent(key, k -> new ArrayList<>()).add(s);
        }
        return new ArrayList<>(map.values());
    }
}
```

---

## 🔍 Dry-Run Table

Input: `strs = ["eat", "tea", "tan", "ate", "nat", "bat"]`

| Index | Word `s` | Sorted Key `key` | Map State After Operation |
| :-: | :--- | :--- | :--- |
| `0` | `"eat"` | `"aet"` | `{"aet": ["eat"]}` |
| `1` | `"tea"` | `"aet"` | `{"aet": ["eat", "tea"]}` |
| `2` | `"tan"` | `"ant"` | `{"aet": ["eat", "tea"], "ant": ["tan"]}` |
| `3` | `"ate"` | `"aet"` | `{"aet": ["eat", "tea", "ate"], "ant": ["tan"]}` |
| `4` | `"nat"` | `"ant"` | `{"aet": ["eat", "tea", "ate"], "ant": ["tan", "nat"]}` |
| `5` | `"bat"` | `"abt"` | `{"aet": [...], "ant": [...], "abt": ["bat"]}` |

**Final Result**: `[["eat", "tea", "ate"], ["tan", "nat"], ["bat"]]`

---

## ⏱️ Complexity Analysis

- **Time Complexity**: $\mathcal{O}(N \cdot K \log K)$
  - $N$ = total number of strings in `strs`.
  - $K$ = maximum length of a string in `strs`.
  - For each string, sorting takes $\mathcal{O}(K \log K)$. Inserting into the hash map takes $\mathcal{O}(K)$ average time.
- **Space Complexity**: $\mathcal{O}(N \cdot K)$
  - Total storage needed to store all $N$ strings inside `anagramMap` and the final `result`.

---

## 🧠 Key Learnings & Mental Models to Remember

1. **Equivalence Class Partitioning**:
   - Whenever a problem asks to *"group items that satisfy a relation"*, seek a **canonical signature** that uniquely identifies the group.
   - For anagrams: sorted string or character frequency tuple `(count_a, count_b, ..., count_z)`.
2. **Move Semantics in C++**:
   - When transferring collections out of intermediate containers (like `unordered_map`), always prefer `std::move()` over copying to prevent heap allocations.
3. **Where This Pattern Reappears**:
   - **Group Shifted Strings (LeetCode #249)**: Compute difference between adjacent characters as key.
   - **Find Duplicate Subtrees (LeetCode #652)**: Serialize subtrees into string signatures and group by hash.

---

## 📸 Submission Proof

![LeetCode #49 Group Anagrams Accepted Proof](../screenshots/leetcode-0049-group-anagrams.png)
