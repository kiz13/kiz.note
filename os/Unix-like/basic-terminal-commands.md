# commander

- check os information `cat /etc/os-release`
- `curl` [post file](https://stackoverflow.com/questions/12667797/using-curl-to-upload-post-data-with-files)
- [Use grep --exclude/--include syntax](https://stackoverflow.com/questions/221921/use-grep-exclude-include-syntax-to-not-grep-through-certain-files) `grep pattern -r --include=\*.cpp --include=\*.h rootdir`
- [exclude words with grep with `--invert-match`](https://stackoverflow.com/questions/4538253/how-can-i-exclude-one-word-with-grep) `grep -v "unwanted_word" file`
- [how to get full path of a file?](https://stackoverflow.com/questions/5265702/how-to-get-full-path-of-a-file) `readlink -f filename.extension`
- [ping doesn't stop?](https://askubuntu.com/questions/200989/ping-for-4-times) `alias ping="ping -c 4"`, with the `-c` option, it will stop after sending 4 ECHO_REQUEST packets, check the [man page](https://man7.org/linux/man-pages/man8/ping.8.html)
- [list the disk usage of directories?](https://stackoverflow.com/questions/1019116/using-ls-to-list-directories-and-their-total-sizes) `du -sh`
- [determine linux kernel architecture](https://unix.stackexchange.com/questions/12453/how-to-determine-linux-kernel-architecture) `uname --machine`
- [How to install a rpm package and its dependencies offline?](https://stackoverflow.com/questions/50648152/how-to-install-a-rpm-package-and-its-dependencies-offline)
  - download that rpm from the machine with internet connected, then ftp the file to the sever and do `rpm -ivh pkg.rpm`
  - use `yumdownloader`
- [unzip tgz file](https://askubuntu.com/questions/499807/how-to-unzip-tgz-file-using-the-terminal) `tar -xvzf /path/to/yourfile.tgz`
  - `x` for extract
  - `v` for verbose
  - `z` for gnuzip
  - `f` for file, should come at last just before file name.
- [explanatory of different outputs with `file`](https://unix.stackexchange.com/a/151035)

## ssh

[automate ssh login with password](https://serverfault.com/questions/241588/how-to-automate-ssh-login-with-password)

[include a password with ssh](https://askubuntu.com/questions/224181/how-do-i-include-a-password-with-ssh-command-want-to-make-shell-script)

## helping links

- [\(pkgs.org\) Packages for Linux and Unix](https://pkgs.org/)
- [\(Linux Handbook\) use crontab](https://linuxhandbook.com/crontab/)
- [\(Open Group\) crontab docs](https://pubs.opengroup.org/onlinepubs/9699919799/utilities/crontab.html)
- [\(cnblogs\) grep命令详解](https://www.cnblogs.com/ggjucheng/archive/2013/01/13/2856896.html)
