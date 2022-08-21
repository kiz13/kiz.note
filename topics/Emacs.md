# *

GNU Emacs /ˈiːmæks/ (Editor MACroS)

META key -- ALT

`C-v` forward one window
`M-v` backward one window
`C-l` center screen on current line

previous (line), next (line), backward (one letter), forward (one letter):

```txt
    C-p
C-b     C-f
    C-n
```

`M-f` (forward one word)
`M-b` (backward one word)

`C-a` (moves cursor to beginning of line of text) `C-e` (...), try press `M-a` or `M-e` repeatably to see the differences with ...

If Emacs stops responding the command, you can use `C-g` to safely terminate the command

`C-d` delete one letter after the caveat
`M-d` delete one word after ...
`C-k` (kill to line end) **移除**从光标到行尾间的字符
`C-y` (yank, 召回最近一次**移除**的内容)

exit Emacs: `C-x c`

`C-h` help command; `C-h i` will bring up the info directory, `C-h m` for mode help page

`u` go up
`l` go to the last page you were on

`C-s` search; then repeat search forward with `C-s` and repeat search backward with `C-r`

fundamental buffer mode - vanilla text editing buffer

If the buffer name is surrounded by asterisks, it means this buffer is not tied to a file on the disk, it's a temporary buffer.

... tab completion

`C-x k` close the buffer in this window

`C-x o` switch to the other window

`M-x` running commands by name

[Within Emacs, `~` at the beginning of a file name is expanded to your HOME directory, so you can always find your `.emacs` file with `C-x C-f ~/.emacs`.](https://superuser.com/a/138127/1233932)

`C-x f` with a directory name directs to Emacs's directory editor mode; `d` mark a file for deletion and then `x` (execute) to actually delete it

`C-x f` make new buffer and read file (create a new one if not exists)

`+` create a new directory

`C-x s` save current buffer

`g` refresh the contents of the buffer

copy file with `shift c` and choose a new name

`m` mark file
`u` un-mark file

## others

hatred towards parenthesis

`M-x org-mode` will enable the Org mode on the current document.

Unordered lists start with `-`,`+`,or `\*`. Ordered lists start with a number and a dot. Descriptions use `::`

[switch buffer ?](https://emacs.stackexchange.com/questions/728/how-do-i-switch-buffers-quickly)
[check](https://www.cs.colorado.edu/~main/cs1300/lab/emacs.html)

## [other key bindings](https://caiorss.github.io/Emacs-Elisp-Programming/Keybindings.html)

`M->` move to the end of buffer
`M->` move to the start of buffer
`M-g g` jump to line (command palette)
`M-g n` jump to next error
`M-g p` jump to previous error

`C-o` open-line
`C-j` (`C-m`) enter
`C-x h` select all
`C-x u` (`C-/`) undo
`C-Space` begin selection
`M-w` copy
`C-w` cut
