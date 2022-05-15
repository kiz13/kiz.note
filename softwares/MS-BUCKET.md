# *

## OneDrive

- [ ] [2-byte character sh*t](https://onedrive.uservoice.com/forums/913516-onedrive-on-android/suggestions/37839025-can-t-display-unicode-text-such-as-chinese-or-japa)

If you remove the "Move to OneDrive" context menu, it will also remove all the context menu items below for when you right-click on an item inside the OneDrive folder.

## OneNote

the indents disappear when pasting text into onenote (text is copied from IDE) [here is an issue opened at vscode git repo](https://github.com/Microsoft/vscode/issues/35954)

## WSL

[home dir?](https://superuser.com/questions/1185033/what-is-the-home-directory-on-windows-subsystem-for-linux) `%LOCALAPPDATA%\Packages\CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc\LocalState\rootfs`

[reset password?](https://askubuntu.com/a/1171006/1097027)

1. log in to the Ubuntu with `wsl --user root`
2. change the password for the current user with `passwd` (or for another user with `passwd username`)
3. done

jetbrains [setup wsl development env](https://www.jetbrains.com/help/idea/how-to-use-wsl-development-environment-in-product.html#open-a-project-in-wsl)

`service crontab status` crontab doesn't run by default, so `service crontab start`

[crontab not working ?](https://stackoverflow.com/questions/41281112/crontab-not-working-with-bash-on-ubuntu-on-windows) `usermod -a -G crontab kiz`

[where is the ubuntu file system root directory?](https://askubuntu.com/questions/759880/where-is-the-ubuntu-file-system-root-directory-in-windows-subsystem-for-linux-an)

## Windows Terminal

[Windows terminal caret thickness](https://github.com/microsoft/terminal/issues/4335)

[Powershell Profiles配置文件的存放位置介绍](https://www.cnblogs.com/backpacker/p/4711823.html)

[customize-settings official site](https://docs.microsoft.com/en-us/windows/terminal/customize-settings/profile-appearance)

[usages with panes](https://docs.microsoft.com/en-us/windows/terminal/panes)

[git bash flickering](https://github.com/microsoft/terminal/issues/7308) this is caused by `set bell-style visible` in the default settings of Git (`%ProgramFiles%/Git/etc/inputrc`)

[only one part of unicode character get deleted on backspace in git bash](https://github.com/microsoft/terminal/issues/5057) change start command line from `bash.exe` to `bash.exe -li`

[beautify the powershell with _oh-my-posh_ -> some tokens are grey -> `Set-PSReadlineOption -TokenKind Operator -ForegroundColor Yellow` not working?](https://stackoverflow.com/questions/52309625/a-parameter-cannot-be-found-that-matches-parameter-name-tokenkind) `Set-PSReadLineOption -Colors @{Operator = "Yellow"; Parameter = "Yellow"}`

git bash icon file location: `${git-installation-directory}/mingw64/share/git/git-for-windows.ico`

this [pull request (merged)](https://github.com/microsoft/terminal/pull/1005) allows you to write comments in the configuration file which is of json format.

remove the powershell start text? [Add the `-nologo` option to the PowerShell command line](https://stackoverflow.com/a/63695674/11844003), then it starts the PowerShell console without displaying the copyright banner.

use `wt` command to start Windows Terminal from the command line, `wt -d .` use the current directory as the starting directory for the console. [check also the official manuals](https://docs.microsoft.com/en-us/windows/terminal/command-line-arguments?tabs=windows)

### remote

[use ssh](https://stackoverflow.com/questions/57363597/how-to-use-a-new-windows-terminal-app-for-ssh) `ssh user@host`

[use putty to connect remote server](https://stackoverflow.com/a/12118746/11844003)

- `plink -pw [password] [user@]host [command]`
- `putty.exe -ssh [username]@[hostname] -pw [password]`

[config the XLaunch](https://superuser.com/questions/1372854/do-i-launch-the-app-xlaunch-for-every-login-to-use-gui-in-ubuntu-wsl-in-windows/1372940)

[exit out of ssh connections and close putty?](https://unix.stackexchange.com/questions/41682/exit-out-of-all-ssh-connections-in-one-command-and-close-putty)

## VS Code

[find and replace newline?](https://stackoverflow.com/questions/30351529/find-and-replace-with-a-newline-in-visual-studio-code) in the local search box, press <kbd>ctrl</kbd> + <kbd>enter</kbd>

[multiline editing?](https://stackoverflow.com/questions/30037808/multiline-editing-in-visual-studio-code)

1. hold <kbd>ctrl</kbd> + <kbd>alt</kbd> while pressing the up or down arrow keys to add cursors
2. hold <kbd>alt</kbd> and left click to place cursors arbitrarily
3. when searching sth, press <kbd>alt</kbd> + <kbd>enter</kbd> to add cursors around

- [cause column selection mode is on](https://stackoverflow.com/questions/53651080/disable-multi-cursor-functionality)

- I want the word wrap effect? [View menu -> Toggle Word Wrapper](https://stackoverflow.com/questions/31025502/how-can-i-switch-word-wrap-on-and-off-in-visual-studio-code)

- use <kbd>ctrl</kbd> and <kbd>,</kbd> to open settings

## Office

- for 2016 & 2013 [disable auto capitalization](https://www.technipages.com/word-enable-disable-auto-capitalization) File -> Options -> Proofing -> AutoCorrect Options

### word stuff

- [x] `.Docx` files are not showing word icon but only white plain icon. [check](https://blog.csdn.net/brazy/article/details/81434302)
- extract file from a word: change extension to `zip`, extract the zip file, under the `word/embeddings` folder, change the extension of the `bin` file to what it should be.
- [show the non-printable character](http://addbalance.com/word/nonprinting.html)
- 在 office 文档中，要保持里面的图片，一张一张另存为太慢了，这个时候可以将这个文档的扩展名改为`rar`，然后解压就行（该方法只适用 docx xlsx pptx 文件）
- [it's just a zipped file](https://superuser.com/questions/278260/how-do-i-see-the-xml-of-my-docx-document), and you can [extract plain text from it](https://stackoverflow.com/a/25620447/11844003):

  ```bash
  unzip -p some.docx word/document.xml | sed -e 's/<[^>]\{1,\}>//g; s/[^[:print:]]\{1,\}//g'

  # if you want to leave newlines
  unzip -p document.docx word/document.xml | sed -e 's/<\/w:p>/\n/g; s/<[^>]\{1,\}>//g; s/[^[:print:]\n]\{1,\}//g'
  ```

### excel stuff

- <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>Enter</kbd> 在表格上插入空行 (<kbd>Alt</kbd> + <kbd>Enter</kbd>)
- [can not close excel](https://answers.microsoft.com/en-us/msoffice/forum/msoffice_excel-mso_win10-mso_2016/excel-will-not-close-workbook-when-clicking-x-if/326bc3fe-9170-43cf-9c94-8cbe62a1cb53)
- [Excel 格式转换](https://zhuanlan.zhihu.com/p/75404453)
- [Excel file still so large after deleting many tabs](https://answers.microsoft.com/en-us/msoffice/forum/msoffice_excel-mso_windows8-mso_2013_release/why-is-my-excel-file-still-so-large-after-i/4d2c0170-f92a-441b-b9c6-958adba02ea3), cuz u didn't do right, try resetting the used range
- [remove leading or trailing spaces](https://stackoverflow.com/questions/9578397/remove-leading-or-trailing-spaces-in-an-entire-column-of-data)

---

- Transpose Data from a Row to a Column `Paste -> Transpose(转置)`
- Compose Text with & `=A2&B2&C2&D2`
- Transforming the Case of Text `=UPPER(A2)`
- reserve leading zero with a leading apostrophe
- autofill series
- use <kbd>ctrl</kbd> + <kbd>d</kbd> to autofill with selected cell
- auto select a cell

## command line tools

- [install pkg-config](https://stackoverflow.com/questions/1710922/how-to-install-pkg-config-in-windows/22363820#22363820)

- If, for some reason, the gcc compiler is already installed, but the symbolic link `/usr/bin/cc` is missing, you can do with [`make CC=gcc`](https://askubuntu.com/a/1095184)

- fatal error - [cygheap base mismatch detected](https://superuser.com/questions/1380238/how-can-i-fix-the-error-fatal-error-cygheap-base-mismatch-detected-when-usin)

- ["perf-stat" on windows](https://stackoverflow.com/questions/34641644/is-there-a-windows-equivalent-of-the-linux-command-perf-stat)

- There is a tree command in windows already, it is `tree.com`. [check](https://superuser.com/a/1312725/1233932), (`/a` for just folder and `/f` for every single file); use `//` or bash would think it is a folder name

- [equivalent of `which`](https://stackoverflow.com/questions/304319/is-there-an-equivalent-of-which-on-the-windows-command-line)
  - use `where.exe` or `Set-Alias which where.exe`
  - use powershell `gcm` (`Get-Command`)
    
- [pidcat](https://github.com/JakeWharton/pidcat/issues/122)

## end
