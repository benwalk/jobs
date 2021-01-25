# Time Conversion from 12-hour to 24-hour format

In Java,
```
/**
 * Converts a time to 24-hour time format. The given string must
 * conform to `HH:MM:SS[AP]M` format.
 */
static String timeConversion(String s) {

    // basic checks
    if (s == null || s.length() != 10){ 
        throw new IllegalArgumentException();
    }

    // store to prevent copying this expression, increase readability
    String withoutMeridiem = s.substring(0, s.length() - 2); 

    // store to prevent multipl string read & assessments
    Boolean isAM = StringUtils.right(s, 2).equals("AM"); 

    // store for comparison and math
    String hour  = s.split(":")[0];

    if (isAM && hour.equals("12")) {
        return withoutMeridiem.replaceFirst(hour, "00");
    }
    else if (!isAM && Integer.parseInt(hour) < 12) {
        return withoutMeridiem.replaceFirst(hour, Integer.parseInt(hour) + 12 +"");
    }
    else {
        return withoutMeridiem;
    }
}
```

This utilizes `import org.apache.commons.lang3.StringUtils;` which may or may not be allowed depending on the quizzer. In reality, you are probably always going to have access to a StringUtils pacakge of some sort.

Analysis: Constant time. The size of the input is constant.
