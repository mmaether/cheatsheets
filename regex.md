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

[Useful Regex Patterns](https://projects.lukehaas.me/regexhub/)

| Characters | Meaning | Example
| -----------| ------- | -------
`/^(0?[1-9]\|[12][0-9]\|3[01])([ \/\-])(0?[1-9]\|1[012])\2([0-9][0-9][0-9][0-9])(([ -])([0-1]?[0-9]\|2[0-3]):[0-5]?[0-9]:[0-5]?[0-9])?$/` | Date in format `dd/mm/yyyy`. Will match dates with dashes, slashes or with spaces (e.g. `dd-mm-yyyy`, `dd/mm/yyyy`, `dd mm yyyy`), and optional time separated by a space or a dash (e.g. `dd-mm-yyyy-hh:mm:ss` or `dd/mm/yyyy hh:mm:ss`). | `09/02/2019` <br> `09-02-2019` <br> `09 02 2019` <br> `09-02-2019-13:33:54` <br> `09-02-2019 13:33:54`
`/^([01]?[0-9]\|2[0-3]):[0-5][0-9]$/` | Time in 24-hour format. | `12:30` or `23:59`
`/^<([a-z1-6]+)([^<]+)*(?:>(.*)<\/\1>\| *\/>)$/` | HTML tags. Match opening and closing HTML tags with content between. | `<body></body>`
`/^#?([a-fA-F0-9]{6}\|[a-fA-F0-9]{3})$/` | Hex color value. | `#fff` or `#ffffff`
`/^.+@.+$/` | Email. Verify that there is an @ symbol with something before it. | `zap.brannigan@example.com`
`/^\+?(\d.*){3,}$/` | Phone Number. | (555) 555-5555
`/[\r\n]\|$/` | New line. | `\r\n`

## Resources

* [MDN Regular Expression Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)
* [Regexr](https://regexr.com/)
* [Regular Expressions 101](https://regex101.com/)
