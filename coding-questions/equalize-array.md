# Equalize the Array

In Java,
```
/**
 * Returns the minimum number of deletions required to remove all
 * integers from the given array except the most common value.
 * 
 * Assumptions:
 * - both the size of the array and the values are bounded by 1..100
 */
static int equalizeArray(int[] arr) {
    // store (value, count) for each item in the array
    HashMap<Integer,Integer> counts = new HashMap<Integer,Integer>();

    // reference to the highest count
    int leadingCount = 0;

    for(int i = 0; i < arr.length; i++) {
        // have we seen this value before?
        if (counts.get(arr[i]) == null) {
            // nope, add it to the map
            counts.put(arr[i], 1);
        }
        else {
            // yep, how many times?
            int count = counts.get(arr[i]);

            // bump leading count, maybe
            if (count > leadingCount) {
                leadingCount++;
            }

            // bump count
            counts.put(arr[i], count + 1);
        }
    }

    return  arr.length - leadingCount - 1;
}
```

Analysis: Linear time. A more expensive approach would not keep track of the highest count, and iterate over the hashmap to find the highest count at the end. More naively, one could track the value with the highest count, and then do a `O(1)` lookup on the map at the end as well, which might be required if the value with the highest count mattered. In this particular problem prompt, it did not.


In Scala, it's very similar:
```
def equalizeArray(arr: Array[Int]): Int = {
    val counts = new scala.collection.mutable.HashMap[Int,Int]()
    var total = 0;
    arr.foreach(number => {
        val count = counts.getOrElse(number, 0)
        if (count > total) total += 1
        counts.put(number, count + 1)
    })
    return arr.length - total - 1;
}
```
