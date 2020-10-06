__Regular Expression__ or __regex__ → sequence of characters that define a search pattern. It's often use by string searching algorithms, or for input validation.

## Terminology
__greedy match__ → finds the longest possible part of a string that fits the regex pattern and returns it as a match. This is the default behaviour.\
*e.g.* `/t[a-z]*i/` → titanic

__lazy match__ → finds the smallest possible part of the string that satisfies the regex pattern. You can change to this behaviour using `?`.\
*e.g* `/t[a-z]*?i/` → ti

## JavaScript functions
Function | Description | Return
--- | --- | ---
`regex.test(str)` | test if the string matches with the regex | boolean
`regex.exec(str)` | execute a search for a match in a specified string | array \| null
`str.match(reg)` | retrieves the resulf of matching against the specified regex | array \| null
`str.replace(reg, '')` | replace the matched text. We can access the capture group using `$n` | string

## Flags
Flag | Description
--- | ---
`i` | case insensitive
`g` | extract or search the pattern more than once

*e.g.* `/test/g`

## Wildcards
Wildcard | Description | Example
--- | --- | ---
`a|b` | OR operator
`.` | dot/period. Match any one character, except newline
`[]` | character classes. Define a group of characters we wish to match | `[a-zA-Z]`
`[^]` | negated character set. Define a group of characters we don't want to match | `[^a-c]`
`y?` | match zero or one character
`y+` | match one or more characters
`y*` | match zero or more characters
`^` | caret. Sarch for patterns at the beginning of the string | `^[abc]`
`$` | dolar sign. Sarch for patterns at the end of the string | `word$`
`{n,n}` or `{n}` | quantity specifier. Specify a certain range of patterns | `a{5}` \| `a{2,}`
`( )` | capture groups. Check for group of characters. Also used to find repeated substrings | `(abc)`
`(?: )` | non-capturing group. Groups multiple tokens without creating a capture group | `(?:abc)`
`\n` | backreference to capture group #n. Starts at 1 | `(abc)(def)\1`

### Lookahead
They tell JavaScript to look-ahead in our string to check for patterns further along. This can be useful wen we want to search for multiple patterns over the same string.
- `(?=...)` → positive lookahead. Look to make sure the element in the search is there, but won't actually match it.
- `(?!...)` → negative lookahead. Look to make sure the element in the search is not there. The rest of the pattern is returned if the negative lookahead is not present.

## Character classes
Class | Description | Equivalent match 
--- | --- | ---
`\w` | alphabetic letters, numbers, and underscore | `[A-za-z0-9_]`
`\W` | negated `\w` | `[^A-Za-z0-9_]`
`\d` | digits | `[0-9]`
`\D` | negated `\d` | `[^0-9]`
`\s` | white space, including carriage return, tab, form feed, and new line
`\r` | carriage return
`\t` | tab
`\f` | form feed
`\n` | new line
`\v` | vertical tab
`\S` | non-white space