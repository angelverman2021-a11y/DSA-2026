# 📌 LeetCode #242: Valid Anagram

- **Difficulty**: Easy
- **Topic**: Strings, Hashing
- **Pattern**: Frequency Array / Hash Map
- **LeetCode Link**: [Valid Anagram](https://leetcode.com/problems/valid-anagram/)

---

## 📝 Problem Statement
Given two strings `s` and `t`, return `true` if `t` is an anagram of `s`, and `false` otherwise.
*(An Anagram is a word formed by rearranging the letters of a different word, using all the original letters exactly once.)*

---

## 💡 Intuition & Core Pattern
Two strings are anagrams if and only if:
1. They have the same length: `len(s) == len(t)`.
2. Every character appears with the exact same count in both strings.

### Optimization: Fixed 26-element Frequency Array
Because inputs consist of lowercase English letters (`'a'` to `'z'`), an integer array of size 26 avoids heap allocations of HashMaps:
- For each char in `s`: `count[char - 'a']++`
- For each char in `t`: `count[char - 'a']--`
- If all 26 entries remain `0`, they are anagrams!

---

## 💻 Solutions

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

### C++
```cpp
#include <string>
#include <vector>

class Solution {
public:
    bool isAnagram(std::string s, std::string t) {
        if (s.length() != t.length()) return false;
        
        int count[26] = {0};
        for (int i = 0; i < s.length(); ++i) {
            count[s[i] - 'a']++;
            count[t[i] - 'a']--;
        }
        
        for (int i = 0; i < 26; ++i) {
            if (count[i] != 0) return false;
        }
        return true;
    }
};
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

## ⏱️ Complexity Analysis
- **Time Complexity**: $O(N)$ — Where $N = \text{len}(s)$. Linear traversal through both strings.
- **Space Complexity**: $O(1)$ — Array of constant size 26 (alphabet size), independent of $N$.

---

## 📸 Submission Proof
Add your accepted screenshot here:
`../screenshots/leetcode-0242-valid-anagram.png`
