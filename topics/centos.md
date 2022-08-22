# CentOS

Q: where can I check os information?

A: check `/etc/os-release`

Q: [apt-get command not found?](https://unix.stackexchange.com/a/34028/437816)

A: For you using cent-os, [yum](https://en.wikipedia.org/wiki/Yum_(software)) is the default _package manager_. Then you should use `sudo yum install <packagename>`

Q: [where are the crontab logs?](https://unix.stackexchange.com/a/176232/437816)

A: `/var/log/cron`, though, this only logs the execution of commands, not the results or exit statuses. The output of the executed command goes to the user's mail by default.

Q: [how to install a rpm package and its dependencies offline?](https://stackoverflow.com/a/66927190/11844003)

A: use `yumdownloader` on another CentOS server with Internet access, it'll download all RPMs required, then compress the directory and upload it to the server, then `yum install -y --cacheonly --disablerepo=* /path/to/your/*.rpm`

## helping links

- (pkgs.org) [Packages for Linux and Unix](https://pkgs.org/)
- [rpm - man page](https://rpm-software-management.github.io/rpm/man/rpm.8.html)
