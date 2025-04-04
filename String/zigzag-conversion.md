# ZigZag Conversion

## Problem Statement
Given a string `s` and an integer `numRows`, arrange the characters in a zigzag pattern across the given number of rows and return the string read row-wise.

### Example:
```plaintext
Input: s = "PAYPALISHIRING", numRows = 3
Output: "PAHNAPLSIIGYIR"
Explanation:
P   A   H   N
A P L S I I G
Y   I   R
```

```plaintext
Input: s = "PAYPALISHIRING", numRows = 4
Output: "PINALSIGYAHRPI"
Explanation:
P     I    N
A   L S  I G
Y A   H R
P     I
```

---

## Solutions

### Python Solution (Using Row Indexing)
```python
def convert(s: str, numRows: int) -> str:
    if numRows == 1 or numRows >= len(s):
        return s
    
    rows = ["" for _ in range(numRows)]
    index, step = 0, 1
    
    for char in s:
        rows[index] += char
        if index == 0:
            step = 1
        elif index == numRows - 1:
            step = -1
        index += step
    
    return "".join(rows)
```

### C++ Solution
```cpp
#include <iostream>
#include <vector>
using namespace std;

string convert(string s, int numRows) {
    if (numRows == 1 || numRows >= s.length()) return s;
    
    vector<string> rows(min(numRows, int(s.length())));
    int index = 0, step = 1;
    
    for (char c : s) {
        rows[index] += c;
        if (index == 0) step = 1;
        else if (index == numRows - 1) step = -1;
        index += step;
    }
    
    string result;
    for (string row : rows) result += row;
    return result;
}
```

### JavaScript Solution
```javascript
var convert = function(s, numRows) {
    if (numRows === 1 || numRows >= s.length) return s;
    
    let rows = Array.from({ length: numRows }, () => "");
    let index = 0, step = 1;
    
    for (let char of s) {
        rows[index] += char;
        if (index === 0) step = 1;
        else if (index === numRows - 1) step = -1;
        index += step;
    }
    
    return rows.join("");
};
```

---

## Complexity Analysis
- **Time Complexity:** `O(n)`, where `n` is the length of the string.
- **Space Complexity:** `O(n)`, as we store the result in an array.