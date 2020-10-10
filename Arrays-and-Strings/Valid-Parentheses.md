# Valid Parentheses

Given a string s containing just the characters `(`, `)`, `{`, `}`, `[` and `]`, determine if the input string is valid.

An input string is valid if:

- Open brackets must be closed by the same type of brackets.
- Open brackets must be closed in the correct order.

### Example 1:

```
Input: s = "()"
Output: true
```

### Example 2:

```
Input: s = "()[]{}"
Output: true
```

### Example 3:

```
Input: s = "(]"
Output: false
```

### Example 4:

```
Input: s = "([)]"
Output: false
```

### Example 5:

```
Input: s = "{[]}"
Output: true
```

### Constraints:

- `1 <= s.length <= 104`
- s consists of parentheses only `()[]{}`.

---

### Solution:

```
/**
 * @param {string} s
 * @return {boolean}
 */
var isValid = function(s) {
    const mappingParentheses = new Map();
    mappingParentheses.set('}','{');
    mappingParentheses.set(')','(');
    mappingParentheses.set(']','[');

    const stack = [];
    stack.push(s[0]);
    for(let i=1; i<s.length; i++){
        if (mappingParentheses.has(s[i])) {
            let c = (stack.length > 0) ? stack.pop() : '#';
            if (c != mappingParentheses.get(s[i])) {
                return false;
            }
        } else {
            stack.push(s[i]);
        }
    }
    return stack.length > 0 ? false : true;
};
```
