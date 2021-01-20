# Counting Valleys

A hiker following a path tracks each step as either uphill or downhill. Every section of the path that is spent below the starting elevation is considered a "valley." This function will count the valleys in a given path.

In Java,
```
/**
 * Returns the number of valleys on a given path, as defined by:
 * - a sequence of steps below "sea-level"
 * - "sea-level" is always the initial (and final) elevation
 *
 * Assumptions:
 * - `steps` is in the range 2 .. 10^6
 * - `path` is a string containing only the chars `D` and `U`
 * - if `steps` or the length of `path` is odd, throwing an exception is acceptable
 */
public static int countingValleys(int steps, String path) 
    throws IllegalArgumentException {

    // check the invalid case of odd number of steps
    if ((steps%2) != 0 ||  (path.length()%2) != 0) {
        throw new IllegalArgumentException();
    }

    int elevation = 0; // start at sea-level
    int numValleys = 0;

    for(char step : path.toCharArray()) {
        switch(step) {
            case 'U':
                if (elevation == -1) numValleys++;
                elevation++;
                break;

            case 'D':
                elevation--;
                break;

            default:
                throw new IllegalArgumentException();
        }   
    }

    if (elevation != 0) throw new IllegalArgumentException();

    return numValleys;
}
```

Analysis: 
- Runs in linear time. We have to trace the full path in order to determine the total number of valleys.

Improvements
- throwing exceptions isn't super user friendly. returning helpful error messages could improve how a caller of this might respond.


