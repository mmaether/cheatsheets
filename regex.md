# Regular Expressions

[Regex Cheat Sheet](https://www.petefreitag.com/cheatsheets/regex/)

| Character | Meaning | Example
|-----------|---------|--------
\* | Match **zero, one or more** of the previous. | `Ah*` matches `"Ahhhhh"` or `"A"`
? | Match **zero or one** of the previous. | `Ah?` matches `"Al"` or `"Ah"`
\+ | Match **one or more** of the previous. | `Ah+` matches `"Ah"` or `"Ahhh"` but not `"A"`
\ | Used to **escape** a special character. | `Hungry\?` matches `"Hungry?"`
. | Wildcard character, matches **any** character. | `do.*` matches `"dog"`, `"door"`, `"dot"`, etc.
( ) | **Group** characters. | See example for `|`
[ ] | Matches a **ranges** of characters. | `[cbf]ar` matches `"car"`, `"bar"`, or `"far"` <br> `[0-9]+` matches any positive integer <br> `[a-zA-Z]` matches ASCII letters a-z (uppercase and lower case) <br> `[^0-9]` matches any character not 0-9. 
\| | Match previous **OR** next character/group. | `(Mon)\|(Tues)day` matches `"Monday"` or `"Tuesday"`
{ } | Matches a specified **number of occurrences** of the previous. | `[0-9]{3}` matches `"315"` but not `"31"` <br> `[0-9]{2,4}` matches `"12"`, `"123"`, and `"1234"` <br> `[0-9]{2,}` matches `"1234567..."`
^ | **Beginning** of a string. Or within a character range [] negation. | `^http` matches strings that begin with http, such as a url. <br> `[^0-9]` matches any character not 0-9.
$ | **End** of a string. | `ing$` matches `"exciting"` but not `"ingenious"`
