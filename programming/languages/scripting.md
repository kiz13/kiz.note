# *

A _scripting language_ is a language that avoids the usual `edit/compile/link/run` cycle by interpreting the program text at runtime. It has a number of advantages:

  - Rapid turnaround, encouraging experimentation
  - Changing the behavior of a running program
  - Enabling customization by program users

## ahk

- **AutoHotKey** is a free, open-source custom scripting language for Windows, initially aimed at providing easy keyboard shortcuts or hotkeys, fast macro-creation ...

[ahk identify different apps](https://stackoverflow.com/a/16558154/11844003)

[winactive](https://www.reddit.com/r/AutoHotkey/comments/b09l0z/if_winactive_vs_ifwinactive/)

[ahk class](https://stackoverflow.com/questions/45642727/what-is-ahk-class-how-can-i-use-it-for-window-matching)

## bash

### introduction

**Bash** is a _Unix shell_ (a command-line interpreter or shell that provides a CLI for Unix-like OS) and command language. [Wikipedia](https://en.wikipedia.org/wiki/Bash_(Unix_shell))

Bash has also been ported to Microsoft Windows and distributed with _Cygwin_ and _MinGW_

[Bash 4 switches its license to GPLv3](https://apple.stackexchange.com/questions/193411/update-bash-to-version-4-0-on-osx)

[to disable visual bell completely](https://stackoverflow.com/a/5933613/11844003), write `set t_vb=` to `~/.vimrc`

### command tools simple usage

[`tar` explained](https://www.cnblogs.com/end/archive/2011/04/20/2022614.html)

[unzip file use `unzip`](https://askubuntu.com/questions/86849/how-to-unzip-a-zip-file-from-the-terminal) if `unzip` isn't already installed, `sudo apt-get install unzip`

[没有当前所在的目录的写入权限时，需要更改（默认当前目录下）解压后的目标目录](https://www.cnblogs.com/redheat/p/7095893.html) `unzip /path/to/source.zip -d /path/to/dest`

`df [OPTION]... [FILE]...` show information about the file system on which each FILE resides, or all file systems by default.

`df –h [--human-readable] /`

### todo

- [ ] [search the bash history and rerun a command](https://superuser.com/questions/7414/how-can-i-search-the-bash-history-and-rerun-a-command)
- [ ] [move all files from subfolders to parent folder, in case there are files with same file name](https://askubuntu.com/questions/146634/shell-script-to-move-all-files-from-subfolders-to-parent-folder#comment1437214_146643)

## batch file and shell script

[check the differences](https://stackoverflow.com/questions/5079180/what-is-the-difference-between-batch-and-bash-files)

### windows batch

- [append text to .bat file](https://stackoverflow.com/a/5143293/11844003) use `>` to overwrite a file if it exists or create if it does not exist. Use `>>` to append to an existing file or create if it does not exist.
  - append a blank line to a file `echo.>>"C:\which folder\trace.log"`
  - append text to a file `echo some text>>"C:\which folder\trace.log"`
- [output every output from a .bat to a file?](https://stackoverflow.com/questions/27097666/batch-file-output-current-cmd-output-to-log) try `script >log.txt`
- [delete all subfolders with a specific name?](https://stackoverflow.com/questions/25554254/batch-command-to-delete-all-subfolders-with-a-specific-name)
- [robocopy maxage not working?](https://stackoverflow.com/questions/34729746/robocopy-minage-maxage-not-working) `/MAXAGE:n` maximum file age - exclude files older than n days/date. [Check a few examples](https://social.technet.microsoft.com/wiki/contents/articles/1073.robocopy-and-a-few-examples.aspx)
- [use xcopy with date option?](https://stackoverflow.com/a/44264014/11844003)
- [get current directory when a .bat file runs](https://stackoverflow.com/a/4420078/11844003)
  - `%cd%` refers to the current working directory (variable)
  - `%~dp0` refers to the full path to the batch file's directory (static)
  - `%~dpnx0` and `%~f0` both refer to the full path to the batch directory and file name (static)
- [list files (only file names) in directory?](https://stackoverflow.com/questions/23228983/batch-file-list-files-in-directory-only-filenames) `dir /b /a-d` for more info see `dir /?`
- [how can i debug a .bat script?](https://stackoverflow.com/questions/165938/how-can-i-debug-a-bat-script) `echo` just
- `errorlevel` stuff, the late *finding* part will return an %errorlevel% > 0 if not found
  - [check if a process is running?](https://stackoverflow.com/a/15449358/11844003) `tasklist /fi "imagename eq spotify.exe" | find ":" > nul`
  - [check if a named program is running](https://stackoverflow.com/a/62010014/11844003) `tasklist /FI "WindowTitle eq Postman" | findstr /B "INFO:" > nul` [friendly remind: the output is translated](https://stackoverflow.com/questions/15449034/batch-program-to-to-check-if-process-exists#comment52565708_15449358)
  - [check whether a port is available?](https://stackoverflow.com/a/10315609/11844003) `netstat -ano | findstr 6379`
- How do I create a Windows Batch file that does not show the Command Prompt when executed? You can't. Executing a batch file with the built-in Command Prompt is going to keep a window open until the batch file exits. What you can do is take steps to make sure that the batch file exits as quickly as possible. [source](https://superuser.com/a/236193/1233932)

### bash script

- [echo a blank?](https://stackoverflow.com/questions/37052899/what-is-the-preferred-method-to-echo-a-blank-line-in-a-shell-script) `echo` is preferred, `echo ""` is good but unnecessary
- [move files from subfolders to their parent directory?](https://stackoverflow.com/questions/40468979/how-to-move-files-from-subfolders-to-their-parent-directory-unix-terminal)
- [parsing json](https://stackoverflow.com/questions/1955505/parsing-json-with-unix-tools)
- [format date](https://stackoverflow.com/questions/1401482/yyyy-mm-dd-format-date-in-shell-script) `date '+%Y-%m-%d %H:%M:%S'`
- [convert string to date](https://stackoverflow.com/questions/11144408/convert-string-to-date-in-bash) `date -d 'date string' +'%Y-%m-%d'`, `date -d "$(date -d "${date}" +%Y-%m-%d) ${time}" +%s` <- wtf is this? (generated by copilot)
- check if a program exists

  ```shell
  if ! command -v <the_command> &> /dev/null
  then
      echo "<the_command> could not be found"
      exit
  fi
  ```

## end
