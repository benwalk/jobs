## Longest Common Prefix
For when you have a bunch of strings and want to find how much they all overlap at the start. For example, `["dog","doge","doug","dug"]` has an LCP of only "d".

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

There are also non-recursive ways to solve this, and I'm sure this could be improved to not need the second function. This was just a limitation of the platform I was writing this on. In some languages, where immutability is less of a concern, higher-level vars could be mutated to store the prefix as it's identified.
