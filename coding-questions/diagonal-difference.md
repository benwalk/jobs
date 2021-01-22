# Diagonal Difference

Not entirely sure when this might come up in practice, but if you had a matrix of integers and needed to find the difference between the sum of the top left to bottom right diagonal and the bottom left to top right diagonal, here's how you might do it.


Scala,
```
def diagonalDifference(arr: Array[Array[Int]]): Int = {
    val lastIndex = arr.length - 1
    var topDown, bottomUp = 0
    (0 to lastIndex).map( n => {
        topDown += arr(n)(n)
        bottomUp += arr(lastIndex - n)(n)
    })

    (topDown - bottomUp).abs
}
```

Analysis: Linear time. You only need to iterate through "columnns" in the matrix, building the two sums as you go. A more naive approach might iterate twice - once for each sum.
