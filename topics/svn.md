# svn

- where is `svn`? By default, the "command line client tools" option is unchecked (i.e., it won't be installed)

- `svn list url`

- `svn info`

- `svn rm --keep-local dirname` [the directory is already "in" svn](https://stackoverflow.com/questions/116074/how-do-i-ignore-a-directory-with-svn#comment13441727_116075), then the status of it is _D_

- `svn update` Bring changes from the repository into the working copy. [see also](https://stackoverflow.com/questions/30055174/svn-status-files-d-while-files-does-not-exist-anymore-from-local-directory-nor)

- [ignoring files](https://stackoverflow.com/a/19593719/11844003)

- `svn ci` commit (ci): Send changes from your working copy to the repository.

- `svn add --force <directory>` (recursively) add un-versioned files [check](https://stackoverflow.com/a/1218274)

- [do this right](https://stackoverflow.com/questions/2152454/how-to-start-an-svn-project-from-the-command-line)

- `svn checkout` results in **504 gateway timeout**, try the conf below
  ```txt
  [http]
  proxy = http://127.0.0.1:7890
  sslVerify = false
  ```
