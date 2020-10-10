# Add Two Numbers

You are given two `non-empty` linked lists representing two non-negative integers. The digits are stored in `reverse order`, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

### Example 1:

![alt text](addtwonumber1.jpg)

```
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
```

### Example 2:

```
Input: l1 = [0], l2 = [0]
Output: [0]
```

### Example 3:

```
Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]
```

### Constraints:

- The number of nodes in each linked list is in the range [1, 100].
- 0 <= Node.val <= 9
- It is guaranteed that the list represents a number that does not have leading zeros.

---

### Solution:

```
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var addTwoNumbers = function(l1, l2) {
    let currL1 = l1, currL2 = l2;
    let L = new ListNode(0);
    let headL = L, carry = 0;
    while (currL1 != null || currL2 != null) {
        let valL1 = (currL1 !== null) ? currL1.val : 0;
        let valL2 = (currL2 !== null) ? currL2.val : 0;
        let sum = valL1 + valL2 + L.val;
        let valL = sum % 10;
        L.val = valL;
        carry = Math.floor(sum / 10);
        currL1 = currL1 !== null ? currL1.next: null;
        currL2 = currL2 !== null ? currL2.next: null;
        if(currL1 != null || currL2 != null || carry != 0) L.next = new ListNode(carry);
        L = L.next;
    }
    return headL;
};
```
