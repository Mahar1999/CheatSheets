# Regex

https://regex101.com/ - practise site

_A list of my commonly used commands -- Mahar1999_

# Special-Character

NOTE - when you want to include '.' in an expression u directly cant use it as it is already defined with a diffrent meaning . Thus to specify '.' as an '.' we use backslash i.e '\\.'

WE USE '\\' to escape the speacial meaning and write the character as an characeter as done with '.'

| Charater | Description                                                    |
| -------- | -------------------------------------------------------------- |
| `[]+`    | The one-or-more quantifier                                     |
| `\`      | The escape character                                           |
| `[]`     | The character set                                              |
| `[^]`    | The negate symobol in a character set                          |
| `?`      | The zero-or-one quantifier(makes preceding character optional) |
| `.`      | Accepts all after the dot( except the newline character)       |
| `*`      | The 0-or-more quantifier( a bit like +)                        |
| `\|`     | OR                                                             |

# Commands

NOTE-The ranges a-z ,A-z , 0-9 arent fixed and we may customize them according to our use like for example
e.g. h-m,S-Y,5-8...etc

| Command        | Description                                                                   |
| -------------- | ----------------------------------------------------------------------------- |
| `/ninja/`      | Filters ninja from string                                                     |
| `/[ng]inja/ `  | Filters ninja or ginja from string                                            |
| `/[^p]inja/`   | Filter everything except pinja                                                |
| `/[a-z]inja/`  | Charset (a-z) followed by "inja" will match                                   |
| `/[A-Z]inja/`  | Charset (A-Z) followed by "inja" will match                                   |
| `/[0-9]inja/`  | Numset (0-9) followed by "inja" will match                                    |
| `/[0-9]{10}/`  | '{ }' Repeats the condition 10 times(Like a phone number)                     |
| `/[0-9]{5,8}/` | '{ }' Repeats the condition 5 to 8 times                                      |
| `/[0-9]{5,8}/` | '{ }' Repeats the condition atleast 5 times                                   |
| `/ninja?/`     | Makes the preceding char optional,here 'a'                                    |
| `/^[a-z]{5}/`  | Here '^' is outside the [], which means the string starts with the expression |
| `/[a-z]{5}$/`  | The string ends with the given expression                                     |
| `/^[a-z]{5}$/` | The string ends and starts with the expression given                          |
| `(h\|p)ot`     | Either hot or pot                                                             |

# Flags

| Flags/Modifier | Description                        | Name        |
| -------------- | ---------------------------------- | ----------- |
| `g`            | Matches all matching string        | Global      |
| `i`            | Avoids sensitivities of characters | Insensitive |

# Meta-Character

| Charater | Description                                            |
| -------- | ------------------------------------------------------ |
| `-\d`    | Match any digit character (same as [0-9])              |
| `-\w`    | Match any word character (same as a-z,A-Z,0-9 and \_ ) |
| `-\s`    | Match a whitespace character (spaces,tabs)             |
| `-\t`    | Match a tab character only                             |
