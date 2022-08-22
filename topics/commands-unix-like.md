# man

[How the `file` command works?](https://unix.stackexchange.com/a/151035/437816)

[What is the difference between `grep`, `pgrep`, `egrep`, and `fgrep`?](https://superuser.com/a/508882/1233932)

## usage

Q: [use `curl` to upload form data with files](https://stackoverflow.com/a/12667839/11844003)

A: use `--form` (`-F`) option: `curl -F "what=ever" -F "image=@/home/k/where/test.jpg"`. The `@` means the content for the named form field should be loaded from a file path. Without it the string argument itself is passed through.

Q: [Use grep --exclude/--include syntax to not grep through certain files?](https://stackoverflow.com/a/221929/11844003)

A: `grep pattern -r --include=\*.cpp --include=\*.h rootdir`

Q: [exclude words with grep?](https://stackoverflow.com/a/4538335/11844003)

A: use `--invert-match` (`-v`) option: `grep -v "unwanted_word" file`

Q: [how to get full path of a file?](https://stackoverflow.com/questions/5265702/how-to-get-full-path-of-a-file)

A: `readlink -f filename.ext` or `realpath -s filename.ext` (see also [realpath v.s. readlink](https://unix.stackexchange.com/questions/136494/whats-the-difference-between-realpath-and-readlink-f))

Q: [ping doesn't stop? Can I ping only for 4 times then stopped? If I can, can I use it as default?](https://askubuntu.com/a/200992/1097027)

A: `ping -c 4 google.com`, with `-c 4`, it will stop after sending 4 ECHO_REQUEST packets. If you want to make this as a default, create an alias `alias ping="ping -c 4"`

Q: [list the disk usage of directories?](https://stackoverflow.com/a/1019124/11844003)

A: `du -csh` **D**isk **U**sage
- `-c/--total`
- `-s/--summarize` (top level file/folder)
- `-h/--human-readable` (with size unit suffixes)

Q: [determine linux kernel architecture?](https://unix.stackexchange.com/questions/12453/how-to-determine-linux-kernel-architecture)

A: `uname -m` (`--machine`)

Q: [extract `.tgz`/`.tar.gz` file?](https://askubuntu.com/a/499809/1097027)

A: `tar -xzvf /path/to/yourfile.tgz` [_eXtract Ze Vucking File_](https://www.reddit.com/r/ProgrammerHumor/comments/whx66x/comment/ij8a3ak/?utm_source=share&utm_medium=web2x&context=3)
- `x` for extract
- `z` for gnuzip
- `v` for verbose
- `f` for file, should come at last just before file name.

Q: [unzip `.zip` file?](https://askubuntu.com/questions/86849/how-to-unzip-a-zip-file-from-the-terminal)

A: use `unzip file.zip` or `7z x file.zip` (make sure you have `unzip` or `p7zip` installed)

Q: [parse JSON returned from a curl request?](https://stackoverflow.com/a/1955555)

A: use [jq](https://stedolan.github.io/jq/), e.g., `curl -s 'https://api.github.com/users/lambda' | jq -r '.name'` outputs the value of the top level json key `name`

Q: [use `tree` command without installing it system-wide?](https://superuser.com/a/190499)

A: `tree` doesn't seem to have particular dependencies (libc6), so you may simply copy the executable into an env path.

Q: [`grep` specify **or** condition?](https://unix.stackexchange.com/a/21765)

A: With normal regex, the characters `(`, `|` and `)` need to be escaped; with _extended regex_ (`-E`) option, you don't need the escapes
- `grep "ass\|hole"`
- `grep -E "ass|hole"`

Q: [move all files from sub folders to parent folder?](https://askubuntu.com/a/146643)

A: go to the parent dir and run `find . -mindepth 2 -type f -print -exec mv {} . \;`

Q: [find ipv4 address from command line?](https://unix.stackexchange.com/questions/504163/easily-find-ipv4-address)

A: `ip -c -4 addr` The `-c[olor]` parameter adds colour to the IP addresses, so you can easily find it.

Q: [list files ordered by size?](https://unix.stackexchange.com/a/53738/437816)

A: use `-S` option: `ls -hlS`

Q: [prevent 'grep' from showing up in ps results?](https://unix.stackexchange.com/questions/74185/how-can-i-prevent-grep-from-showing-up-in-ps-results)

A: `ps aux | grep "[p]rometheus"` or `pgrep prometheus`

Q: [use `curl` to stimulate `wget`?](https://stackoverflow.com/a/65571522/11844003)

A: `curl -kLSs your_link -o file.what`
- `L` follow redirects
- `o` (lower case O) to write output to file instead of stdout.
- `Ss` silent mode, but show errors, if any
- `k` allows curl to proceed and operate even for server connections otherwise considered insecure.

## helping links

- [\(Linux Handbook\) use crontab](https://linuxhandbook.com/crontab/)
- [\(Open Group\) crontab docs](https://pubs.opengroup.org/onlinepubs/9699919799/utilities/crontab.html)
- [\(cnblogs\) grep命令详解](https://www.cnblogs.com/ggjucheng/archive/2013/01/13/2856896.html)
- [\(nixCraft\) grep with examples](https://www.cyberciti.biz/faq/grep-regular-expressions/)
