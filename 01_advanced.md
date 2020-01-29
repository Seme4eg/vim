# Sources

> When you are browsing Vim’s documentation, you can follow the link
> under the cursor with the command: `ctrl-]`

Now go [here](http://derekwyatt.org/vim/tutorials/index.html) and go through all tutors from top to bottom,

And as additional info watch some [vimcasts](http://vimcasts.org/episodes/archive/)


# some clippings from 'user-manual'

## moving around (usr_03.txt)

### line travelling (03.5)

- `H/M/L` - move cursor to top/middle/bottom of current lines

### scrolling around (03.7)

- `zt/zz/zb` - redraw, cursor line at top/center/bottom accordingly


### simple searches (03.8)

`:set {options}` - set options for search

**ignoring case**:
- 'ic' (ignorecase)	- ignore upper/lower case when searching
- 'nic' (noignorecase)	- ignore upper/lower case when searching

**highlight search**:
- 'hls' (hlsearch) - highlight all matching phrases
- 'nhls' (nohlsearch) - disable highlight of all matching phrases

`:nohl` -> to disable highlighting of search instances -

**tuning search**:
- 'is' (incsearch) - show partial matches for a search phrase
- 'nowrapscan' - stops search at the end/start of file. (on by default)


### using marks (3.10) + change/jump-list

\`\` / `''` - jump to your previous position (will jump back if u use it again) (not same as `C-o`, but similar)

**jumplist** - remembering each position to which the cursor jumped, rather than scrolled

`C-o` / `C-i` - move backward / forward through the jumplist

`:jumps` - view the contents of the jumplist. Entry which u used last is marked as `>`

#### named marks

`m + {mark}` - mark some place in file with specified letter, to find it faster

`' + {mark}` - go to the marked with this letter

special marks (`:marks`):
- `'` - cursor position before doin a jump
- `"` - cursor position when last edigin file
- `[` / `]` - start / eng or the last change

**changelist** - remembers the position of every change that can be undone. You can move back and forwards
through the changelist using the commands:

`g;` / `g,`

> last one is kinda meh, cuz ',' is better as leader, so if u have it it won't work for ya

`:changes` - view the contents of the changelist


## making small changes (usr_04.txt)

### visual mode (04.4)

`ctrl+v` -> start selecting rectangular block

When using blockwise selection, `o` takes u to 1 of the other corners, diagonally, `O` moves to the other
corner in the same line.


## set your settings (usr_05.txt)

basic .vimrc setup taken and modified from https://github.com/amix/vimrc/blob/master/vimrcs/basic.vim

_leader_ is changed it to `,` (`/` - def.)

> `:map` will list u all current mappings

With a map leader it's possible to do extra key combinations

> like `,w` with this config saves the current file

`CR` (carriage return) = `enter` (`:help key-notation`)

`:source $MYVIMRC` - applyes changes to _.vimrc_ without reloading vim


### adding a plugin (05.6)

these are all plugins i've installed for couple weeks of using vim:

- [**Vundle**](https://github.com/VundleVim/Vundle.vim 'see docs')
    - to install added plugins - `:PluginInstall`
    - to update installed pluigns - `:PluginUpdate`
    - [usage docs](https://github.com/VundleVim/Vundle.vim/blob/v0.10.2/doc/vundle.txt#L234-L254)
- [Nerdtree](https://github.com/scrooloose/nerdtree)
- [ctrlp.vim](https://github.com/ctrlpvim/ctrlp.vim)
- [fugitive](https://github.com/tpope/vim-fugitive)
- [syntastic](https://github.com/vim-syntastic/syntastic)



## splitting windows + tabs (usr_08.txt)

http://vimcasts.org/episodes/working-with-windows/

`C-w s` (`:sp[lit] [file]`) - horizontal split

`C-w v` (`:vs[plit] [file]`) - vertical split

`C-w c` (`:close`) - close window

`C-w o` (`:only`) - focus window (make cur. window the only visible)

`C-w hjkl` - switch between windows

`C-w H|J|K|L` - move (swap) windows (08.5)

`C-w >/<` - increase/decrease width (ex. 30<C-w><)

`C-w =` - equalize width and height of all windows

`{height}C-w _` - set window height to a apecified number of lines

**Commands for all windows (08.6):**
- `[q|w|qw]all[!]` - close/save/save'n'close all windows and quit vim
- `vim -[o|O] one.txt two.txt` - open vim with a window splitted horizontally/vertically for each arg


### viewing differences with vimdiff (08.7)

`vimdiff main.c~ main.c`

`vertical diff[split|patch] [[file|patch]name]` - open vertical diffsplit

> `vertical diffpatch main.c.diff` - open vertical diffwindow with patch file

`[c` \ `]c` - jump between changes (if u've disabled changes)

`dp` / `do` (diff put/obtain) - remove difference (use from left/right windows)

[using vimdiff / diffthis](http://vimcasts.org/episodes/comparing-buffers-with-vimdiff/)

> See also: :help CTRL-W & :help vimdiff


### tab pages (08.9)

http://vimcasts.org/episodes/working-with-tabs/

`:tabedit {filename}` - create new tab page with given file

`gt` / `gT` - go to next/prev tab

`:tab split` - creates new tab with current file

`:tabnew` -> creates a new tab (inside new tab is buffer, so it's possible to open a new file in it - :e
  filename

`:tabonly` - close all tabs except current one

`:tabp` -> 'tab previous' - go to the previous tab

`:tabn` -> 'tab next' - go to the next tab


## making big changes (usr_10.txt)

### record and playback commands (10.1)

`q{register}` - start writing macros into given register
`[count]@{register}` - use macros from given register

**editing macros (instead of recording again):**
- `"{register}p` - paste macros
- change commands that were wrong
- yank the corrected commands back into register and use again


### substitution (10.2)

`:[range]s/old/new/[flags]` - substitute 'new' for 'old'

- `%` before `:s` command specifies the command works on all lines (but only 1st occurance on each line)
- `g` flag - change every occurance on **line**
- `p` flag - print out last line it changed
- `c` flag - ask confirmation before each substitution
- `e` flag - tells 'substitute' command that not finding a match is not an error
  - y/n/a - yes/no/all
  - q - quit, don't make any more changes
  - l - last, make this change and then quit

> if u r substituting string with slash in it use this syntax: `:%s+old/slash+newNoSlash` (slashes are
> replaced with plus)

`:%s/\(1st regex\), \(2nd regex\)/\2 \1/` - swaps matches for 1st and 2nd regexps (`\2` and `\1` are
backreferences (pockets))


### command ranges (10.3)

`:#,#s/old/new/g` - #,# are line numbers to which any ':' command can be applyed (single number can be used
to address 1 specific line)

`.` / `$` - is the shortcut for current/last line address

**line duplication (sample)**

`:{range/line_number}y[ank]` - yanks given line without moving the cursor

`:{range/line_number}copy{address}` - copy line(s) and paste to given (address) line

> command 'copy' has shortcut - `t` | _9t._, _.t$_

**using a pattern in a {range}:**

`:?^Chapter?,/^Chapter/s=grey=gray=g` - first `?^Chapter?` finds line above cur. position, that matches, next
`/^Chapter/` finds line below cur. position, adds 2 more lines and replaces 'grey' for 'gray' between those
lines

**adding count manually:**

`:.+3,$-5s/old/new/g` - substract from current line + 3 lines to last line - 5 lines

_Example:_ `.,.+4..` - when u know how many lines to operate on..

**using marks:**

`:'t,'b..` - substract between those marks

> right here in this tutorial, instead of words 'Example' above and below i had words 'Sample', so i decided
> to practice a bit and replaced it with command: `?Sample?-1,/Sample/+1s=sample=Example`, which worked
> perfectly, feel like VIM-superman ^^

**visual modes and ranges:**

select text --> press ':' --> `:'<,'>` will appear ('< and '> are marks, placed at the start and end of the
visual selection) --> any ':' command will be now applyed to this selected text

_Example:_

select text -> `:` -> `:'<,'>w {filename}` - save selected text to file
{filename}


### the global command (10.4)

[docs](http://vimdoc.sourceforge.net/htmldoc/repeat.html#:g)

**global** is similar to 'substitute', but instead of replacing the matched text, {command} is executed

`:[range]g[lobal]/{pattern}/{command}` - Execute {command} (default ":p") on the lines within [range] where
{pattern} matches.

`:[range]g[lobal]!/{pattern}/[cmd]` - opposite as above

`:[range]v[global]/{pattern}/[cmd]` - Same as :g!

_Examples:_

`:g+//+s/foobar/barfoo/g` - replace foobar on barfoo in all C++ style comments (search string is wrapped in
'+' instead of '/' cuz it itself contains '/'

`:g/TODO/yank A` - yank all lines containing 'TODO' word into reg. A

`:4,6g/^/m 't` - move text between lines 4 and 6 to mark 't'


### reading and writing part of a file (10.6)

`:[range]r[ead] {filename}` - paste {filename} contents in current file in [range] | _:$r patch_ - put 'patch'
file contents at the end of cur. file

`:[range]w[rite] {filename}` - write a **[range]** of lines from cur. file into {filename}; use `w!` to
override existing files; use `w >>{filename}` to append to a file


### formatting text (10.7)

`:set textwidth=100` - make lines automatically trim when typing at 100 symbols

`gq{motion}` - format a section of text (ie `gqip` applies formatting to the current paragraph). And after
formatting cursor will be on the last line of the paragraph

`gw{motion}` - same, but the cursor will remain on the word it was on

how hard wrapping behaves depends on _textwidth_ and _wrapmargin_ values, see more about them
[here](http://vimcasts.org/episodes/hard-wrapping-text/)

`:set fo[rmatoptions]+=ta`


### changing case (10.8)

`g{action}{motion}` - perform {action} in {motion} (ik, ima pro at explaining ^^)

To make operator work on lines - double it. ('gUgU' == 'gUU')

_Examples_:

- `gUw` - uppercase next word
- `gUU` (shortcut from 'gUgU') - uppercase whole line
- `g~gn` - switch case on next search match


## clever tricks (usr_12.txt)

### replace a word (12.1)

`:%s/\<four\>/4/g` - replace ' four ' to 4 filewide (not 'thirtyfour' or 'fourteen'), where `\<` means 'match
the beginning of word and `/>` end of word


### find a man page (12.6)

`K` - find the man page for word/func below the cursor

for more info look '12.6' section

# Copy / paste

## Registers

vim has **35** copy buffers

- 1-9 - history registers (delete registers)
- 0 - the **yank** register
- a-z - named registers
- A-Z - same as (a-z) but append
  + _Example_: you copied something in 'a' register, now if you copy something in 'A' register it will apend to
    what is already copied.
- "/ - current search pattern
- "- - small delete
- "_ - the black hole register (_) - deleting in this register actually **deletes**

`:reg` -> view the contents of registers

**`C-r` in INSERT mode puts user in " mode (being able to paste from any register)**

> and the thing above also works in vim command line

`C-r C-o` - inserts literally from current default buffer (useful when repeating with '.' command)

**Read-only registers**

- ": - last :command
- ". - last inserted text
- "% - filename of the current buffer
- "# - filename of the alternate file

> :h registers

`q{reg_name}q` - clear given register (tho don't forget bout black hole register)


## Expression register

"= - expression register

> [how to use it](http://vimcasts.org/episodes/simple-calculations-with-vims-expression-register/)

_Example_:

`C-r =` in insert mode, put there some mathematical expression -> `CR` will paste the result of this
expression


# Extending ':' knowledge

**all commands below are supposed to be used in `:` mode**

`! {bash_command}` - run external command

`r {filename/bash_command}` - puts {filename} content / {command} output below the cursor

`CTRL-D` - see possible completions

`!sort` - sorts selected lines

`e[dit]` called with no arguments will revert to the latest saved version of the current file. To discard
unwanted changes - add '!' | `:e!`

`earlier 2m` - vim will go to the file 2 minutes ago

`@:` - repeat last command-line [count] times (useful with switching buffers)


# Navigation

## Buffers

`:bp/:bn` - next/prev buffer

jump between current and prev buffer (in VIM - `C-^`)

`:bd!` - forsibly remove buffer from buffer list


# Advanced movement

**vertical movement:**

`{number}|` - move to a certain column

`zL/zH` - move the view on the text half a screenwidth to the right/left

`g[hjkl]` - goes thrue the **visual** lines (only if line wrapping is on)

`ctrl+( or )` -> move to the beginning / end of sentence

`ctrl+{ or }` -> move to the beginning / end of paragraphs

> More: see :h motion.txt


# Keeping Coding Syntax

VIM, to fix indentation in file (spaces to tabs):

`:set noexpandtab`

`:retab!` // can be used also on visual block

`:set expandtab` // convert tabs back to spaces

if u move to the beginning of a file and press eigher <, > or =, the effect will be applied to  whole file

two times '=' -> properly indent

**Properly reindent the whole document**:

- `gg` - go to the top of the document
- `=` - enter to the indentation mode and await of modifier
- `G` - go to the bottom of document

`<` / `>` + `%` - indend / de-indent respectively code block


# Vim folding commands

**Essential folding commands**

- `zi` - switch folding on or off
- `za` - toggle a fold at the cursor.
- `zA` - recursively open/close current fold
- `zo` - opens a fold at the cursor.
- `zO` - opens all folds at the cursor.
- `zc` - closes a fold under cursor.
- `zC` - recursively close current fold
- `zr` - decreases the foldlevel by one.
- `zR` - decreases the foldlevel to zero - all folds will be open.
- `zm` - increases the foldlevel by one.
- `zM` - closes all open folds.
- `zv` - expand folds to reveal the cursor

**Navigating the unfolded document**

- `zj` - moves the cursor to the next fold.
- `zk` - moves the cursor to the previous fold.

**Ones that i can't get to work**

- `zf#j` - creates a fold from the cursor down # lines.
- `zf/` - string creates a fold from the cursor to string .
- `zd` - deletes the fold at the cursor.
- `zE` - deletes all folds.
- `[z` - move to start of open fold.
- `]z` - move to end of open fold.


# Sessions

`:mksession ~/mysession.vim`

`:source ~/mysession.vim` - load this session

`$ vim -S ~/mysession.vim` - or open vim with the -S option:


# Additional info

`CTRL-G` - show your location in the file and the file status.

`g?` - rotates selected text by 13 characters (bu, h npghnyyl gevrq vg..)
`set showbreak=_` - make long lines more readable

`:help usr_11.txt` - **recovering from a crash**

**operating on search matches using 'gn'**:

`gn` - Search forward for the last used search pattern, like with n, and start Visual mode to select the
match. If the cursor is on the match, visually selects it. If an operator is pending, operates on the
match. (_`cgn` - del next occurance of the match and enter insert mode_)

`C-^` - go to alternate (prev) file

`C-w C-^` - split window horizontally and go to alternate file

`:set paste` - enable paste mode (useful when pasting from system clipboard)

`C-l` - redraw screen (in case some usage of external command produced an error message and messed up screen)

`g C-g` - vim will count words in current files and display it
