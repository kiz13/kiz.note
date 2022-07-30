# [online book](https://jwiegley.github.io/git-from-the-bottom-up/)

## terms

- **repository** a collection of _commits_, each of which is an archive of what the project's _working tree_ looked like at a past date.
- **the index** git doesn't commit changes directly from the _working tree_ into the _repository_. Instead, changes are first registered in something called **the index**. Think of it as a way of "confirming" your changes, one by one, before doing a commit.
- **working tree** any directory on your filesystem which has a _repository_ associated with it.
- **commit** a snapshot of your working tree at some point in time. The state of _HEAD_ at the time your commit is made becomes that commit's parent. This is what creates the notion of a "revision history".
- **branch** just a name for a commit, also called a reference
- **tag** also a name for a commit, similar to a _branch_, except that it always name the same commit, and can have its own description text.
- **master** the main line of development in most repositories is done on a branch called "master". (typical default)
- **HEAD** used by your repository to define what is currently checked out:
  - if you checkout a branch, `HEAD` symbolically refers to that branch, indicating that the branch name should be updated after the next commit operation.
  - if you checkout a specific commit, `HEAD` refers to that commit only. This is referred to as a _detached HEAD_, and occurs, e.g., if you check out a tag name.

## commit by any other name

- branchname: the name of any branch is simply an alias for the most recent commit on that "branch".
- tagname: a tag-name alias is identical to a branch alias in terms of naming a commit. It never changes.
- HEAD: the currently checked out commit.
- a commit may always be referenced using its full 40-character SHA hash id. U only need use as many digits of a hash id as are needed for a unique reference within the repository.
- **name^**: the parent of any commit is referenced using the caret symbol.
- **name^^**: carets may be applied successively; "the parent of the parent".
- **name^2**: if a commit has multiple parents, you can refer the _nth_ parent using name^n
- **name~10**: a commit's _nth_ ancestor may be referenced using a tilde followed by the ordinal number
- **name:path** to reference a certain file within a commit's content tree, specify that file's name after a colon. This is helpful with `show`, or to show the difference between two versions of a committed file, e.g., `git diff HEAD^1:Makefile HEAD^2:Makefile`
- **name1..name2**: indicate _commit ranges_, which are supremely useful with commands like `log` for seeing what's happened during a particular span of time. The syntax to the left refers to all the commits reachable from **name2** back to, but not including, **name1**. If either is omitted, `HEAD` is used in its place.
- **name1...name2**: for commands like `log`, it refers to all the commits referenced by **name1** or **name2**, but not by both. for commands like `diff`, the range expressed is between **name2** and the common ancestor of **name1** and **name2**.
- some other names

## dirt on

### rebase

```bash
git checkout Z    # switch to the Z branch
git merge D       # merge commits D into Z
```

Instead of doing a merge "meta-commit", the contents are related to work done solely in the repository, and not to new work done in the working tree—there is a way to transplant the Z branch straight onto D.

```bash
git checkout Z
git rebase D      # change Z's base commit to point to D
```

Every time you rebase, you're potentially changing every commit in the branch.

rule of thumb: Use `rebase` if you have a local branch with no other branches that have branched off from it, and use `merge` for all other cases. `merge` is also useful when you’re ready to pull your local branch’s changes back into the main branch.

iterative rebase: `git rebase -i`, pick (default), squash, edit

### add

in case you forget it: `git add -i` -> type `p` or `5` -> type `?`, then ... -> type `e` (manually edit) -> do stuff in vim

### reset

With the `--mixed` option (or no option at all, as this is the default), reset will revert parts of the index along with the HEAD reference to match the given commit.

```bash
git add foo.c     # add changes to the index as a new blob
git reset HEAD    # delete any changes staged in the index
```

The `--soft` option only changes the meaning of `HEAD` and doesn't touch the index.

`git reset --soft HEAD^` backup HEAD to its parent, effectively ignoring the last commit. This is the same as `git update-ref HEAD HEAD^` (manually)

### stash & reflog

The _reflog_ records—in the form of commits—every change you make to your repository. When you create a tree from your index and store it under a commit, you are also inadvertently adding that commit to the reflog. The commit can be viewed using `git reflog`

... reach the end of a long day, a good habit to get into is to stash away your changes with `git stash`; it takes all the directory's contents—including both the working tree, and the state of the index—and creates blobs for them in the ...

`git stash list` or `git reflog show stash`

`stash apply` pull the changes back out of the stash

`git log stash@{1}`, `git show stash@{1}`, `git checkout -b temp stash@{1}`

If you ever want to clean up your stash list — say to keep only the last 30 days of activity — don’t use stash clear; use the reflog expire command instead: `git reflog expire --expire=30.days refs/stash`

The beauty of `stash` is that it lets you apply unobtrusive version control to your working process itself: namely, the various stages of your working tree from day to day.
