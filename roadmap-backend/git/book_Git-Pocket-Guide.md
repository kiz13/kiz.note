# *

## table of contents

- [get started](#dirt)
- [add stuff](#add)
- [commit stuff](#commit)
- [undo stuff](#chapter4-undoing-and-editing-commits)
- [branching](#chapter5-branching)
- [tracking other repos](#chapter6-tracking-other-repos)
- [merging](#chapter7-merging)
- [naming commits](#chapter8-naming-commits)
- [viewing history](#chapter9-viewing-history)
- [editing history](#chapter10-editing-history)
- [misc](#miscellaneous)

## dirt

The `commit` is the fundamental unit of change in Git. It consists of: a pointer to a tree containing the complete state of the repo content at one point in time; ancillary info about this change (the 'author', the 'committer' ...); etc.

`git init directory` will create the argument directory if needed.

`git commit` creates a new tree object capturing the current state of the index, as well as a commit object with ur comment text, personal identification, the current time, and so on, pointing to that tree. It finally sets the _master_ branch to the new commit; that is, makes the ref `refs/heads/master` point to the new commit ID:

```shell
$ git log --pretty=oneline
id  (HEAD -> master) last_commit_msg
id2 commit_msg2
...
$ git show-ref master
id  refs/heads/master
```

> Git doesn't track directories as separate entities; rather, it creates directories in the working tree as needed to create the paths to files it checks out, and removes directories if there are no longer any files in them. This implies that u can't represent an empty dir directly to Git. You have to put at least one placeholder file within the dir to get Git to create it.

## add

`git add [--dry-run | -n] [--force | -f] [--interactive | -i] [--patch | -p] [--edit | -e] [--update | -u] blah [<pathspec>]`

<code>git add _filename_</code>: Git adds the current working file contents to the object database as a new blob-type object (assuming it's not already there) if the file is new, then this will be a new index entry; if not, just an updated one pointing to the new object.

A file is 'new' if its pathname isn't in the index, this causes `git status` to note a file as 'untracked' prior to ur adding it.

Adding partial changes(for TRACKED files): `git add -p (--patch)` this (with no args) starts an interactive loop

    y - stage this hunk
    n - do not ...
    q - quit; do not stage this hunk or any of the remaining ones
    a - stage this hunk and all later hunks in the file
    d - do not ...
    ....
    e - manually edit the current hunk
    ? - print help

`git add -A (--all)` include all filenames in the index and in the working tree; this stages new files as well.

## commit

`git commit -a` adds all tracked, modified files to the index before committing. This commits **changed** and **deleted** files, but NOT new ones; it is equivalent to `git add -u` followed by `git commit`

Because of content-based addressing if u change anything about a commit, it becomes a different commit, since it now has a different object ID. So when speak of changing a commit, we really mean replacing it with one having corrected attrs or contents.

with `git commit --amend` git will present u with the previous commit message to edit.

`git commit --amend -m msg` If no changes are made to the index, it functions the same as above.

## Chapter4 undoing and editing commits

discarding commits: `git reset rev` it moves the head of the current branch to a given commit, it updates the index but leaves the working tree alone. ("uncommit" and continue working), when discarding more than one commit, some further options to git reset become useful:

- `--mixed` the default: makes the index match the given commit, but does not change the working files.
- `--soft` This resets the branch tip only, and does not change the index; the discarded commit’s changes remain staged. You might use this to stage all the changes from several previous commits, and then reapply them as a single commit.
- `--merge`
- `--hard`

undoing: `git revert rev` it is used to record some new commits to reverse the effect of some earlier commits (often only a faulty one)

## Chapter5 Branching

`git checkout -b simon 9c6a1fad` starts a new branch 'simon' at the named commit and switches to it.

> -b option is a special case: switching to a branch that doesn't yet exist is creating a new branch.

`git branch simon` just creates a new branch but not switch to it.

> The HEAD by definition indicates the branch that you are 'on.'

`git symbolic-ref HEAD` shows the ref(branch name) to which HEAD points

`git branch -d simon` simply deletes a pointer: a branch name ref that points to the branch tip. It doesn't delete the content of the branch.

Renaming a local branch: <code>git branch -m _old_ _new_</code>

## Chapter6 Tracking other Repos

The `git clone` command initializes a new repository with the contents of another one and sets up tracking branches between the two with push/pull mechanism. We call the first repository a "remote", and by default, this remote is named _origin_; u can change this with the `--origin (-o)` option, or with `git remote rename` later on.

`git clone https://.../foo.git` if give a second argument, Git will create a directory with that name for the new repo(or use an existing dir, so long as its empty); otherwise, it derives the name from that of source repo using some ad hoc rules. E.g., foo stays foo, but foo.git and bar/foo also become foo

page 86 ... remote case ...

`git pull` If only u or the upstream has added commits to this branch since ur last pull, then this will succeed with a "ff (fast-forward)" update: one branch head just moves forward along the branch to catch up with the other.

If `git pull` starts a merge when u know there's no need for it, u can always cancel it by giving an empty commit msg, or with `git merge --abort` if the merge failed leaving u in conflict-resolution mode. If u complete such a merge and want to undo it, use `git reset HEAD^` to move ur branch back again, discarding the merge commit. U can then use `git pull --rebase` instead.

<code>git remote show _remote_</code> gives a useful summary of the status of the repo in relation to a remote.

`git branch -vv` (lists upstream for each branch) gives a more compact summary without contacting the remote (and thus reflects the state as of the last fetch or pull)

## Chapter7 Merging

Most often there r only two branches involved, but there can be any number, and that is called an "octopus merge".

### Resolving merge conflicts

`git merge theirs` if merge conflicts happened, and u want to cancel it, use `git merge --abort`. To get an overview of the merge state, use `git status`.

- an `add/add` conflict, in which the same filename is added to both branches but with different contents

If you want to discard all the changes from one side of the merge, use <code>git checkout --{ours,theirs} _file_</code> to update the working file with a copy from the current or other branch, followed by <code>git add _file_</code> to stage the change and mark the conflict as resolved. Having done that, if u would like to apply _some_ changes from the opposite side, use <code>git checkout -p _branch file_</code>

To find out what went wrong in detail, use `git diff`. It will show the differences between various combinations of working tree, index and commits; it also displays the alternative versions of the section in conflict. (Git then updated the working file with similar stuff) e.g.,

```text
hello
doctor
<<<<<<< ours
Jupiter
dolphin
=======
Europa
monoliths
>>>>>>> theirs
yesterday tomorrow
```

Once you’ve edited the file to resolve the conflict, then stage your fixed version for commit. Once you’ve addressed all the conflicts and `git status` no longer reports any unmerged paths, you can use `git commit` to complete the merge

page 104 Notes

>When merging several branches, Git seeks a "merge base": a recent common ancestor of all the branch tips, to use as a reference point for arbitrating changes.

`git ls-files -s --abbrev` shows the contents of the index: ID of the blob object holding the file's contents, the stage number, and the filename. After a merge conflict, it'll show three messages: merge base one, current branch one, and "other" branch one. Stage number is 1, 2, 3 respectively.

Use <code>git cat-file -p _ID(or :n:path)_</code> see the contents of the different stages Another syntax referring to a specific stage of a file: <code>git show _:n:path_</code>

- if all three stages match, reduce to a single stage 0.
- If stage 1 matches stage 2, then reduce to a single stage
  0 matching stage 3 (or vice versa): one side made a change while the other did nothing.
- If stage 1 matches stage 2, but there is no stage 3, then remove the
  file: we made no change, while the other branch delete it, so
  accept the other branches' deletion.
- If stage 1 and 2 differ, and there is no stage 3, then report
  a "modify/delete" conflict: we changed the file, while the other
  branch deleted it; the user must decide what to do.

### Merging strategies

`git merge -s ours` discards all changes from the other branch (u might use this to retain the history of a branch, without incorporating its effects.)

## Chapter8 Naming commits

To find a ref named `foo`, Git looks for the following in order:

1. foo: Normally, these r refs used by Git internally, such as HEAD,
   MERGE_HEAD, FETCH_HEAD ... and r presented as files directly under `.git`
2. refs/foo
3. refs/tags/foo: The namespace for tags
4. refs/heads/foo: The namespace for local branches
5. refs/remotes/foo: The namespace for remote ...
6. refs/remotes/foo/HEAD: The default branch of the remote "foo"

### Names relative to a given commit

Below the `rev` refers to any "revision"—an object referred to using any of the syntax.

- rev^ = rev^1
- rev^0 = rev if rev is a commit. If rev is a tag, then rev^0 is the commit to which the tag refers.
- rev~ = rev~1
- rev~0 = rev

---

Addressing path names: `rev:path`; special cases: `:path`, `:n:path`

Naming sets of commits: using a combination of reachability in the commit graph, and the usual mathematical operations on sets: union, intersection, complement, and difference.

- A: add all commits reachable from A
- ^A: remove all commits reachable from A
- A^@: add all commits reachable from A, but exclude A itself.
- A^!: add only the commit A

- --not X Y Z = ^X ^Y ^Z

- A B C ... ^X ^Y ^Z = (A ∪ B ∪ C ∪ ...) ∩ (X ∪ Y ∪ Z ∪ ...)

- A...B = A B --not $(git merge-base A B)
  all commits reachable from either A or B, but not from both. It's called _symmetric difference_, which is the name for the corresponding set operation: (A ∪ B) - (A ∩ B)

`foo@{upstream}` (or ...{u}) names the branch upstream of the branch _foo_, as defined by the repository configuration. This is usually arranged automatically when checking out a local branch corresponding to a remote one, but may be set explicitly with commands such as `git checkout --track`, `git branch --set-upstream-to`, and `git push -u`. It just gives the object ID of the upstream branch head, though.

- `git rev-parse HEAD@{u}` object ID
- `git rev-parse --abbrev-ref HEAD@{u}` origin/master
- `git rev-parse --symbolic-full-name HEAD@{u}` refs/remotes/origin/master

## Chapter9 Viewing history

<code>git log [_options_] [_commits_] [[--] _path_ ...]</code>

`git log` The default for commits is HEAD

`git log topic` lists all commits in the _topic_ branch, even if u r on another branch.

`git log topic feature` all commits on either of the branches.

### Output formats

some options available for `git log`:

- `--oneline` short for `--format=oneline --abbrev-commit`; the default is `--format=medium`
- `--pretty` is a synonym for `--format`
- `--graph`
- `--diff-filter`=[A|C(copied)|D|M|R(renamed)|T(type change)] (just one of them)
- `--walk-reflog (-g)`
- `--stat` gives an ASCII-art graph representing the amount and kind of change in each file

`git log --cherry-pick master...other` omits the patch equivalent commits, that is commits produced with <code>cherry-pick _what_</code> and _what_

The variation `--cherry-mark` will mark duplicate commits with an equal sign before the ID, instead of omitting them.

`git cherry [-v] [upstream [head [limit]]]` It shows commits on a branch that are not in the upstream, making those whose changes are duplicated by distinct upstream commits with a minus sign (while other commits have a plus sign).

`git shortlog` summarizes commit history, grouping commits by authors with the number of commits and their subjects ...

## Chapter10 Editing history

The steps Git follows during a rebase are as follows:

1. Identify the commits to be replicated.
2. Compute the corresponding changesets.
3. Move HEAD to the new branch location.
4. Apply the changesets in order, making new commits preserving author info.
5. Finally, update the branch ref to point to the new tip commit.

`git rebase [--onto newbase] [upstream] [branch]` means to replay the commit set `upstream..branch` starting at `newbase`. The defaults are:

- `upstream` HEAD@{upstream}
- `branch` HEAD
- `newbase` The upstream argument

### Undo a rebase

To undo the rebase, then, all u need to do is moving the branch ref back to its original spot, which u can discover using the reflog.

Find the spot where it starts rebase, then get the previous commit id and run `git reset --hard commit_id`

### Commit surgery

To replace a commit, say b5ef899, first, check it out and amend it, a new commit is created, say 82d4c5b, which has the same content and parents as the 'commit to be replace'. Then just use `git replace b5ef899 82d4c5b`.

The replacement list is an artifact of ur repo; it alters ur view of the commit graph, but not the graph itself. If u were to clone this repo or push to another one, the replacement would not be visible there. To make it 'real', we have to actually rewrite all the subsequent commits, which u can do thus: `git filter-branch -- --all`

> see also the warning at page 162

## Miscellaneous

`git cherry-pick` apply the changeset of a given commit as a new commit on the current branch, preserving the original author info and commit message. ... E.g. u might discover that a bug fix applied to a certain version actually needs to be applied to an earlier one as well, and merging in that direction is not desirable ...

`git rev-parse` mainly for use by other Git programs to parse and interpret portions of Git command lines that use common options for specifying revisions ... several options: `-- git-dir` `--show-toplevel` ...

`git clean` removes untracked files from the working tree ... options include:
- --force (-f) really do sth. `git clean` will make no changes without this flag,
  unless u set `clean.requireForce` to false.
- --dry-run (-n) show what would be done, but remove no files.
- ...
- -d remove untracked directories as well as files...
- -X remove only ignored files

---

`git stash` saves your current index and working tree ... this allows u to conveniently set aside and later restore ur working state so that u can change branches, pull, or perform other operations that world be blocked by ur current changes.

The saved states r arranged in a "stack," meaning ... Unlike a pure stack, however, the commands do generally allow u to bypass the stack order and directly address previous states, if u want to.

subcommand: `save` (the default), `list`, `show`, etc.

---

`git show` displays a given object (default HEAD) in a manner appropriate to the object type:

- _commit_ commit ID, author, date, and diff
- _tag_ tag message and tagged object
- _tree_ pathnames in (one level of) the tree
- _blog_ contents

E.g., to see the diff from one commit to the next, u could use `git diff foo~ foo`, but `git show foo` is just simpler.

The command takes any options valid for `git diff-tree`

---

<code>git tag _tagname commit_</code> creates a new lightweight tag
pointing to the given commit (default HEAD)

### diff

`git diff` shows any remaining _unstaged_ changes, adding the `--cached` option (or the synonym `--staged`) shows the difference between the index and last commit instead (it checks the actual changes you're applying)

`git diff <commit>` shows the difference between the working tree and the named commit

`git diff <A> <B>` shows the difference between two commits, trees, or
blobs A and B.

U can limit the comparison to specify files with trailing
patterns: `git diff -- '*.java' '*.[ch]'`

`git diff` accepts quite a few options, most of which it has in common with `git log`

## end

[back to top](#table-of-contents)
