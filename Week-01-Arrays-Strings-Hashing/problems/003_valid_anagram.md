# 📌 LeetCode #242: Valid Anagram

- **Difficulty**: Easy
- **Topic**: Strings, Hashing
- **Pattern**: Frequency Array / Hash Map
- **LeetCode Link**: [Valid Anagram](https://leetcode.com/problems/valid-anagram/)
- **Verdict**: Accepted (56 / 56 testcases passed ⚡)

---

## 📝 Problem Statement
Given two strings `s` and `t`, return `true` if `t` is an anagram of `s`, and `false` otherwise.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, using all the original letters exactly once.

### Examples
- **Example 1**:
  - **Input**: `s = "anagram"`, `t = "nagaram"`
  - **Output**: `true`
- **Example 2**:
  - **Input**: `s = "rat"`, `t = "car"`
  - **Output**: `false`

---

## 💡 What Is Happening Under The Hood?

Two strings are valid anagrams if and only if:
1. **Length Invariant**: Both strings have the identical length (`s.length() == t.length()`). If not, return `false` in $O(1)$!
2. **Character Multiset Invariant**: Every character must appear with the exact same frequency in both strings.

### Approach 1: Sorting Canonical Forms (Your C++ Solution)
By sorting both strings alphabetically, we transform any permutation into its canonical sorted representation:
$$\text{sort}("anagram") \implies "aaagmnr"$$
$$\text{sort}("nagaram") \implies "aaagmnr"$$
Comparing the two sorted strings directly verifies if their multisets match.
- **Time Complexity**: $O(N \log N)$ where $N$ is string length.
- **Space Complexity**: $O(1)$ if sorted in-place (or $O(N)$ when passed by value as copies).

### Approach 2: Fixed 26-Element Frequency Array (Optimal $O(N)$)
Since the problem statement specifies English lowercase letters (`'a'` to `'z'`), we don't need a heavy hash map with dynamic bucket allocations. A simple array `int count[26] = {0}` tracks relative frequency:
- For each character in `s`: Increment `count[s[i] - 'a']++`
- For each character in `t`: Decrement `count[t[i] - 'a']--`
- If the strings are anagrams, every single cell in `count` must balance back to `0`.

---

## 💻 Solutions

### Approach 1: C++ (Your Accepted Sorting Solution - 7 ms)
```cpp
#include <string>
#include <algorithm>

class Solution {
public:
    bool isAnagram(std::string s, std::string t) {
        // Fast fail on length mismatch
        if (s.length() != t.length()) return false;
        
        // Sort both strings to canonical form
        std::sort(s.begin(), s.end());
        std::sort(t.begin(), t.end());
        
        // Equal sorted strings imply identical character multiset
        return s == t;
    }
};
```

### Approach 2: C++ (Optimal 26-Bucket Counting - 0 ms)
```cpp
#include <string>

class Solution {
public:
    bool isAnagram(std::string s, std::string t) {
        if (s.length() != t.length()) return false;
        
        int count[26] = {0};
        
        // Single pass: tally s and cancel with t
        for (int i = 0; i < s.length(); ++i) {
            count[s[i] - 'a']++;
            count[t[i] - 'a']--;
        }
        
        // All net frequencies must be exactly zero
        for (int i = 0; i < 26; ++i) {
            if (count[i] != 0) return false;
        }
        
        return true;
    }
};
```

### Python 3
```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False
            
        count = [0] * 26
        for ch1, ch2 in zip(s, t):
            count[ord(ch1) - ord('a')] += 1
            count[ord(ch2) - ord('a')] -= 1
            
        return all(c == 0 for c in count)
```

### Java
```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) return false;
        
        int[] count = new int[26];
        for (int i = 0; i < s.length(); i++) {
            count[s.charAt(i) - 'a']++;
            count[t.charAt(i) - 'a']--;
        }
        
        for (int c : count) {
            if (c != 0) return false;
        }
        return true;
    }
}
```

---

## 🔍 Dry-Run Table (Approach 2 Counting)

Input: `s = "anagram"`, `t = "nagaram"`

| Step ($i$) | `s[i]` | `t[i]` | Net Effect on Frequency Array |
| :-: | :-: | :-: | :--- |
| `0` | `'a'` | `'n'` | `count['a']++` (+1), `count['n']--` (-1) |
| `1` | `'n'` | `'a'` | `count['n']++` (0), `count['a']--` (0) |
| `2` | `'a'` | `'g'` | `count['a']++` (+1), `count['g']--` (-1) |
| `3` | `'g'` | `'a'` | `count['g']++` (0), `count['a']--` (0) |
| `4` | `'a'` | `'r'` | `count['a']++` (+1), `count['r']--` (-1) |
| `5` | `'r'` | `'a'` | `count['r']++` (0), `count['a']--` (0) |
| `6` | `'m'` | `'m'` | `count['m']++` (+1), `count['m']--` (0) |
| **End** | — | — | **All 26 elements are `0` $\implies$ Valid Anagram!** |

---

## ⏱️ Complexity Comparison

| Solution | Time Complexity | Auxiliary Space | When to Use |
| :--- | :---: | :---: | :--- |
| **Approach 1: Sorting** | $\mathcal{O}(N \log N)$ | $\mathcal{O}(1)$ or $\mathcal{O}(N)$ | Minimal code, easily adapts to Unicode or wide strings. |
| **Approach 2: Frequency Array** | $\mathcal{O}(N)$ | $\mathcal{O}(1)$ | Optimal performance on fixed alphabets (lowercase a-z). |

---

## 🧠 Key Learnings & Mental Models to Remember

1. **Length Check as an Early Guard**:
   - Always check `s.length() != t.length()` first. It is an instant $\mathcal{O}(1)$ rejection for non-anagrams.
2. **The "Tally and Cancel" Invariant**:
   - Instead of maintaining two separate maps or arrays, iterate through both strings in tandem: increment for `s` and decrement for `t`. If they cancel out completely to zero, they are anagrams.
3. **Follow-Up / What If the Inputs Contain Unicode?**:
   - If inputs contain Unicode characters (special symbols, Cyrillic, Chinese, emojis), a fixed 26-size array fails.
   - **Solution**: Use `std::unordered_map<wchar_t, int>` or UTF-32 code point counting. Alternatively, the **Sorting approach** handles arbitrary character encodings natively!
4. **Where This Pattern Reappears**:
   - **Group Anagrams (LeetCode #49)**: Use either sorted strings or frequency tuples as keys in a hash map.
   - **Find All Anagrams in a String (LeetCode #438)**: Maintain a sliding window of size `len(p)` with frequency counting.
   - **Permutation in String (LeetCode #567)**: Identical fixed-size sliding window anagram check.

---

## 📸 Submission Proof

![LeetCode #242 Valid Anagram Accepted Proof](../screenshots/leetcode-0242-valid-anagram.png)
