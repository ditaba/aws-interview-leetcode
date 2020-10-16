# Copy List with Random Pointer

A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a **deep copy** of the list.

The Linked List is represented in the input/output as a list of `n` nodes. Each node is represented as a pair of `[val, random_index]` where:

- `val`: an integer representing `Node.val`
- `random_index`: the index of the node (range from `0` to `n-1`) where random pointer points to, or `null` if it does not point to any node.

### Example 1:

![alt text](copylistwithrandompointer_e1.png)

```
Input: head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
Output: [[7,null],[13,0],[11,4],[10,2],[1,0]]
```

### Example 2:

![alt text](copylistwithrandompointer_e2.png)

```
Input: head = [[1,1],[2,1]]
Output: [[1,1],[2,1]]
```

### Example 3:

![alt text](copylistwithrandompointer_e3.png)

```
Input: head = [[3,null],[3,0],[3,null]]
Output: [[3,null],[3,0],[3,null]]
```

### Example 4:

```
Input: head = []
Output: []
Explanation: Given linked list is empty (null pointer), so return null.
```

### Constraints:

- `-10000 <= Node.val <= 10000`
- `Node.random` is null or pointing to a node in the linked list.
- The number of nodes will not exceed 1000.

---

### Solution:

```
/**
 * // Definition for a Node.
 * function Node(val, next, random) {
 *    this.val = val;
 *    this.next = next;
 *    this.random = random;
 * };
 */

/**
 * @param {Node} head
 * @return {Node}
 */
var copyRandomList = function(head) {
    if(head==null) return null;
    let curr = head, temp = null;

    // Insert additional node after every node of original list
    while(curr != null){
        temp = curr.next;
        curr.next = new Node(curr.val, curr.next);
        curr = temp;
    }
    curr = head;

    // Adjust the random pointers of the newly added nodes
    while(curr != null){
        if(curr.next != null){
            curr.next.random = (curr.random != null) ? curr.random.next : curr.random;
        }

        // Move to the next newly added node by skipping an original node
        curr = (curr.next != null) ? curr.next.next : curr.next;
    }
    let original = head, copy = head.next;

    // Save the start of copied linked list
    temp = copy;

    // Now separate the original list and copied list
    while(original != null){
        original.next = (original.next != null) ? original.next.next : original.next;
        copy.next = (copy.next != null) ? copy.next.next : copy.next;
        original = original.next;
        copy = copy.next;
    }
    return temp;
};
```
