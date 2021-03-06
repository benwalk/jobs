## Merge Two Sorted Lists
When you have two lists already sorted but want only one.

In Scala,

```
/*
 * Returns the head of a single list generated by merging
 * the two provided lists.
 *
 * Assumptions:
 * - lists are between 0 and 50 nodes, already sorted
 * - node values range -100 to 100
 * 
 */
def mergeTwoLists(l1: ListNode, l2: ListNode): ListNode = {
    l1 match {
        // both are null, :picard_why:
        case null if l2 == null =>
            null

        // no more l1, l2 takes it from here
        case null => 
            l2

        // no more l2, l1 takes it from here
        case _ if l2 == null => 
            l1

        // take l1 head and recurse
        case _ if l1.x <= l2.x =>
            l1.next = mergeTwoLists(l1.next, l2)
            l1

        // take l2 head and recurse
        case _ if l1.x > l2.x =>
            l2.next = mergeTwoLists(l1, l2.next)
            l2

        // obligatory "this should never happen"
        case _ => throw new IllegalArgumentException()

    }
}
```

This has a number of drawbacks, as matching might be more expensive than strict comparisons. Recursion could be considered another drawback,
and a solution without recursion would be done by iterating over both lists generating a new list as you go or "stitching" the two
together via `next` field updates.

In a real world scenario, another solution for this problem is to make `ListNode` extend `Ordered` and use built-ins. Whether or not this
improves the solution likely depends on the complexity of the actual class. Additionally, you're more likely to encounter immutable fields
and thus modifying the `next` pointer directly may not be an option.
