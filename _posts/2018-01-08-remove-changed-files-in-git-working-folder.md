---
type: post
title: "Remove changed files in git working folder"
meta-description: "If something goes wrong, you can always go back with git-checkout and git-clean!"
share-img: "/img/remove-changed-files-in-git-working-folder/git-stages.png"
---

Git has [three states](https://git-scm.com/book/en/v2/Getting-Started-Git-Basics#_the_three_states).
 * working directory
 * staging area (index), files marked to be included in the next commit
 * .git directory, for files already in the git tree

Sometimes you may want to restore changed or staged files back as they were in last commit.

### To remove changed files use:
```bash
# this will discard changes to existing files
# and switch back to master branch
# works even for staged changes
git checkout -f master

# this will remove untracked files
# add -d to remove untracked folders
# add -x to remove .gitignored files
git clean -f
```

### Example from scratch
Clone a sample repo `hello-world/php`:
```bash
git clone git@labs.moneysmart.top:hello-world/php.git hello-world-php
```

Create and edit some files:
```bash
cd hello-world-php

# create new file
touch new_file

# modify existing file
echo "Add new line to existing file" >> README.md

# stage README.md file
git add README.md
```

To see current repository status:
```bash
git status
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   README.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        new_file
```
Now run the `git checkout -f master` and `git clean -f` commands to get back to last commit.
