# Sources

> When you are browsing Vim’s documentation, you can follow the link
> under the cursor with the command: `ctrl-]`

Now go [here](http://derekwyatt.org/vim/tutorials/index.html) and go through all tutors from top to bottom,

And as additional info watch some [vimcasts](http://vimcasts.org/episodes/archive/)

sequence of sections below taken from 'user_manual' and changed a bit, so you can access
'user_manual' '30.1' for instance by typing `:help 30.1`

# simple searches (03.8) and regexp

`/` also supports offset after it (`/search_query/offset`)

- `/somethingu/±2` - position cursor 2 lines below match

> If the offset begins with 'b[egin]/s[tart]/e[nd]' and a number, the cursor moves to the beginning
> / end of the pattern, and then travels the “number” of characters. If the number is positive, the
> cursor moves forward, if negative, backward.

> to specify offset for reverse search use `?search?offset` syntax

`:set {options}` - set options for search

**ignoring case**:

- 'ic' (ignorecase) - ignore upper/lower case when searching
- 'nic' (noignorecase) - ignore upper/lower case when searching

**highlight search**:

- 'hls' (hlsearch) - highlight all matching phrases
- 'nhls' (nohlsearch) - disable highlight of all matching phrases

`:nohl` -> to disable highlighting of search instances -

**tuning search**:

- 'is' (incsearch) - show partial matches for a search phrase
- 'nowrapscan' - stops search at the end/start of file. (on by default)

## regular expressions

on those read 03 file in this repo

# Copy / paste

## Registers

vim has **35** copy buffers

- 1-9 - history registers (delete registers)
- 0 - the **yank** register
- a-z - named registers
- A-Z - same as (a-z) but append
  - _Example_: you copied something in 'a' register, now if you copy something in 'A' register it will apend to
    what is already copied.
- "_ - the black hole register (_) - deleting in this register actually **deletes**
- "\* - system clipboard register

`:reg` -> view the contents of registers

**`C-r` in INSERT mode puts user in " mode (being able to paste from any register)**

- `C-r C-o reg `- insert from a register _without_ autoindent
- `C-r C-p reg` - insert from a register with Vim doing 'the right thing'

> and the thing above also works in vim command line

`C-r C-o` - inserts literally from current default buffer (useful when repeating with '.' command)

**Read-only registers**

- "- - small delete
- ". - last inserted text
- "% - filename of the current buffer
- "/ - current search pattern
- ": - last :command
- "# - filename of the alternate file

> :h registers

`q{reg_name}q` - clear given register (tho don't forget bout black hole register)

## Expression register

"= - expression register

> [how to use it](http://vimcasts.org/episodes/simple-calculations-with-vims-expression-register/)

_Example_:

`C-r =` in insert mode, put there some mathematical expression -> `CR` will paste the result of this
expression

# using marks (3.10) + change/jump-list

\`\` / `''` - jump to previous position (will jump back if u use it again) (not same as `C-o`, but similar)

`m + {mark}` - mark some place in file with specified letter, to find it faster

`' + {mark}` - go to the marked with this letter

special marks (`:marks`):

- `'` - cursor position before doin a jump
- `"` - cursor position when last editin file
- `[` / `]` - start / eng or the last change

**jumplist** - remembering each position to which the cursor jumped, rather than scrolled

- `C-o` / `C-i` - move backward / forward through the jumplist
- `:jumps` - view the contents of the jumplist. Entry which u used last is marked as `>`

**changelist** - remembers the position of every change that can be undone.

- `g;` / `g,` - move back and forwards through the changelist
- `:changes` - view the contents of the changelist

# visual mode (04.4)

`ctrl+v` -> start selecting rectangular block

`gv` - select previously selected text after performin any operation on it (**26.1**)

When using blockwise selection, `o` takes u to 1 of the other corners, diagonally, `O` moves to the other
corner in the same line.

# set your settings (.vimrc) (usr_05.txt)

basic .vimrc setup taken and modified from https://github.com/amix/vimrc/blob/master/vimrcs/basic.vim

`CR` (carriage return) = `enter` (`:help key-notation`)

`:source $MYVIMRC` - applyes changes to _.vimrc_ without reloading vim

also look up **usr_40.txt (make new commands)**, which contains _key mapping_, defining command-line commands
and autocommands

> `:map` will list u all current mappings

**adding a plugin (05.6):**

these are all plugins i've installed for couple weeks of using vim:

- [**Vundle**](https://github.com/VundleVim/Vundle.vim "see docs")
  - to install added plugins - `:PluginInstall`
  - to update installed pluigns - `:PluginUpdate`
  - [usage docs](https://github.com/VundleVim/Vundle.vim/blob/v0.10.2/doc/vundle.txt#L234-L254)
- [Nerdtree](https://github.com/scrooloose/nerdtree)
- [ctrlp.vim](https://github.com/ctrlpvim/ctrlp.vim)
- [fugitive](https://github.com/tpope/vim-fugitive)
- [syntastic](https://github.com/vim-syntastic/syntastic)

# navigation -> windows, tabs (usr_08.txt) + buffers

## windows

http://vimcasts.org/episodes/working-with-windows/

- `C-w s` (`:count sp[lit] [+command] [file]`) - horizontal split
- `C-w v` (`:count vs[plit] [+command] [file]`) - vertical split
- `C-w c` (`:close`) - close window
- `C-w o` (`:only`) - focus window (make cur. window the only visible)
- `C-w hjkl` - switch between windows
- `C-w H|J|K|L` - move (swap) windows (08.5)
- `C-w >/<` - increase/decrease width (ex. 30<C-w><)
- `C-w =` - equalize width and height of all windows
- `{height}C-w _` - set window height to a apecified number of lines

**Commands for all windows (08.6):**

- `[q|w|qw]all[!]` - close/save/save'n'close all windows and quit vim
- `vim -[o|O] one.txt two.txt` - open vim with a window splitted horizontally/vertically for each arg

## buffers

- `:bp/:bn` - next/prev buffer
- `C-^` - jump between current and prev buffer
- `:bd!` - forsibly remove buffer from buffer list

## tabs (08.9)

http://vimcasts.org/episodes/working-with-tabs/

- `:tabedit {filename}` - create new tab page with given file
- `gt/T` - go to next/prev tab
- `:tab split` - creates new tab with current file
- `:tabn[ew]` -> creates a new tab (inside new tab is buffer, so it's possible to open a new file in it - :e
  filename
- `:tabo[nly]` - close all tabs except current one
- `:tabp[rev]`/`:tabn[ext]` -> go to the prev/next tab

# viewing differences with vimdiff (08.7)

`vimdiff main.c~ main.c`

`vertical diff[split|patch] [[file|patch]name]` - open vertical diffsplit

> `vertical diffpatch main.c.diff` - open vertical diffwindow with patch file

`[c` \ `]c` - jump between changes (if u've disabled changes)

`dp` / `do` (diff put/obtain) - remove difference (use from left/right windows)

[using vimdiff / diffthis](http://vimcasts.org/episodes/comparing-buffers-with-vimdiff/)

> See also: :help CTRL-W & :help vimdiff

# making big changes (usr_10.txt)

## record and playback commands (10.1)

`q{register}` - start writing macros into given register
`[count]@{register}` - use macros from given register

**editing macros (instead of recording again):**

- `"{register}p` - paste macros
- change commands that were wrong
- yank the corrected commands back into register and use again

## substitution (10.2)

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

## command ranges (10.3)

`:#,#s/old/new/g` - #,# are line numbers to which any ':' command can be applyed (single number can be used
to address 1 specific line)

`.` / `$` - is the shortcut for current/last line address

**line duplication (sample)**

- `:{range/line_number}y[ank]` - yanks given line without moving the cursor
- `:{range/line_number}copy{address}` - copy line(s) and paste to given (address) line

> command 'copy' has shortcut - `t` | _9t._, _.t$_

**using a pattern in a {range}:**

- `:?^Chapter?,/^Chapter/s=grey=gray=g` - first `?^Chapter?` finds line above cur. position, that matches, next
- `/^Chapter/` finds line below cur. position, adds 2 more lines and replaces 'grey' for 'gray' between those
  lines

**adding count manually:**

- `:.+3,$-5s/old/new/g` - substract from current line + 3 lines to last line - 5 lines

_Example:_ `.,.+4..` - when u know how many lines to operate on..

**using marks:**

- `:'t,'b..` - substract between those marks

> right here in this tutorial, instead of words 'Example' above and below i had words 'Sample', so i decided
> to practice a bit and replaced it with command: `?Sample?-1,/Sample/+1s=sample=Example`, which worked
> perfectly, feel like VIM-superman ^^

**visual modes and ranges:**

select text --> press ':' --> `:'<,'>` will appear ('< and '> are marks, placed at the start and end of the
visual selection) --> any ':' command will be now applyed to this selected text

_Example:_

select text -> `:` -> `:'<,'>w {filename}` - save selected text to file
{filename}

## the global command (10.4)

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

## reading and writing part of a file (10.6)

`:[range]r[ead] {filename}` - paste {filename} contents in current file in [range] | _:$r patch_ - put 'patch'
file contents at the end of cur. file

`:[range]w[rite] {filename}` - write a **[range]** of lines from cur. file into {filename}; use `w!` to
override existing files; use `w >>{filename}` to append to a file

## formatting text (10.7)

`:set textwidth=100` - make lines automatically trim when typing at 100 symbols

`gq{motion}` - format a section of text (ie `gqip` applies formatting to the current paragraph). And after
formatting cursor will be on the last line of the paragraph

`gw{motion}` - same, but the cursor will remain on the word it was on

how hard wrapping behaves depends on _textwidth_ and _wrapmargin_ values, see more about them
[here](http://vimcasts.org/episodes/hard-wrapping-text/)

`:set fo[rmatoptions]+=ta`

## changing case (10.8)

`g{action}{motion}` - perform {action} in {motion} (ik, ima pro at explaining ^^)

To make operator work on lines - double it. ('gUgU' == 'gUU')

_Examples_:

- `gUw` - uppercase next word
- `gUU` (shortcut from 'gUgU') - uppercase whole line
- `g~gn` - switch case on next search match

# typing command-line commands quickly (usr_20.txt)

**command line completion (20.3):**

- `TAB` completion is contextual, rotate between suggestions with `TAB`
- `C-d` - see list of possible completions
- `C-l` - complete word to the longest unambiguous string

**command line window (20.5):**

- `q:` - open small command line window at the bottom of the screen, type and execute commands there

# go away and come back (usr_21.txt)

**suspend and resume (21.1):**

- `C-z` - suspend and go back to shell
- `fg` (from shell) - go back to vim session

**Executing shell commands (21.2) (pipe command):**

- `! {bash_command}` - run external command (`!sort` - sorts selected lines)
- or just start shell `:shell`

> can be performed on a region
> ! command always works on lines even if you are in character visual mode or visual block mode.

**remembering information - viminfo (21.3)** - after u quit vim 'viminfo' contains your history, marks and
such..

**getting back to where u stopped vim:**

`'0` - `'9` - when quitting vim it places mark '0' where u were, each time u quit vim mark '0' becomes mark
'1' and so on.. Mark '9' is lost

**sessions(21.4)** contain all info 'bout what u r editing, file list, window layout, global vars, options and
such..

- `:mksession mysession.vim` (add `!` to override session with same name or if u r rewriting cur. 1)
- `:source mysession.vim` - load this session
- `$ vim -S mysession.vim` - open vim and restore specific session

**views(21.5)** store properties for one window only, not of the whole Vim, like sessions

- `mkview 1`
- `loadview 1`

u can store up to 10 views for the same file, 1 unnumbered and nine numbered from 0 to 9

- `mkview ~/.vim/main.vim` - save view of cur. file
- `source ~/.vim/main.vim` - restore it

# inserting quickly (usr_24.txt)

**making corrections (in insert mode) (24.1):**

- `C-w` - same as `C-BS`
- `C-u` - same as `C-Shift-BS`

also look up **completion (24.3)**

`C-a` (in insert mode) - **insert text u typed last time u were in insert mode (24.4)**

**copying from another line (24.5):**

- `C-@` - does `C-a` and then exits insert mode
- `C-y` / `C-e` - insert char above/below cursor

- `C-v {char/digits}` - enter special char (like 'ESC') literally (**24.8**)

# digraphs (24.9)

some chars aint on the keyboard (like copyright char ℅), so to type them use digraphs:

`C-k {digraph}`

`:digraphs` - show u all possible ones

`:digraph {sequence} {digraph}` - define your own digraph

# editing formatted text (usr_25.txt) & keeping Coding Syntax

`:{range}left/center/right [width/margin]` - accordingly align range of lines in {range} | _:1,5center 40_

`:packadd justify` (or in .vimrc `packadd! justify`) - add new visual command `_j`, using which u will justify
selected text (or u can filter text through an external program

**indents and tabs (25.3):**

to fix messed up (like 3-spaced tabs) in cur. file:

- `:set tabstop=3` -> `:retab 8`

to fix indentation in file (spaces to tabs):

- `:set noexpandtab`
- `:retab!` // can be used also on visual block
- `:set expandtab` // convert tabs back to spaces

if u move to the beginning of a file and press eigher <, > or =, the effect will be applied to whole file

two times '=' -> properly indent

> `=i{` - indent text within the scope (or `vi{` ..)

**Properly reindent the whole document**:

- `gg` - go to the top of the document
- `=` - enter to the indentation mode and await of modifier
- `G` - go to the bottom of document

`<` / `>` + `%` - indend / de-indent respectively code block

## advanced movement, dealing with long lines (25.4)

**vertical movement:**

- `zl`/`zh` - scroll left/right
- `zL`/`zH` - scroll half a window width left/right
- `zs`/`ze` - scroll left/right to put cursor at the start/end
- `{number}|` - move to a certain column

`C-b/u/y / d/e/f` - scroll full screen / half screen / one line UP / DOWN

`C-` - scroll full screen / half screen / one line DOWN

`g[hjkl]` - goes thrue the **visual** lines (only if line wrapping is on)

`ctrl+( or )` -> move to the beginning / end of sentence

`ctrl+{ or }` -> move to the beginning / end of paragraphs

> More: see :h motion.txt

# folding (usr_28.txt)

**manual folding (28.2):**

- `zf{motion}` - **create** manual fold | _zfap - fold a paragraph_
- `zo` - open fold at cursor
- `zc` - close menually created fold again (and not only manually)
- `zr`/`zm` - decreases/increases the foldlevel by one.
- `zR`/`zM` - open/close all folds
- `zi` - switch folding on or off
- `za` - toggle a fold at the cursor.
- `zA` - recursively toggle current fold
- `zv` - expand folds to reveal the cursor

> use `:mkview` and `:loadview` to save and restore folds in file

**Navigating the unfolded document**

- `zj` - moves the cursor to the next fold.
- `zk` - moves the cursor to the previous fold.

**Ones that i can't get to work**

- `zd` - deletes the fold at the cursor.
- `zE` - deletes all folds.
- `[z` - move to start of open fold.
- `]z` - move to end of open fold.

**folding unchanged lines (29.9):**
`:setlocal diff foldmethod=diff scrollbind nowrap foldlevel=1` - usefil when u set 'diff' option in the same
window. `vimdiff` command does this for ya

# moving through programs (usr_29.txt)

`gd/D` - searches for the local/global declaration of the variable under the cursor

**moving in code blocks (29.3):**

all commands below are meant to be done in some huge funcs, that r enclosed in {} with lots of nested stuff:

- `[[`/`][` - move to start/end of outer block
- `[{`/`]}` - move to the start/end of current block
  - `[(`/`])` - work similar, except they work on '()' pairs, instead of '{}'
- `[]`/`]]` - move to the end/start of prev/next function
- `[/`/`]/` and `[* / ]*` - move to start/end of a comment block (only works for /_ - _/ comments)

**formatting comments (30.6):** position cursor at comment start -> `gq]/`

# undo tree (usr_32.txt)

`:earlyer/later [count]f[ile]/time` - undo/redo up ot a file write (time argument as '1s', '1m', '2d'..)

`:undolist` - see what branches there r in undo tree (number/changes/time)

`:undo [count]` - jump to change '2' in change tree

`g-/+` - move back/forward in time, goes to the change made before/after

> if u want even more details 'bout undto tree, use `:echo undotree()`

---

# Additional info

`ga` - prints the number of the character under the cursor

`g?` - encrypt a block of text with the rot13 algorithm (rotates selected text by 13 characters)
(bu, h npghnyyl gevrq vg..)

`g??` - encrypts the current line

`C-p/n` (in insert mode) - searches backward for a word to complete

`set showbreak=_` - make long lines more readable

`:help usr_11.txt` - **recovering from a crash**

`:preserve` - This command writes all the edits to the swap file. The original file remains
unchanged and will not be changed until you do a :write or exit with ZZ . If the
system crashes, you can use the swap file to recover all your edits. Note that after a
:preserve , you can recover even if the original file is lost.Without this command, you
need both the original file and the swap file to recover.

**operating on search matches using 'gn'**:

`gn` - Search forward for the last used search pattern, like with n, and start Visual mode to select the
match. If the cursor is on the match, visually selects it. If an operator is pending, operates on the
match. (_`cgn` - del next occurance of the match and enter insert mode_)

`C-^` - go to alternate (prev) file

`C-w C-^` - split window horizontally and go to alternate file

`:set paste` - enable paste mode (useful when pasting from system clipboard)

`C-l` - redraw screen (in case some usage of external command produced an error message and messed up screen)

on line '#include "inits.h"' hover over file name and press `gf` - vim will try to find this file and open it
(22.3)

editin files in vim with encryption: `:help 23.3`

`C-o` in insert mode - quits insert mode, lets u execute 1 command and goes back into insert mode

Turning a paragraph into 1 line (if u want to import text into a program like MS-Word):

`:g/./,/^$/join` - find all lines that contain at least 1 char and join them until an empty line

`C-a` - increment number below cursor (26.2)

`e[dit]` called with no arguments will revert to the latest saved version of the current file. To discard
unwanted changes - add '!' | `:e!`

`@:` - repeat last command-line [count] times (useful with switching buffers)

**clever tricks (usr_12.txt):**

- `:%s/\<four\>/4/g` - replace 'four' to 4 filewide (not 'thirtyfour' or 'fourteen'), where `\<` means 'match
  the beginning of word and `/>` end of word (12.1)
- `K` - find the man page for word/func below the cursor (for more info look '12.6' section) (12.6)

- . - repeat the last simple change. Does not repeat a command-line command.

`$vim --help` - get all the possible flags for starting vim

## encryption

`$vim -x secret.md` - create encrypted file (vim will prompt you for a key used for encrypting and
decrypting the file)

`:X<RET>` - Switching Between Encrypted and Unencrypted Modes (will prompt the key)

> tho the swap file that will be created while editing the file won't be encrypted, to avoid
> creation of a swap file start vim with `-n` flag, which will store file in memory instead of swap
> file

## where am i in detail

`C-g` - show your location in the file and the file status.

`1C-g` - command gives you the full path of the file

`2C-g` - .. lists a buffer number as well.

`g C-g` - displays the current byte number of a file (along with the current line, column, and
other information)
