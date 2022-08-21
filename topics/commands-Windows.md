# command stuff

## equivalents

Equivalent [tree](http://mama.indstate.edu/users/ice/tree/) command on Windows? [There is a tree command in windows already, it is `tree.com`](https://superuser.com/a/1312725/1233932) N.B. use `//` within bash or bash would think it is a folder name
- `/a` for just folder
- `/f` for every single file

[Equivalent of `which`](https://stackoverflow.com/a/304447)
- use `where.exe` or `Set-Alias which where.exe`
- use `gcm` (`Get-Command`) with powershell

## how to

How create a log of every operation processed in a `.bat` file? Use `>` to overwrite a file if it exists or create if it does not exist. Use `>>` to append to an existing file or create if it does not exist. [credits](https://stackoverflow.com/a/5143293/11844003)
- append a blank line to a file `echo.>>"C:\which folder\trace.log"`
- append text to a file `echo some text>>"C:\which folder\trace.log"`

How to delete all subfolders with a specific name? [credits](https://stackoverflow.com/a/25554347)
- from command line:`FOR /d /r . %d IN (specifig-name) DO @IF EXIST "%d" rd /s /q "%d"`
- if used from batch file, escape the `%` char with another `%` char
- [how to use the damn for](https://ss64.com/nt/for.html)

How to get current directory from within `.bat` file? [credits](https://stackoverflow.com/a/4420078/11844003)
- `%cd%` refers to the current working directory (variable)
- `%~dp0` refers to the full path to the batch file's directory (static)
- `%~dpnx0` and `%~f0` both refer to the full path to the batch directory and file name (static)

How to list files (only file names) in directory? [`dir /b /a-d`](https://stackoverflow.com/a/23229008) (not for powershell)

How can i debug a `.bat` script? [Just use `echo`](https://stackoverflow.com/questions/165938/how-can-i-debug-a-bat-script)

How do I create a Windows Batch file that does not show the Command Prompt when executed? You can't. Executing a batch file with the built-in Command Prompt is going to keep a window open until the batch file exits. What you can do is take steps to make sure that the batch file exits as quickly as possible. [credits](https://superuser.com/a/236193/1233932)

How to check from `.bat` if a process is running? [credits](https://stackoverflow.com/a/15449358/11844003) the *finding* part will return an `errorlevel` equals 0 if found

```bat
@echo off
tasklist /fi "imagename eq spotify.exe" | findstr "spotify.exe" > nul
if %errorlevel% equ 0 taskkill /f /im "spotify.exe"
exit
```

How to check from `.bat` if a named program is running? [credits](https://stackoverflow.com/a/62010014/11844003) friendly remind: [the output is translated, so you better go with `findstr ":"`](https://stackoverflow.com/questions/15449034/batch-program-to-to-check-if-process-exists#comment52565708_15449358)

```bat
tasklist /FI "WindowTitle eq Postman" | findstr /B "INFO:" > nul
```

How to check whether a port is available? [credits](https://stackoverflow.com/a/10315609/11844003)

```bat
@echo off
netstat -ano | findstr 6379
@rem then still, check the ErrorLevel
```

## use case

[robocopy maxage not working?](https://stackoverflow.com/questions/34729746/robocopy-minage-maxage-not-working) `/MAXAGE:n` maximum file age - exclude files older than n days/date. [Check a few examples](https://social.technet.microsoft.com/wiki/contents/articles/1073.robocopy-and-a-few-examples.aspx)

[use xcopy with date option?](https://stackoverflow.com/a/44264014/11844003)
