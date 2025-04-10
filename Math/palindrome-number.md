# Palindrome Number

## Problem Statement
Given an integer `x`, return `true` if `x` is a palindrome, and `false` otherwise.

### A palindrome is a number that reads the same backward as forward.

### Example:
```plaintext
Input: x = 121
Output: true

Input: x = -121
Output: false // because -121 != 121-

Input: x = 10
Output: false // because 10 != 01
```

---

## Solutions

### Python
```python
def isPalindrome(x: int) -> bool:
    return str(x) == str(x)[::-1]
```

### C
```c
#include <stdbool.h>
#include <string.h>

bool isPalindrome(int x){
    if (x < 0) return false;
    char str[20];
    sprintf(str, "%d", x);
    int len = strlen(str);
    for (int i = 0; i < len / 2; i++) {
        if (str[i] != str[len - i - 1]) return false;
    }
    return true;
}
```

### C++
```cpp
#include <string>
using namespace std;

bool isPalindrome(int x) {
    if (x < 0) return false;
    string s = to_string(x);
    int l = 0, r = s.size() - 1;
    while (l < r) {
        if (s[l++] != s[r--]) return false;
    }
    return true;
}
```

### JavaScript
```javascript
var isPalindrome = function(x) {
    if (x < 0) return false;
    let str = x.toString();
    let reversed = str.split('').reverse().join('');
    return str === reversed;
};
```

---

## Optimized Solution (No string conversion)

### Python (No string version)
```python
def isPalindrome(x: int) -> bool:
    if x < 0 or (x % 10 == 0 and x != 0):
        return False
    reverted = 0
    while x > reverted:
        reverted = reverted * 10 + x % 10
        x //= 10
    return x == reverted or x == reverted // 10
```

---

## Complexity Analysis
- **Time Complexity:** `O(log₁₀ n)` because we process half of the digits
- **Space Complexity:** `O(1)` for the optimized solution (no extra space used)