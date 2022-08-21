# *

> In terminal, running `vim` starts a mode called "normal mode". In order to get typing press `i`. When you are done, press `esc` backing to normal mode.

## [vim cheatsheet](https://github.com/hackjutsu/vim-cheatsheet)

`:sp` `0` `$` `dd` `y` `p` `/` `u` `Ctrl r` `gg` `G` `zz`

### cursor movement

- h, j, k, l (left, down, up, right)
- `H`, `M`, `L` (to top of screen, to middle of screen, to bottom of screen)
- `w`, `e` (jump forwards to the start/end of a word), `W`, `E` (words can contains punctuation); `b` (jump backwards to the start of a word), `B` (...)
- `0` jump to the start of the line, `^` jump to the first non-blank character of the line, `$` jump to the end of the line, `g_` jump to the last non-blank character of the line
- `gg` go to the first line of the document, `G` go to the last line of the document, `4G` go to line 4
- `fx` jump to the next occurrence of character `x`, `tx` jump to before next occurrence of character `x`
- `}` jump to next paragraph (or function/block, when editing code), `{`
- `zz` center cursor on screen
- `Ctrl b` move back one full screen, `Ctrl f` forward one full screen, `Ctrl d` forward 1/2 a screen, `Ctrl u` back 1/2 a screen

### insert mode (inserting/appending text)

- `i` insert before the cursor, `I` insert at the beginning of the line
- `a` insert (append) after the cursor, `A` insert at the end of the line
- `o` append (open) a new line below the current line, `O` ... above ...
- `ea` insert (append) at the end of the word
- `Esc` exit insert mode

### Editing

- `r` replace a single character
- `J` join line below to the current one
- `cc` change (replace) entire line, `cw` change (replace) to the start of the next word, `ce` change (replace) to the end of the next word, `cb` change (replace) to the start of the previous word
- `c0` change (replace) to the start of the line, `c$` ... end ...
- `s` delete character and substitute text, `S` delete line and substitute text (same as `cc`)
- `xp` transpose two letters (delete and paste)
- `.` repeat last command
- `u` undo
- `Ctrl r` redo

### marking text (visual mode)

- `v` start visual mode, mark lines, then do a command (line y-yank), `V` start linewise visual mode
- `o` move to other end of marked area, `O` move to other corner of block
- ~~`aw` mark a word, `ab` a block with (), `aB` a block with {}, `ib` inner block with (), `iB` inner block with {}~~
- `Esc` exit visual mode

### visual commands

- `>` shift text right, `<` shift text left
- `y` yank (copy) marked text
- `d` delete marked text
- `~` switch case

### cut and paste

- `yy` yank (copy) a line, `13yy` yank (copy) 13 lines
- `yw` yank (copy) the characters of the word from the cursor position to the start of the next word
- `y$` yank (copy) to the end of line
- `p` put (paste) the clipboard after cursor, `P` ... before ...
- `dd` delete (cut) a line, `13dd` delete (cut) 13 lines
- `dw` delete (cut) the characters of the word from the cursor position to the end of the next word
- `D` delete (cut) to the end of the line
- `d$` delete (cut) to the end of line
- `d^` delete (cut) to the first non-blank character of the line
- `d0` delete (cut) to the beginning of the line
- `x` delete (cut) character

### search and replace

- `/pattern` search for pattern
- `?pattern` search backward for pattern
- `\vpattern` 'very magic' pattern: non-alphanumeric are interpreted as special regex symbols (no escaping needed)
- `n` repeat search in same direction, `N` ... opposite ...
- `:%s/old/new/g` replace all old with new throughout file
- `:%s/old/new/gc` replace all old with new throughout file with confirmations
- ~~`noh` remove highlighting of search matches~~

#### search in multiple files

- `:vimgrep /pattern/ {file}` search for pattern in multiple files
- `:cn` jump to the next match, `:cp` jump to the previous match
- `:copen` open a window containing the list of matches

