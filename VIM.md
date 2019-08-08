   k
h     l
   j

## WEB - navigate WORDs

## WORD vs word

A **WORD** consists of a sequence of non-blank characters, separated with white space. An empty line is also considered to be a WORD. Use 'W', 'E', and 'B' to navigate WORDs.
A **word** consists of a sequence of letters, digits and underscores, or a sequence of other non-blank characters, separated with white space (spaces, tabs, <EOL>). An empty line is also considered to be a word.

Use 'w', 'e', and 'b' to navigate words.

- w -- [count] words forward | position the cursor at the **beginning** of the word
- e -- forward to the **end** of word [count]
- b -- [count] wordS backward | position the cursor at the **beginning** of the word

> same small letters are doing the same, but with words, not WORDs


- r{char} -- replace the character | `6rX`

- x -- delete [count] chars under and **after** the cursor

- X -- delete [count] chars **before** ..

Deleteing with x at times is too slow, you can delete whole words in one go. **_d_ folloewd by _w_** deletes word to the end.

- d{motion} -- delete text that {motion} moves over [into a register if specified] | _dw, db, d71, dj (delete this line + line below)_

- D -- delete the characters under the cursor until the end of the line and [count]-1 more lines [into a register], synonym for 'd$' | _3D_

- ~ -- switch case of the character under the cursor and move the cursor to the right. If a [count] is given, do that many characters. | 9~

- $ -- go to the end of the line. When a count is given also go [count-1] lines downward. | _$, 2$_

- 0 -- go to the first character of the line. (very first character, even space)

- ^ -- go to the first non-blank charater of the line.

- f{char} -- go to [count]'th occurrence of {char} to the right. The cursor is placed on {char}. | _3ft_

- F{char} -- go to [count]'th occurrence of {char} to the left. The cursor is placed on {char}. | _3Ft_

- t{char} -- go till before [count]'th occurrence of {char} to the right. The cursor is placed on the character left of {char}. | _3tt_

- T{char} -- go till after [count]'th occurrence of {char} to the left. The cursor is placed on the character right of {char}. | _3Tt_

- , -- repeat latest f, t, F or T in opposite direction. | _fu,  tt2,_

- ; -- repeat latest f, t, F of T [count] times. | _fu;  Tt3;_

- zt, zz, zb -- redraw, cursor line at:
	- zt - top of window
	- zz - center of window
	- zb - bottom of window

- % -- find the next item in this line after or under the cursor and jump to its match. Items can be: ([{}])/* */ #if #ifdef #else #elif #endif. No count is allowed, {count}% jumps to a line {count} percentage down the file.

> very useful for coding

- gg -- goto line [count], default first line, on the first non-blank character | 5gg

- G -- goto line [count], default last line, on the first non-blank character | 5G

- * -- search forward for the [count]'th occurrence of the while word nearest to the cursor in the current line. The word used for the search is the first of:
	- the keyword (A-Za-z0-9\_@) under the cursor 
	- the first keyword after the cursor
	- the non-blank word under the cursor
	- the first non-blank word after the cursor
> _2*_

- # -- same as '\*', but search backward | 2#

- n -- repeat the latest '/' or '?' [count] times. '\*' and '#' searches are also considered '/' and '?' repectively. | _*2n_

- N -- repeat the latest ... in **opposite direction**

- [count] -- an optional number that may precede the command to multiply or iterate the command. If no number is given, a count of one is used, unless otherwise noted. Use 'del' to erase the last digit

- p -- put the text [from the specified register] after the cursor [count] times. When no register is specified, use the unnamed register (") which contains the last text deleted (d,x), changed (c, s), or yanked (y).

- P -- put the text ... **before** 

> "{register}p(or P)

- " -- use regiester {a-zA-Z0-9.%#:-"} for next delete, yank or put (i.e. paste). Use uppercase cahracter to append with delete and yank. {.%#:} only work with put and are currently not supported in the game. Type :reg to see the register's content.

- y -- yank {motion} text [into a register]. Text is stored into "0 register unless another register is specified. | _y2w_

- c{motion} -- delete (change) {motion} text [into the specified register] and start insert. 'cw' and 'cW' are treated like 'ce and 'cE' is interpreted as change-word, and a word does not include the following white space. _cc_ changes the whole line.

- i -- insert text before the cursor [count] times. | _3isometext{esc}_

- a -- append text after the cursor [count] times. If the cursor is in the first column of an empty line Insert starts three.

- o -- begin a new line below the cursor and insert text, repeat [count] times.

- s -- delete (subttitute) [count] characters [into the specified register] and start insert (s stands for _Substitute_). Synonym for 'cl' (not linewise).

- ) -- [count] sentences forward. A sentence is defined as ending at a '.', '!' or '?' followed by either the end of a line, or by a space of tab. Any number of closing ')', ']', '"' and ''' characters may appear after the '.', '!', or '?' before the spaces, tabs or end of line. A paragraph bondary (an empty line) is also a sentence boundary.

- ) -- [count] sentences **backward**...

- [{, [(, ]), ]} -- go to [count] previous (or next) unmatched '{' (or ')') starting at, but not including, cursor position. _To understand it better, just go to vim-adventures.com and type ':help [{'_

- } -- [count] paragrahps forward. Move the cursor to the empty line after the current paragraph, or after the next paragraph if the cursor isn't in a paragraph.

- { -- [count] paragraphs **backward**

- text-objects -- text objects are two characters used after an operator ('d', 'y', 'c' etc.) to select a range to operate on. The first character is either 'a' (for "an object", including white space) or 'i' (for "inner" oject, without surrounding white space, or only the white space). The second character denotes the object type and is one of the following:
	- **w**ord, **W**ORD, **s**sentence, **p**aragraph
	- **"** or **'** - a ", ', or ` quoted string
	- {, }, or B - A {} block
	- (, ), or b - a () block
	- [ or ] - A [] block
	- < or > - a <> block
	- **t** - A HTML or XML tag block

- . -- repeat the last simple change. Without a count, the count of the last change is used If you enter a count, it will replace the last onel. If the last change included a specification of numbered register, the register number will be incremented. Does not repeat a command-line command.

> well, i guess that's enought for now for you, to go on go to youtube and type there _Vim Adventures - levels 4-12 (Speed Run Practice)_
