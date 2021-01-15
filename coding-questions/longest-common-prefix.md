## Longest Common Prefix

In Scala,
```
/*
 * Given an array of strings, returns the longest common prefix of all strings.
 *
 * If there is no prefix, the empty string is returned.
 */
def longestCommonPrefix(strs: Array[String]): String = {
    recurse(strings = strs)
}

/*
 * Recursively checks letters of each string to build a common prefix
 */
private def recurse(prefix: String = "", strings: Array[String]): String = {
    // base case, edge case: no strings to check
    if (strings.isEmpty) {
        return prefix
    }


    // base case: no more letters in one or more strings
    strings.foreach { s => 
        if (s.isEmpty) {
            return prefix
        }
    }

    // grabs first letter of each string
    val letters: Array[Char] = strings.map(_.head)

    // compare each letter for matching
    val first = letters.head
    val allMatch: Boolean = letters.forall(_.equals(first))

    if (allMatch) {
        recurse(prefix.appended(first), strings.map(_.tail))
    }
    else {
        return prefix
    }
}
```
