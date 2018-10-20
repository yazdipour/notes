# Regex

* `^((?!XXX).)*$` Get Lines that not have XXX

---
* `^abc$`	start-end of the string
* `.`	any character except newline
* `\w\d\s`	word, digit, whitespace
* `\W\D\S`	not (word, digit, whitespace)
* `[abc]`	any of a, b, or c
* `[^abc]`	not a, b, or c
* `[a-g]`	character between a & g
* `(abc)`	capture group
* `\1`	backreference to group #1
* `(?:abc)`	non-capturing group
* `(?=abc)`	positive lookahead
* `(?!abc)`	negative lookahead
* `a*a+a?`	0 or more, 1 or more, 0 or 1
* `a{5}a{2,}`	exactly 5, 2 or more
* `a{1,3}`	between one & three
* `\.\*\\`	escaped special characters
* `\t\n\r`	tab, linefeed, carriage return
* `[A-Fa-z1-4]` This would match uppercase letters from A to F, all lowercase and the numbers 1 to 4