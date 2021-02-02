# Add Two Number (Lists)

For example, 
```
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
```

and
```
Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]
```

We have the following constraints:
```
- The number of nodes in each linked list is in the range [1, 100].
- 0 <= Node.val <= 9
- It is guaranteed that the list represents a number that does not have leading zeros.
```

In Scala,
```
/**
 * Definition for singly-linked list.
 * class ListNode(_x: Int = 0, _next: ListNode = null) {
 *   var next: ListNode = _next
 *   var x: Int = _x
 * }
 */
object Solution {
    /**
     * Given two singly-linked lists of integer nodes representing
     * reversed digits of a positive decimal number, adds the two
     * numbers together returning a new list for the sum.
     */
    def addTwoNumbers(l1: ListNode, l2: ListNode): ListNode = {
        // track original head
        var head = ListNode()
        
        // tracking as we go
        var tail = head
        var l1Curr = l1
        var l2Curr = l2
        var carry = 0
        
        // traverse if either list continues or we still have carry over
        while (l1Curr != null || l2Curr != null || carry > 0) {
            
            // bump tail pointer to make a place for this digit
            if (tail.next == null) { 
                tail.next = ListNode()
                tail = tail.next
            } 
            
            // calc sum
            val l1x = if (l1Curr == null) 0 else l1Curr.x
            val l2x = if (l2Curr == null) 0 else l2Curr.x
            
            l1x + l2x + carry match {
                // need to carry
                case sum if sum > 9 =>
                    tail.x = sum % 10
                    carry = sum / 10
                
                // don't need to carry, might have carried to here though
                case sum =>
                    tail.x = sum
                    if (carry > 0) carry = sum / 10
            }
            
            l1Curr = if (l1Curr == null) null else l1Curr.next
            l2Curr = if (l2Curr == null) null else l2Curr.next
            
        }
        // we may have carried off the end
        if (l1Curr == null && l2Curr == null && carry > 0) {
            tail.x = carry
        }
        head.next
    }
}
```

Analysis: `O(max(m,n))` - linear time of whichever list is larger. Space complexity is the `O(max(m,n) + 1)` at most.
