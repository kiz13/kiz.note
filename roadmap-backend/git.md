# *

## github?

[git and GitHub differences?](https://stackoverflow.com/questions/13321556/difference-between-git-and-github)

> Git is a revision control system, a tool to manage your source code history.
>
> GitHub is a hosting service for Git repositories.

Remote repositories are for backup and collaboration. (from the [comment](https://stackoverflow.com/questions/13321556/difference-between-git-and-github#comment18172627_13321586))

## commands

local docs `${git-installation-directory}/mingw64/share/doc/git-doc/`

---

- `git branch -D branch_name` (`--delete --force`)
- `git branch -a` list both remote-tracking branches and local branches
- `git stash list` and `git stash pop`

[abort merge conflict](https://stackoverflow.com/questions/101752/i-ran-into-a-merge-conflict-how-can-i-abort-the-merge) `git reset --merge` for git version >= 1.6.1

add line break to the commit message? [Simon's answer](https://stackoverflow.com/a/5070502/11844003) the command below creates separate paragraphs - not lines.

  ```shell
  git commit -m "head line" -m "content line." 
  ```

### undo

[undo the last git add?](https://stackoverflow.com/questions/12132272/how-can-you-undo-the-last-git-add) `git reset` will unstage all the files you've added after your last commit

[undo a git reset?](https://stackoverflow.com/questions/2510276/how-to-undo-git-reset) `git reset 'HEAD@{xxx}'`

[undo a git reset hard?](https://stackoverflow.com/questions/5473/how-can-i-undo-git-reset-hard-head1) it should be similar to the question above

[yet another git reset](https://stackoverflow.com/questions/927358/how-do-i-undo-the-most-recent-local-commits-in-git)

### remote access

clone a repository

1. [create personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)
2. `git clone --config http.sslCAInfo=/usr/ssl/certs/ca-bundle.crt repo-url` [also check this answer and comments](https://stackoverflow.com/a/26710477) and [this one](https://stackoverflow.com/a/26785963/11844003) (p.s. [run command with administrator privilege](https://stackoverflow.com/questions/52140830/error-could-not-lock-config-file-c-program-files-git-mingw64-etc-gitconfig-pe) if permission denied)
3. provide your username and token
4. [openssl errno 10054?](https://stackoverflow.com/questions/25485816/openssl-errno-10054-connection-refused-whilst-trying-to-connect-to-our-server)

[clone just one branch](https://stackoverflow.com/a/14930421/11844003) `git clone -b another_one --single-branch git_repo`

[download a single folder or directory](https://stackoverflow.com/questions/7106012/download-a-single-folder-or-directory-from-a-github-repo)

[clone a subdirectory only](https://stackoverflow.com/questions/600079/how-do-i-clone-a-subdirectory-only-of-a-git-repository/52269934#52269934)

[git clone with ssl verify](https://stackoverflow.com/questions/11621768/how-can-i-make-git-accept-a-self-signed-certificate)

[push changes to remote branch](https://stackoverflow.com/questions/36139275/git-pushing-to-remote-branch)

[update a local repo with changes from a GitHub repo](https://stackoverflow.com/questions/1443210/updating-a-local-repository-with-changes-from-a-github-repository) `git pull origin master`

[change the remote url for a repo](https://stackoverflow.com/questions/44390210/how-can-i-change-the-url-for-a-project-in-gitlab) `git remote set-url origin url`

[git asks for username and pwd every time I push](https://stackoverflow.com/questions/11403407/git-asks-for-username-every-time-i-push) use the globally configured info `git config credential.helper store`

[delete remote branch](https://stackoverflow.com/questions/2003505/how-do-i-delete-a-git-branch-locally-and-remotely) `git push -d origin branch-name` the `origin` is the remote name ini most cases

[delete a git branch remotely](https://stackoverflow.com/questions/2003505/how-do-i-delete-a-git-branch-locally-and-remotely)

- `git push -d <remote_name> <branchname>`

### configuration

[get start with first time setup](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup)

`git config -l --show-origin` view all settings

- `-l` --list, list all variables set in config file, along with their values.
- `--show-origin` show the actual origin (config file path, ref, or blob id if applicable).

`git config --global user.name "John Doe"`

`git config --global --unset core.xxx`
 
[where is the global `.gitconfig` file](https://stackoverflow.com/a/17619024/11844003), do a `git config --global -e` and then, if you're lucky, you will get a text editor loaded with the global `.gitconfig` file. (created if missing)

### statistics

#### logs

`git shortlog -s -n` [see also](https://stackoverflow.com/questions/42715785/how-do-i-show-statistics-for-authors-contributions-in-git)

- `-n` --numbered, sort by number of commits per author instead of author alphabetical order
- `-s` --summary, show only the commit count summary

[type `q` to exit the out of `git log`](https://stackoverflow.com/questions/9483757/how-to-exit-git-log-or-git-diff)

#### files

[show all files under version control](https://stackoverflow.com/a/15606995) `git ls-tree -r master --name-only`

- `-r` recurse into subdirectories
- `--name-only` show only the file names

#### diff

[see the differences between two branches?](https://stackoverflow.com/questions/9834689/how-can-i-see-the-differences-between-two-branches) `git diff --name-only branch1 branch2 [--]` appending that `--` if the branch name also name some files

## what and why

[what is the convention for an initial git commit message](https://stackoverflow.com/questions/35103508/what-is-the-convention-for-the-content-of-an-initial-first-git-commit)

[LF will be replaced by CRLF, what is it?](https://stackoverflow.com/questions/5834014/lf-will-be-replaced-by-crlf-in-git-what-is-that-and-is-it-important)

[why edited hunk does not apply](https://stackoverflow.com/a/3268698/11844003)

[tag?](https://stackoverflow.com/questions/1457103/how-is-a-tag-different-from-a-branch-in-git-which-should-i-use-here)

## helping links

- tool [repo visualization](https://next.github.com/projects/repo-visualization/)
- roriri 的博客 [commit message 格式参考](https://roriri.one/2019/12/06/git-commit-message/)
- v2ex [`git commit message` 用中文還是英文的帖子](https://www.v2ex.com/t/221152)
- someone's blog [how to write a git commit message](https://cbea.ms/git-commit/) the url used to be `https://chris.beams.io/posts/git-commit/`
- someone's blog [a successful git branching model](https://nvie.com/posts/a-successful-git-branching-model/)
- [A collection of useful `.gitattributes` templates](https://github.com/alexkaratarakis/gitattributes)
- [Git Best Practices](https://sethrobertson.github.io/GitBestPractices/)
- [bitbucket - no foxtrot merge](https://bitbucket.org/blog/no-foxtrot-merges-allowed)

## end
