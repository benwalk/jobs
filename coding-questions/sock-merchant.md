# Sock Merchant
Sock merchant has a large number of socks of at most that many colors. The merchant needs to identify how many pairs of each color exist.

In Java,
```
/**
 * Returns the number of pairs that can be made, given
 * a total number of socks and a list of the colors of
 * all the socks.
 *
 * Assumptions: 
 * - numSocks is in the range 1 .. 100
 * - colors includes 1 .. 100 colors
 *
 * Analysis:
 * - runs in O(m+n) time, one iteration over colors, one over counts
 */
static int sockMerchant(int numSocks, int[] colors) {

    // map for storing <Color,Count> pairs
    HashMap<Integer,Integer> map = new HashMap<Integer,Integer>();

    // iterator over colors to build map
    for(int color : colors) {
        int count = 0;
        try {
            count = map.get(color);
        }
        catch (NullPointerException e) {
            // do nothing
            // doesn't exist, so this is the first one
        }

        map.put(color, count+1);
    }

    int total = 0;
    for(int count : map.values()) {
        total += count / 2;
    }

    return total;
}
```

Some improvements to this solution:
- the number of socks could be gleaned from the size of colors array
- there is no debug logging for troubleshooting
- there are no input validation checks (trusts assumptions)
- an actual merchant might want to persist this data
- there are no performance metrics gathered and output
- in an actual web store, if this was being read significantly more often than sales, a cache could be considered
- there are no analytics events emitted

An alternate (better) solution would be to use a `HashSet` and count pairs while iterating over colors.

Here it is in Scala,
```
def sockMerchant(n: Int, ar: Array[Int]): Int = {
    val set = new HashSet[Int]()
    var pairs = 0
    ar.foreach(color => { 
        if (set.contains(color)) {
            pairs += 1
            set.remove(color)
        }
        else {
            set.add(color)
        }
    })
    pairs
}
```    
