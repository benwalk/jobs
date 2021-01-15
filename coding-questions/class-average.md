## Class Average

### Problem
You are writing code for grading multiple choice questions. You are given an answer key:

```["A", "B", "C", "D", "A", "B", "C", "D"]```

and the answers that students gave to the test:

```
{
    "Alice":   ["A", "B", "C", "C", "A", "B", "C", "D"],
    "Bob":     ["B", "B", "C", "C", "A", "B", "C", "D"],
    "Charlie": ["C", "C", "C", "C", "C", "C", "C", "C"],
    "Dave":    ["A", "B", "C", "C", "B", "B", "C", "D"],
    "Eve":     ["A", "B", "C", "D", "D", "C", "B", "A"]
}
```

and tasked with finding the average score for the entire class (as a decimal 0 -> 1).


### Solution 
In Scala,
```
// define the key
val key : Array[String] = Array("A", "B", "C", "D", "A", "B", "C", "D")

// define the set of student answers
val studentAnswers : List[(String,Array[String])] = List(
  ("Alice",               Array("A", "B", "C", "C", "A", "B", "C", "D")),
  ("Bob",                 Array("B", "B", "C", "C", "A", "B", "C", "D")),
  ("Charlie",             Array("C", "C", "C", "C", "C", "C", "C", "C")),
  ("Dave",                Array("A", "B", "C", "C", "B", "B", "C", "D")),
  ("Eve",                 Array("A", "B", "C", "D", "D", "C", "B", "A"))
)

//-----------------------------------------------------------------------

/*
 * Return class average as a decimal given an answer key and set of student answers.
 */ 
def getClassAverage(key: Array[String], studentAnswers: List[(String, Array[String])]): BigDecimal = {

 // iterate over student answers and map answers to a score
 val scores = studentAnswers.map(sa => {

   val (student, answers) = sa
   var score: BigDecimal = 0.0

   // compare answers to the answer key and calc score
   answers.indices.foreach(i => {
     val correctAnswer = key(i)
     val answer = answers(i)

     if (answer == correctAnswer) {
       score += 1
     }
   })

   score / key.size
 })

 // calc class average
 scores.sum / studentAnswers.size
}
```

An immediate improvement here would be to add error checking checking for empty list input.
