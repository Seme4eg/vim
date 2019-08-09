   k
h     l
   j

## WORD vs word

A **WORD** consists of a sequence of non-blank characters, separated with white space. An empty line is also considered to be a WORD. Use 'W', 'E', and 'B' to navigate WORDs.
A **word** consists of a sequence of letters, digits and underscores, or a sequence of other non-blank characters, separated with white space (spaces, tabs, <EOL>). An empty line is also considered to be a word.

- w -- move to the beginning of next word | `3w`
- e -- move to the end of cur. word | `3e`
- b -- move to the beginning of prev. word | `3b`

> same big letters are doing the same but with WORDs

- r{char} -- replace the character | `6rX`
- x -- delete [count] chars under and **after** the cursor
- X -- delete [count] chars **before** ..

- d{motion} -- delete text {motion} | _dw, db, d71, dj (delete this line + line below)_
- D -- deletes until the end of the line, synonym for 'd$' | `3D`

- ~ -- switch case | `9~`

- $ -- go to the end of the line | `$`, `2$`
- 0 -- go to the first character of the line. (very first character, even space)
- ^ -- go to the first non-blank charater of the line.

- f{char} -- find forward (only on cur. string). The cursor is placed on {char}. | `3ft`
- F{char} -- find backward ..

- t/T{char} -- find forward. The cursor is placed left of {char}. | `3tt`

- , -- repeat latest f, t, F or T in opposite direction. | _fu,  tt2,_
- ; -- repeat latest f, t, F of T [count] times. | _fu;  Tt3;_

- zt/zz/zb -- redraw, cursor line at top/center/bottom accordingly

- % -- find the next ([{}])/* */ #if #ifdef #else #elif #endif.
> very useful for coding
- {count}% -- jumps to a line {count} percentage down the file.

- gg/G -- goto line [count], default first/last line accordingly | 5gg, 5G

- */# -- search forward/backward for the [count]'th occurrence of the while word nearest to the cursor | `2*`

- n -- repeat the latest '/' or '?' [count] times. '\*' and '#' searches are also considered '/' and '?' repectively. | _*2n_
- N -- repeat the latest ... in **opposite direction**

- "{register}p/P -- put the text [from the specified register] after/before the cursor [count] times. Def. register is `"`, which contains the last text deleted (d,x), changed (c, s), or yanked (y).

- " -- use regiester {a-zA-Z0-9.%#:-"} for next delete, yank or put (i.e. paste). Use uppercase cahracter to append with delete and yank.
- `:reg` to see the register's content.

- y -- yank {motion} text [into a register]. Def. register is 0

- c{motion} -- delete (change) {motion} text [into the specified register] and start insert. | `cw` `cE`, `cc` (changes the whole line)
- s -- delete (substitute) [count] characters [into the specified register] and start insert

- i/a -- insert text before/after the cursor | `3isometext{esc}`
- o -- begin a new line below the cursor and insert text, repeat [count] times.

- )/( -- [count] sentences forward/backward. A sentence is defined as ending at a '.', '!' or '?' followed by either the end of a line, or by a space or tab. Any number of closing ')', ']', '"' and ''' characters may appear after the '.', '!', or '?' before the spaces, tabs or end of line. A paragraph bondary (an empty line) is also a sentence boundary.

- [{, [(, ]), ]} -- go to [count] previous (or next) unmatched '{' (or ')') starting at, but not including, cursor position. _To understand it better, just go to vim-adventures.com and type ':help [{'_

- }/{ -- [count] paragrahps forward/backward. Move the cursor to the empty line after the current paragraph, or after the next paragraph if the cursor isn't in a paragraph.

- text-objects -- text objects are two characters used after an operator ('d', 'y', 'c' etc.) to select a range to operate on. The first character is either 'a' ("an object") or 'i' ("inner"). The second character denotes the object type and is one of the following:
	- **w**ord, **W**ORD, **s**sentence, **p**aragraph
	- ", ', ` - quoted strings
	- {, }, or B - A {} block
	- (, ), or b - a () block
	- [ or ] - A [] block
	- < or > - a <> block
	- **t**ag - A HTML or XML tag block

- . -- repeat the last simple change. Does not repeat a command-line command.
