# Longest Palindromic Substring

## Problem Statement
Given a string `s`, return the **longest palindromic substring** in `s`.

### Example:
```plaintext
Input: s = "babad"
Output: "bab"
Explanation: "aba" is also a valid answer.
```

```plaintext
Input: s = "cbbd"
Output: "bb"
```

---

## Solutions

### Python Solution (Expand Around Center)
```python
def longest_palindrome(s):
    def expand_around_center(left, right):
        while left >= 0 and right < len(s) and s[left] == s[right]:
            left -= 1
            right += 1
        return s[left+1:right]
    
    longest = ""
    for i in range(len(s)):
        odd = expand_around_center(i, i)
        even = expand_around_center(i, i+1)
        longest = max(longest, odd, even, key=len)
    return longest
```

### C++ Solution (Expand Around Center)
```cpp
#include <iostream>
using namespace std;

string expandAroundCenter(string s, int left, int right) {
    while (left >= 0 && right < s.length() && s[left] == s[right]) {
        left--;
        right++;
    }
    return s.substr(left + 1, right - left - 1);
}

string longestPalindrome(string s) {
    string longest = "";
    for (int i = 0; i < s.length(); i++) {
        string odd = expandAroundCenter(s, i, i);
        string even = expandAroundCenter(s, i, i + 1);
        longest = odd.length() > longest.length() ? odd : longest;
        longest = even.length() > longest.length() ? even : longest;
    }
    return longest;
}
```

### JavaScript Solution (Expand Around Center)
```javascript
var longestPalindrome = function(s) {
    function expandAroundCenter(left, right) {
        while (left >= 0 && right < s.length && s[left] === s[right]) {
            left--;
            right++;
        }
        return s.substring(left + 1, right);
    }
    
    let longest = "";
    for (let i = 0; i < s.length; i++) {
        let odd = expandAroundCenter(i, i);
        let even = expandAroundCenter(i, i + 1);
        longest = odd.length > longest.length ? odd : longest;
        longest = even.length > longest.length ? even : longest;
    }
    return longest;
};
```

---

## Complexity Analysis
- **Expand Around Center:** `O(n^2)` time, `O(1)` space.