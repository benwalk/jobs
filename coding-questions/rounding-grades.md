# Rounding Grades

Sam is a professor at the university and likes to round each student's grade according to these rules:
- If the difference between the grade and the next multiple of 5 is less than 3, round  up to the next multiple of 5.
- If the value of grade is less than 38, no rounding occurs as the result will still be a failing grade.

In Scala, I thought the easiest solution to grok involved defining a grade object. This makes the actual logic very quick.
```
object Grade {
    /**
     * Constructs a Grade object from an integer.
     */
    def fromInt(score: Int): Grade = {
        val roundUpBy = (score % 5) match {
            // e.g., ends in 3 or 8, add 2 to get to next multiple
            case 3 => 2
            // e.g., ends in 4 or 9, add 1
            case 4 => 1
            // otherwise it doesn't round up
            case _ => 0
        }

        val passable = score >= 38 // number below which fails regardless

        if (!passable){
            Grade(score, false)
        }
        else {
            Grade(score + roundUpBy)
        }
    }
}

/**
 * Reprensentation of a "Professor Sam Grade", which is a rounded
 * version of a normal grade.
 */
case class Grade(
    val grade: Int,
    val passing: Boolean = true
)

/**
 * Given an array of unrounded grades returns an array
 * of rounded grades.
 */
def gradingStudents(grades: Array[Int]): Array[Int] = {
    grades.map(Grade.fromInt(_).grade)
}
```

Analysis: linear time - one iteration through the array.

Improvements:
- To the code golfer, you don't _need_ an object definition for this. You could just define a rounding function and map over the array with that.
