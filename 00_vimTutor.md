## Sources

[derekwyatt.org](http://derekwyatt.org/vim/tutorials/index.html)
[vimcasts](http://vimcasts.org/episodes/archive/)



[basics](http://derekwyatt.org/vim/tutorials/novice/)

text objects:
    w - words
    s - sentences
    p - paragraphs
    t - tags


## Plugins

Installed [**Vundle**](https://github.com/VundleVim/Vundle.vim 'see docs') 
Installed [Nerdtree](https://github.com/scrooloose/nerdtree)
Installed [ctrlp.vim](https://github.com/ctrlpvim/ctrlp.vim)
Installed [fugitive](https://github.com/tpope/vim-fugitive)
Installed [syntastic](https://github.com/vim-syntastic/syntastic)


## Copy / paste regs

vim has 35 copy buffers

:reg -> view the contents of registers

**<C-r> in INSERT mode puts user in " mode (being able to paste from any register)**

> and this also words in vim command line

<C-r><C-o> - inserts literally from current default buffer (useful when repeating with '.' command)

1-9 -- history registers (delete registers)
0 -- the **yank** register
a-z -- named registers
A-Z -- same as (a-z) but append

Example: you copied something in 'a' register, now if you copy something in 'A' register it will apend to what is already copied.

"/ -- current search pattern
"- -- small delete


### Expression register

"= -- expression register
> [useful demo how to use it](http://vimcasts.org/episodes/simple-calculations-with-vims-expression-register/)

[evaluating scripts with vim's expression register](http://vimcasts.org/episodes/evaluating-scripts-with-vims-expression-register/)

Example:
	In 'INSTERT' mode `ctrl+r + =` and there some mathematical expression + `Enter`
	will paste the result of this expression

---

"_ -- the black hole register (_) -- deleting in this register actually **deletes**

**Read-only registers**

": - last :command
". - last inserted text
"% - filename of the current buffer
"# - filename of the alternate file
:h registers

`q{reg_name}q` - clear given register

`:global/{pattern}/{command} A -- :global/TODO/yank A - will yank all
lines containing 'TODO' word into reg. A

:set paste -- enable paste mode (useful when pasting from system clipboard)


## The substitute command

`:s/old/new/g` - substitute 'new' for 'old' on current **line**
`:%s/old/new/g` - to change every occurrence in the **whole file**
`:%s/old/new/gc` - find every occurrence in the whole file, with a prompt whether to substitute or not.

change every occurrence of a character string between two lines:
`:#,#s/old/new/g` - #,# are the line numbers of the range of lines where the substitution is to be done.

:nohl -> to disable highlighting of search instances --


## Line duplication

`:{column_number}y[ank]` -- yanks given line without moving the cursor

`:{yank_line_number}copy{paste_line_number}` - copy from line 9 after line 16

> command 'copy' has shortcut - `t`, so the command can be written: `9t16` for example

`.` - shortcut for number of line cursor is positioned at atm

so the example above can be reduced to `9t.`, which is `:[range]copy {address}`


------------------------


## Windows

http://vimcasts.org/episodes/working-with-windows/

`C-w s` | :sp[lit] - horizontal split
`C-w v` | :vs[plit] - vertical split

`C-w c` | :close - close window

`C-w hjkl` - switch between windows
`C-w HJKL` - reposition windows

`C-w o` - focus window (make cur. window the only visible)
`Ctrl+W >/<` : increase/decrease width (ex. 30<C-w><)
`Ctrl+W =` : equalize width and height of all windows

> See also: :help CTRL-W


## Tabs

http://vimcasts.org/episodes/working-with-tabs/

:tabnew -> creates a new tab (inside new tab is buffer, so it's possible to open a new file in it -- :e filename

:tabp -> 'tab previous' - go to the previous tab
:tabn -> 'tab next' - go to the next tab


## Changelist & Jumplist

The changelist remembers the position of every change that can be undone. You can move back and forwards through the changelist using the commands:

`g;` / `g,`

`:changes` -- view the contents of the changelist


jumplist - remembering each position to which the cursor jumped, rather than scrolled

move backwards and forwards through the jumplist with the commands:

`ctrl-O` / `ctrl-I`

`:jumps` -- view the contents of the jumplist

> When you are browsing Vim’s documentation, you can follow the link
> under the cursor with the command: `ctrl-]`


## Buffers

:bp/:bn - next/prev buffer

jump between current and prev buffer (in VIM - `C-^)

`:bd!` - forsibly remove buffer from buffer list

## Hard wrapping text

`gq{motion}` - format a section of text (ie `gqip` applies formatting to the current paragraph). And after formatting cursor will be on the last line of the paragraph

`gw{motion}` - same, but the cursor will remain on the word it was on

how hard wrapping behaves depends on _textwidth_ and _wrapmargin_
values, see more about them
[here](http://vimcasts.org/episodes/hard-wrapping-text/)

:set fo[rmatoptions]+=ta


## Marking

m + {marking letter} -> mark some place in file with specified letter, to find it faster
' + {marking letter} -> go to the marked with this letter


## Keeping Coding Syntax

if move to the beginning of a file and press eigher <, > or =, the effect will be applied to  whole file

two times '=' -> properly indent

**Properly reindent the whole document**:

gg - go to the top of the document
= - enter to the indentation mode and await of modifier
G - go to the bottom of document

<|> + % -- indend or de-indent code block


## Vim folding commands

**Essential folding commands**

`zi` - switch folding on or off
`za` - toggle a fold at the cursor.
`zA` - recursively open/close current fold
`zo` - opens a fold at the cursor.
`zO` - opens all folds at the cursor.
`zc` - closes a fold under cursor.
`zC` - recursively close current fold
`zr` - decreases the foldlevel by one.
`zR` - decreases the foldlevel to zero -- all folds will be open.
`zm` - increases the foldlevel by one.
`zM` - closes all open folds.
`zv` - expand folds to reveal the cursor

**Navigating the unfolded document**

`zj` - moves the cursor to the next fold.
`zk` - moves the cursor to the previous fold.

**Ones that i can't get to work**

`zf#j` - creates a fold from the cursor down # lines.
`zf/` - string creates a fold from the cursor to string .
`zd` - deletes the fold at the cursor.
`zE` - deletes all folds.
`[z` - move to start of open fold.
`]z` - move to end of open fold.


## Sessions

`:mksession ~/mysession.vim`
`:source ~/mysession.vim` - load this session
`$ vim -S ~/mysession.vim` - or open vim with the -S option:


Additional info
----

`U` - undo all the changes on a line

`CTRL-G` - show your location in the file and the file status.

Type  :! followed by an external command to execute that command

visual mode (`v`) -- select text -- enter command mode (`:`) (:'<,'>w) will
appear - 'w {filename} -- save selected text to file {filename}

:r FILENAME  retrieves disk file FILENAME and puts it below the
  cursor position.

:r !dir  reads the output of the dir command and puts it below the
  cursor position.

Typing ":set xxx" sets the option "xxx".  Some options are:
- 'ic' 'ignorecase'	ignore upper/lower case when searching
- 'is' 'incsearch'	show partial matches for a search phrase
- 'hls' 'hlsearch'	highlight all matching phrases
> You can either use the long or the short option name.

You can find help on just about any subject, by giving an argument to the
":help" command.  Try these (don't forget pressing <ENTER>):

- :help w
- :help CTRL-D
- :help insert-index
- :help user-manual

When typing a  :  command
- `CTRL-D` - see possible completions.
- `<TAB>` - use one completion.

---

`g?` - rotates selected text by 13 characters (fbzr grkg gb cenpgvfr)

`ctrl+v` --> select block --> by moving with `w` or `e` you can select
words, and by pressing `o` you reverse the side from which you are
selecting

`:!sort` - sorts selected lines

---

`:source $MYVIMRC` -- applyes changes to _.vimrc_ without reloading vim

**Next character**

{number}|:to a certain column
zL - move the view on the text half a screenwidth to the right
zH - opposite

`g[hjkl]` -- goes thrue the **visual** lines (only if line wrapping is on)
ctrl+( or ) -> move to the beginning / end of sentence
ctrl+{ or } -> move to the beginning / end of paragraphs

> More: see :h motion.txt


`:edit` called with no arguments will revert to the latest saved
version of the current file. To discard unwanted changes - add
trailing ‘!’ bang.


:earlier 2m -> vim will go to the file 2 minutes ago

there is also useful thing as macros -- search in internet how to use it (pretty ez)

`set showbreak=_` - make long lines more readable


**Antipatterns**

A less efficient way of doing something that becomes a bad habit:
	- ddO instead of **S**
	- f<lvt>U instead of **gUit** (???)


`:e!` - restore original file


in visual block (`C+v`) pressing `o` toggles cursor to opposite corner

after editing anything in VIM, it marks first and last point of edited
text with `[` and `]` marks respectively, so if you cut some
paragraph, you can jump then to the beginning of changed place in the
file by `'[`


`qall` - quit all files

`@:` - repeat last command-line [count] times (useful with switching buffers)


### Compare two files / buffers

[using vimdiff / diffthis](http://vimcasts.org/episodes/comparing-buffers-with-vimdiff/)


### Operating on search matches using 'gn'

`gn` - Search forward for the last used search pattern, like with n,
and start Visual mode to select the match. If the cursor is on the
match, visually selects it. If an operator is pending, operates on the
match. (_`cgn` - del next occurance of the match and enter insert mode_)

> `gUgn` - upcase next search match
