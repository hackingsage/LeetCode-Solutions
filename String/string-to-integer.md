# String to Integer (atoi)

## Problem Statement
Implement the `myAtoi(string s)` function, which converts a string to a 32-bit signed integer (similar to C/C++'s `atoi` function).

### The algorithm follows these rules:
1. Read and ignore any leading whitespace.
2. Check for an optional '+' or '-' sign.
3. Read in the next characters until the next non-digit character or the end of the input is reached.
4. Convert these digits into an integer.
5. Clamp the integer so that it falls within the 32-bit signed integer range: [-2^31, 2^31 - 1].
6. If no valid conversion could be performed, return 0.

### Example:
```plaintext
Input: s = "42"
Output: 42

Input: s = "   -42"
Output: -42

Input: s = "4193 with words"
Output: 4193

Input: s = "words and 987"
Output: 0

Input: s = "-91283472332"
Output: -2147483648
```

---

## Solutions

### Python
```python
def myAtoi(s: str) -> int:
    s = s.lstrip()  # 1. Remove leading whitespace
    if not s:
        return 0

    sign = 1
    index = 0
    if s[0] in ['-', '+']:
        if s[0] == '-':
            sign = -1
        index += 1

    num = 0
    while index < len(s) and s[index].isdigit():
        num = num * 10 + int(s[index])
        index += 1

    num *= sign
    INT_MIN, INT_MAX = -2**31, 2**31 - 1
    return max(INT_MIN, min(num, INT_MAX))
```

### C
```c
#include <limits.h>
#include <ctype.h>

int myAtoi(char * s) {
    while (*s == ' ') s++;
    int sign = 1;
    if (*s == '-' || *s == '+') {
        if (*s == '-') sign = -1;
        s++;
    }
    long result = 0;
    while (isdigit(*s)) {
        result = result * 10 + (*s - '0');
        if (sign * result <= INT_MIN) return INT_MIN;
        if (sign * result >= INT_MAX) return INT_MAX;
        s++;
    }
    return sign * result;
}
```

### C++
```cpp
#include <climits>

int myAtoi(string s) {
    int i = 0, sign = 1;
    long result = 0;
    while (s[i] == ' ') i++;

    if (s[i] == '+' || s[i] == '-') {
        if (s[i] == '-') sign = -1;
        i++;
    }

    while (isdigit(s[i])) {
        result = result * 10 + (s[i] - '0');
        if (sign * result <= INT_MIN) return INT_MIN;
        if (sign * result >= INT_MAX) return INT_MAX;
        i++;
    }
    return sign * result;
}
```

### JavaScript
```javascript
var myAtoi = function(s) {
    s = s.trim();
    let sign = 1, i = 0, result = 0;
    if (s[i] === '+' || s[i] === '-') {
        if (s[i] === '-') sign = -1;
        i++;
    }
    while (i < s.length && s[i] >= '0' && s[i] <= '9') {
        result = result * 10 + (s[i].charCodeAt(0) - '0'.charCodeAt(0));
        if (sign * result < -(2 ** 31)) return -(2 ** 31);
        if (sign * result > (2 ** 31) - 1) return (2 ** 31) - 1;
        i++;
    }
    return sign * result;
};
```

---

## Complexity Analysis
- **Time Complexity:** `O(n)`, where `n` is the length of the input string.
- **Space Complexity:** `O(1)` — no extra space other than a few variables.