##### 预定义类

Character | Meaning
----------|--------
`.`|matches any single character except the newline character.
\d|Matches a digit character. Equivalent to [0-9].
\D|Matches any non-digit character. Equivalent to [^0-9].
\s|Matches a single white space character, including space, tab, form feed, line feed（空白符）
\S|Matches a single character other than white space（非空白符）
\w|Matches any alphanumeric character including the underscore. Equivalent to [A-Za-z0-9_].
\W|Matches any non-word character. Equivalent to [^A-Za-z0-9_].

`.`匹配除了回车和换行之外的所有字符，等价于[^\r\n]


##### 边界

Character | Meaning
----------|--------
`^`|Matches beginning of input.
`$`|Matches end of input.

