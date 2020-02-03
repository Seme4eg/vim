hjkl, dear neophyte, now go [here](https://vim-adventures.com) and come back to this repo after u done at
least all free levels of this game

now type `:help user-manual` and check how much u actually know now, reading it from top to bottom, stop
when/if u r completely lost

done already? ok, if u still don't feel yourself confident when using vim, read my notes below..


# vim built-in documentation

`:help usr_02.txt` --> 02.8 Finding help (or just `:help 02.8`)

or `:help helphelp`


# WORD vs word

A **WORD** consists of a sequence of non-blank characters, separated with white space. An empty line is also
considered to be a WORD. Use 'W', 'E', and 'B' to navigate WORDs.

A **word** consists of a sequence of letters, digits and underscores, or a sequence of other non-blank
characters, separated with white space (spaces, tabs, <EOL>). An empty line is also considered to be a word.

- `w` - move to the beginning of next word | `3w`
- `e` - move to the end of cur. word | `3e`
- `ge` - move to the end of prev. word | `3e`
- `b` - move to the beginning of prev. word | `3b`

> big letters are doing the same but with WORDs


# Basic operations

`r{char}` - replace the character | `6rX`
`R` - enter replace mode

`d{motion}` - delete text {motion} | _dw, db, diw, das, d71, dj (delete this line + line below)_

- `x` (chortcut for `dl`) - delete [count] chars **under** and **after** the cursor
- `X` (chortcut for `dh`) - delete [count] chars **before** the cursor
- `D` (chortcut for `d$`) - delete to the end of the line
- `C` (chortcut for `c$`) - change to the end of the line
- `s` (chortcut for `cl`) - change one char
- `S` (chortcut for `cc`) - change a whole line

`u` - undo last change(s)

`U` - undo all the changes on a line

`~` - switch case | `9~`


# Line navigation

`$` - go to the end of the line | `$`, `2$`

`0` - go to the first character of the line. (very first character, even space)

`^` - go to the first non-blank charater of the line.

`H/M/L` - move cursor to top/middle/bottom of current lines

`zt/zz/zb` - redraw, cursor line at top/center/bottom accordingly


# Searching

`f{char}` - find forward (only on cur. string). The cursor is placed on {char}. | `3ft`

`F{char}` - find backward ..

`t/T{char}` - find forward. The cursor is placed left of {char}. | `3tt`

`n/N` - repeat the latest '/' or '?' [count] times (`N` repeats in opposite direction). '\*' and '#'
  searches are also considered '/' and '?' repectively. | _*2n_

`,` - repeat latest f, t, F or T in opposite direction. | _fu,  tt2,_

`;` - repeat latest f, t, F of T [count] times. | _fu;  Tt3;_

`*/#` - search forward/backward for the [count]'th occurrence of the while word nearest to the cursor | `2*`


# Navigation

`%` - find the next ([{}])/* */ #if #ifdef #else #elif #endif.
> very useful for coding

`{count}%` - jumps to a line {count} percentage down the file.

`gg/G` - goto line [count], default first/last line accordingly | 5gg, 5G


# Text objects

**text-objects** - text objects are two characters used after an operator ('d', 'y', 'c' etc.) to select a range
to operate on. The first character is either 'a' ("an object") or 'i' ("inner"). The second character denotes
the object type and is one of the following:

- **w**ord, **W**ORD, **s**entence, **p**aragraph
- `"`, `'`, \` - quoted strings
- `{`, `}`, or B - A {} block
- `(`, `)`, or b - a () block
- `[` / `]` - A [] block
- `<` / `>` - a <> block
- **t**ag - A HTML or XML tag block

`)/(` - [count] sentences forward/backward. A sentence is defined as ending at a '.', '!' or '?' followed by
  either the end of a line, or by a space or tab. Any number of closing ')', ']', '"' and ''' characters may
  appear after the '.', '!', or '?' before the spaces, tabs or end of line. A paragraph bondary (an empty
  line) is also a sentence boundary.

`[{, [(, ]), ]}` - go to [count] previous (or next) unmatched '{' (or ')') starting at, but not including,
  cursor position. _To understand it better, just go to vim-adventures.com and type ':help [{'_

`}/{` - [count] paragrahps forward/backward. Move the cursor to the empty line after the current paragraph,
  or after the next paragraph if the cursor isn't in a paragraph.


# Inserting

`i/a` - insert text before/after the cursor | `3isometext{esc}`
`i/a` - start inserting at the beginning/eng of the line

`o` / `O` - begin a new line below/above the cursor and insert text, repeat [count] times.


# Regs and yanking (copying) / deleting / cutting

`"{register}p/P` - put the text [from the specified register] after/before the cursor [count]
  times. Def. register is `"`, which contains the last text deleted (d,x), changed (c, s), or yanked (y).

`"` - use regiester {a-zA-Z0-9.%#:-"} for next delete, yank or put (i.e. paste). Use uppercase cahracter to
  append with delete and yank.

`:reg` to see the register's content.

`y` - yank {motion} text [into a register]. Def. register is 0

`c{motion}` - delete (change) {motion} text [into the specified register] and start insert. | `cw` `cE`, `cc`
(changes the whole line)

`s` - delete (substitute) [count] characters [into the specified register] and start insert


# Other

> `=i{` - indent text within the scope (or `vi{` ..)

- . - repeat the last simple change. Does not repeat a command-line command.
