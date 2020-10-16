# Merge Two Sorted Lists

Merge two sorted linked lists and return it as a new **sorted** list. The new list should be made by splicing together the nodes of the first two lists.

### Example 1:

![alt text](mergetwosortedlists_ex1.jpg)

```
Input: l1 = [1,2,4], l2 = [1,3,4]
Output: [1,1,2,3,4,4]
```

### Example 2:

```
Input: l1 = [], l2 = []
Output: []
```

### Example 3:

```
Input: l1 = [], l2 = [0]
Output: [0]
```

### Constraints:

- The number of nodes in both lists is in the range `[0, 50]`.
- `-100 <= Node.val <= 100`
- Both `l1` and `l2` are sorted in **non-decreasing** order.

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
var mergeTwoLists = function(l1, l2) {
    let headL3 = new ListNode(-1);
    let ptrL3 = headL3;
    while (l1 != null && l2 != null) {
        if (l2.val <= l1.val) {
            ptrL3.next = l2;
            ptrL3 = ptrL3.next;
            l2 = l2.next;
        } else {
            ptrL3.next = l1;
            ptrL3 = ptrL3.next;
            l1 = l1.next;
        }
    }
    ptrL3.next = (l1 == null) ? l2 : l1;
    return headL3.next;
};
```
