# Jumping On Clouds
I think I've seen a variation of this problem where a frog is trying to jump out of a well. The key is to realize that a large jump at the end will put you out of bounds, or - in this case - is also not needed.

The rules:
> There is a new mobile game that starts with consecutively numbered clouds. Some of the clouds are thunderheads and others are cumulus. The player can jump on any cumulus cloud having a number that is equal to the number of the current cloud plus  or . The player must avoid the thunderheads. Determine the minimum number of jumps it will take to jump from the starting postion to the last cloud. It is always possible to win the game.

In Java,
```
/**
 * Returns the minimum number of jumps required from start to finish,
 * following the rules of the game:
 * - Jumps can be to the next cloud, or they can skip at most 1 cloud.
 * - Thunderhead clouds must be avoided (jumped over and not landed on).
 * 
 * Assumptions:
 * - `c` is formatted correctly (number of clouds -> \n -> array of [0,1]+)
 * - The game can always be won.
 */
static int jumpingOnClouds(int[] c) throws IllegalArgumentException {

    int numClouds = c.length;
    System.out.println("There are "+ numClouds +" clouds this game.");
    int numJumps = 0;
    for(int i = 0; i < numClouds - 1; i++ ) {
        System.out.print("From Cloud " + i);

        // check double jump
        if (i+2 < numClouds && c[i+2] == 0) {
            System.out.println(", double jumping to Cloud " +(i+2) +".");
            i++;
            numJumps++;
        }
        // otherwise, single jump is the default
        else {
            System.out.println(", jumping to Cloud " +(i+1) +".");
            numJumps++;
        }
    }

    return numJumps;
}
```

Analysis: Runs in linear time.

Improvements: 
- Validate inputs, despite the provided constraints and assumptions (array could be `null`, contain invalid ints, or no ints).
- Throwing an exception, while perfectly valid, may not be the most useful to the caller. For a game API, consider user-facing messages.
- STDOUT logging is fairly rudimentary. Ideally, using a logging framework, this could be tagged with a level for easier troubleshooting live systems.
