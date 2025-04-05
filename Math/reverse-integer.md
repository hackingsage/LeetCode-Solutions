# Reverse Integer

## Problem Statement
Given a signed 32-bit integer `x`, return `x` with its digits reversed. If reversing `x` causes the value to go outside the signed 32-bit integer range `[-2^31, 2^31 - 1]`, return `0`.

### Example:
```plaintext
Input: x = 123
Output: 321

Input: x = -123
Output: -321

Input: x = 120
Output: 21

Input: x = 0
Output: 0
```

---

## Solutions

### Python Solution
```python
def reverse(x: int) -> int:
    sign = -1 if x < 0 else 1
    x_abs = abs(x)
    reversed_x = int(str(x_abs)[::-1])
    result = sign * reversed_x
    if -2**31 <= result <= 2**31 - 1:
        return result
    return 0
```

### C Solution
```c
#include <limits.h>

int reverse(int x) {
    long reversed = 0;
    while (x != 0) {
        reversed = reversed * 10 + x % 10;
        x /= 10;
    }
    if (reversed < INT_MIN || reversed > INT_MAX) return 0;
    return (int)reversed;
}
```

### C++ Solution
```cpp
#include <climits>

int reverse(int x) {
    long result = 0;
    while (x) {
        result = result * 10 + x % 10;
        x /= 10;
    }
    return (result < INT_MIN || result > INT_MAX) ? 0 : result;
}
```

### JavaScript Solution
```javascript
var reverse = function(x) {
    const sign = x < 0 ? -1 : 1;
    const reversed = parseInt(Math.abs(x).toString().split('').reverse().join(''));
    const result = sign * reversed;
    return (result < -(2**31) || result > 2**31 - 1) ? 0 : result;
};
```

---

## Complexity Analysis
- **Time Complexity:** `O(log₁₀(n))` — we process each digit once
- **Space Complexity:** `O(1)` — constant extra space