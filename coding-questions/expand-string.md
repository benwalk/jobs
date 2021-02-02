```
// Write a function that expands a string. A number X (the multiplier) that precedes an alphabetical character repeats this single character X times. A character not preceded by a number has a multiplier of 1. Assume that all numbers are single digit and that only valid input will be passed for now.

// Examples of valid input:
// abc -> abc
// 2a2A -> aaAA

// Examples of invalid input:
// a12b - only single digits are allowed
// a2 - digits should always precede a character


// Add a grouping feature so that a multiplier can be applied to a group of characters (grouped by '[' and ']'). Assume that groups cannot be nested and that only valid input will be passed for now.

// Example of valid input:
// a2b2[cd] -> abbcdcd

// Examples of invalid input: 
// a[b[c]] - groups are not allowed inside groups
// a[bc - mismatched bracket



// pseudocode
// scan input seq
// if a char is seen, then append that to an output string because (x 1)
// if a num is seen, then store that number, skip
// when a char is seen, append that X times (num seen above)
// if a open bracket is seen, start storing a temp string to multiply

object Solution extends App {
  
  def expandString(s: String): String = {
    var out = ""
    var inGroup = false
    var temp = ""
    var multiplier = 1
    s.toCharArray.foreach({ c =>
      c match {
        // digit is seen
        case _ if Character.isDigit(c) =>
            multiplier = c.toString.toInt
        
        // open bracket is seen 
        case _ if c == '[' =>
          inGroup = true
               
        // close backet and append to out
        case _ if c == ']' =>
          inGroup = false
          out = out + (temp * multiplier)
          temp = ""
        
        // if char in group
        case _ if inGroup =>
          temp = temp + c.toString
        
        // char is seen 
        case _ =>
          out = out + (c.toString * multiplier)
          multiplier = 1
          inGroup = false
          
        
      }
      
    })
    
    out
  }

  
  
  def testExpandString() = {
    println(expandString("1c"))  // expects 'c'
    println(expandString("1c1b"))  // expects 'cb'
    println(expandString("1c2b"))  // expects 'cbb'
    println(expandString(""))  // expects ''
    println(expandString("2a2A")) // expects 'aaAA'
    
    println(expandString("2a2A[b]")) // expects 'aaAAb'
    println(expandString("2a2A3[b]")) // expects 'aaAAbbb'
    println(expandString("2a2A3[bc]")) // expects 'aaAAbcbcbc'
    println(expandString("2[ab]")) // expects 'abab
    println(expandString("[b]")) // expects 'b'
    println(expandString("[b]3[c]")) // expects 'bccc'
    println(expandString("0[b]")) // expects ''
    println(expandString("0[abc]")) // expects ''
    println(expandString("2[aBc]")) // expects 'aBcaBc
    println(expandString("abc[]")) // expects 'abc'
    println(expandString("2[2b]c")) // expects 'bbbbc'
    
  }  
  
  
  testExpandString()
}
```
