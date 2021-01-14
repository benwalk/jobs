## Balancing Brackets

The problem of how to determine if opened brackets have been closed when given a string of brackets. I would 
imagine this to be a common function for syntax validators and IDEs.

```
/*
 * Given a string containing just the characters '(', ')', '{', '}', '[' and ']', returns
 * whether the input string is valid.
 *
 * An input string is valid if:
 * - open brackets must be closed by the same type of brackets
 * - open brackets must be closed in the correct order
 */
def isValid(s: String): Boolean = {

    val stack = new scala.collection.mutable.Stack[Char]()

    for {
        c <- s
    } yield {
        c match {
            // on open brackets, push
            case '(' | '{' | '[' => 
                stack.push(c)

           // have to open a bracket before closing
           case _ if stack.size < 1 => return false

             // on closing brackets, pop & match
            case ')' if stack.pop() == '(' => 

            case '}' if stack.pop() == '{' => 

            case ']' if stack.pop() == '[' => 

            case _ => return false
       }              
    }

    // an empty stack means everything opened was successfully closed
    stack.isEmpty
}

```
