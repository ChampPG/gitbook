---
description: Regular Expression Cheat Sheet
---

# Regular Expression

### Regular Expression Websites

[https://regexone.com/](https://regexone.com/) - Very nice and quick questions to learn more about regex



### Basic Matching

Each symbol matches a single character

| Syntax            | Description                        |
| ----------------- | ---------------------------------- |
| .                 | Anything                           |
| \d                | Digit in 0,1,2,3,4,5,6,7,8,9       |
| \D                | Non-digit                          |
| \w                | "Word" (letters and digits and \_) |
| \W                | Non-word                           |
| \c                | Control Character                  |
| {SPACE\_KEYPRESS} | space                              |
| \t                | tab                                |
| \r                | return                             |
| \n                | new line                           |
| \s                | whitespace                         |
| \S                | non-whitespace                     |
| \x                | Hexadecimal digit                  |
| \O                | Octal digit                        |

### Character Classes

{% embed url="https://www.regular-expressions.info/charclass.html" %}

{% embed url="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions/Character_Classes" %}

| Syntax  | Description                                                                              |
| ------- | ---------------------------------------------------------------------------------------- |
| \[xyz]  | `[abcd]` is the same as `[a-d]`. They match the "b" in "brisket", and the "c" in "chop". |
| \[^xyz] | `[^abc]` is the same as `[^a-c]`. They initially match "o" in "bacon" and "h" in "chop". |

### Escape Sequences

"­Esc­api­ng" is a way of treating characters which have a special meaning in regular expres­sions literally, rather than as special charac­ters. The escape character is usually \\

| Syntax | Description                |
| ------ | -------------------------- |
| \\     | Escape following character |
| \Q     | Begin literal sequence     |
| \E     | End literal sequence       |

### Boundaries

Boundary characters are helpful in "anchoring" your pattern to some edge, but do not select any characters themselves

| Syntax | Description                                                  |
| ------ | ------------------------------------------------------------ |
| \b     | word boundaries (as defined as any edge between a \w and \W) |
| \B     | non-word boundaries                                          |
| \A     | Start of string                                              |
| \Z     | End of string                                                |
| \\<    | Start of word                                                |
| \\>    | End of word                                                  |
| ^      | the beginning of the line                                    |
| $      | The end of the line                                          |

Example: `\bcat\b` finds a match in "the cat in the hat" but not in "locate"

### Quantifiers

By default quantifiers just apply to the one character. Use (...) to specify explicit quantifier "scope"

| Syntax | Description                                |
| ------ | ------------------------------------------ |
| X\*    | 0 or more repetitions of X                 |
| X+     | 1 or more repetitions of X                 |
| X?     | 0 or 1 instances of X                      |
| X{m}   | Exactly m instances of X                   |
| X{m,}  | At least m instances of X                  |
| X{m,n} | Between m and n (inclusive) instances of X |

### Disjunction

| Syntax | Description |
| ------ | ----------- |
| (X\|Y) | X or Y      |

Example: `\b(cat|dog)s\b` matches cats and dogs.

### Special Characters

The character `{} [] ^ $ . | * + > \` (and - inside \[...]) have special meaning in regex, so they must be "escaped" with \ to match them

Example: `\.` matches the period `.` and `\\` matches the backslash `\`

### Backreferences

Count your open parentheses `(` from the left, starting with 1. Whatever is matched by parthesis number `n` can be refernced later by `\n`

Example: `\b(\w+) \1\b` matches two identical words with a space in between

Example 2: `\b(\w+)er\b` and replacing with `more \1` will map "the taller man" -> "the more tall man" and "I am shorter" -> "I am more short"