### exiting

- `:w` write (save) the file, but don't exit
- `:wq` or `:x` or `ZZ` write (save) and quit
- `:q` quit (fails if there are unsaved changes)
- `:q!` or `ZQ` quit and throw away unsaved changes

### working with multiple files

- `:e file` edit a file in a new buffer
- `:bnext` or `:bn` go to the next buffer, `:bprev` or `:bp` ... previous ...
- `:bd` delete a buffer (close a file)
- `:ls` list all open buffers
- `:sp file` open a file in a new buffer and split window, `:vsp file` ... vertically ...
- `Ctrl ws` split window, `Ctrl ww` switch windows, `Ctrl wq` quit a window, `Ctrl wv` split window vertically
- `Ctrl wh` move cursor to the left window (vertical split), `Ctrl wl` ... right ...
- `Ctrl wj` move cursor to the window below (horizontal split), `Ctrl wk` ... above ...

### tabs

- `:tabnew` or `:tabnew file` open a file in a new tab
- `gt` or `:tabnext` or `:tabn` move to the next tab, `gT` or `:tabprev` or `:tabp` ... previous ...
- `13gt` move to tab 13
- `:tabmove 13` move current tab to the 13th position (indexed from 0)
- `:tabclose` or `:tabc` close the current tab and all its windows
- `:tabonly` or `:tabo` close all tabs except for the current one
- `:tabdo command` run the command on all tabs (e.g., `:tabdo q` - closes all opened tabs)

### appendix

#### Search

Search for whole word: `\<` marks the beginning of a word, `\>` marks the end of a word; by moving the cursor to the word and pressing `*` to search forwards or `#` to search backwards.

Search history: to browse the search history, press `/` or `?` and use the arrow up/down keys to find a previous search operation. (**What if there are no arrow keys on the keyboard?**)

To ignore case type `:set ignorecase` or `:set ic`, to change back to case match mode, type `:set noignorecase` or `:set noic`

## others

[check](https://stackoverflow.com/questions/3385753/in-vim-how-can-i-shift-a-block-of-code-to-right)

- `4>>` will indent all four lines
- `>}` will indent all of the lines until the end of the paragraph (to the first empty line)
- `>ap` will indent all of the lines **a** **p**-aragraph, even if your cursor isn't on the first line.

[cursor previous location](https://vi.stackexchange.com/questions/2001/how-do-i-jump-to-the-location-of-my-last-edit) ``.`

[copy text from/to clipboard](https://stackoverflow.com/a/3961877/118440030) use the register `"+` (copy to the system clipboard) or `"*` (paste from the system clipboard), e.g., `"+y`, `"*p`

[find next](https://stackoverflow.com/questions/6607630/find-next-in-vim), after hitting the enter (when doing a search), `n` for next and `N` for previous; also `*` and `#` for a quick search

[vim shortcut](https://gist.github.com/awidegreen/3854277)

(surround selection on typing v google search) [for vim](https://stackoverflow.com/questions/2147875/what-vim-commands-can-be-used-to-quote-unquote-words)

---

**change file encoding**

convert file encoding, **write files in place**, [no need to enter vim](https://stackoverflow.com/questions/4544669/batch-convert-latin-1-files-to-utf-8-using-iconv#comment67371494_35329638)

```bash
vim "+set nomore" "+bufdo set fileencoding=utf8 | w" "+q" $(find . -type f)
```

or you want to enter vim:

```bash
vim $(find . -type f)

# in vim, go into command mode (:)
:set nomore
:bufdo set fileencoding=utf8 | w
```

see also [how does vim perform charset conversion](https://stackoverflow.com/questions/54571068/how-does-vim-perform-charset-conversion)

---

[change case of the selected text?](https://stackoverflow.com/questions/2946051/changing-case-in-vim), visual select the text, then <kbd>U</kbd> for uppercase, <kbd>u</kbd> for lowercase, <kbd>~</kbd> for swapping all casing

## end
