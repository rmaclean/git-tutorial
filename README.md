# An intro to Git

# Prep
- git config unset --global pull.rebase
git config --global alias.dad '!curl https://icanhazdadjoke.com/ && echo'

## Creating a repo and our first commit

```
mkdir food
cd food
code recipes.txt
git status (see not a repository)
git init
git status (see untracked file)
ls -a
cd .git
cat config
cat HEAD
code recipes.txt
(add some animals)
git status (see untracked file)
git add recipes.txt
git status (see staged file)
git commit -m 'adds some animals'
git status (see no staged files and no untracked files)
git log (see our commit, our sha-1)
```

## Staged and unstaged changes

```
vi animals.txt (add a frog)
git status (see unstaged changes. Explain untracked vs unstaged)
git diff
git add . (talk to the difference in this one)
git status (see staged changes)
git restore --staged recipes.txt
git status (see unstaged changes)
code cocktails.txt
git status
git add cocktails.txt
git status (see one new and one modified)
git commit -m 'added a file'
git status (see one unstaged. one committed)
git log (see our commit)
git show (see only our commit)
git status (see one unstaged)
code recipes.txt (add a lion on top)
git status
git diff
git add -p animals.txt (split - yes to lion no to frong)
git status (see unstaged and staged. explain deltas are lines not files)
git commit -m 'added a lion'
git status
git diff
git add .
git commit -m 'added a frog'
git status
```

## Working with others

(Explain distributed vs server/client. Everyone has the repo.)
(Create a repo on github - follow instructions. Explain ssh vs https.)
```
git remote add origin <repo-url> (explain remotes)
git push -u origin master (explain tracking and branches)
```

(Refresh repo page on github)
(explain git is not github)

```
git status (see tracking info)
git remote
git remote get-url origin
vi animals.txt (add monkey)
git status
git add .
git status
git commit -m 'added a monkey'
git status (ahead by ...)
```

(How does someone else see all this?)
```
cd ..
mv animals dev1
ls
git clone <repo-url> (get from github)
ls
mv <repo-name> dev2
ls
cd dev2
git status
git log (see added a monkey)
cd ../dev1
git status
git log
git push
git status
cd ../dev2
git status
git fetch
git status
git log
git pull
git log
```

(Dealing with conflicts)
```
vi animals.txt (capital letters)
git status
git add .
git status
git commit -m 'start with capital letters'
git status
git push
cd ../dev1
vi animals.txt (note we dont have changes. change frog to unicorn.)
git status
git add .
git status
git commit -m 'change frog to unicorn'
git status
git push (explain reject - how distributed works)
git fetch
```

(the merge - 2 ways)

(prep)
```
cd ..
ls
cp -r dev1 dev1-merge
ls
mv dev1 dev1-rebase
ls
```

(way 1 - merge)
```
cd dev1-merge
git status
git push (see reject)
git pull (see conflict, see instructions)
git status (see both modified)
vi animals.txt (resolve conflicts)
git status
git add animals.txt
git status
git commit (accept message)
git status
git log (see merge commit)
git log --graph --pretty=oneline --abbrev-commit

```
(way 2 - rebase)
```
cd ../dev1-rebase
git status
git push
git pull --rebase (see instructions - First, rewinding head to replay your work on top of it...)
git status
vi animals.txt (resolve conflict)
git status
git diff (explain that we're changing our commit)
git add animals.txt
git status
git rebase --continue (explain applying)
git status
git log (see our commit after the dev2 commit)
git log --graph --pretty=oneline --abbrev-commit
```
(explain why rebase is preferable)

-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-

# Branching

```
git branch -M uno
git switch -c demo
git status
git switch demo

git status (note no tracking)
edit file
git commit -am ""
git push (since it knows about origin sets it up)

talk about pull requests
```

https://mermaid.live/
- gitGraph

Trunk based
```
gitGraph
    commit
    branch feature1
    commit
    commit
    switch main
    merge feature1
    branch feature2
    commit
    switch main
    branch hotfix1
    commit
    switch feature2
    commit
    switch main
    merge feature2
    branch feature3
    commit
    switch hotfix1
    commit
    switch main
    merge hotfix1
```

Git flow
```
gitGraph
commit
branch dev
commit
branch feature1
commit
commit
switch dev
branch feature2
commit
commit
switch dev
merge feature1
branch release1
commit
switch main
merge release1
switch dev
merge release1
```

TAGS
annotaed have details in the DB, like date/author/signing
lightweight just a tag

```
git tag
git tag v2.0
git tag
git log
git tag -a v3.0
git tag -a v3.0.1 -m "my version 2"
commit
git tag -l "v3.0*"
git tag v1.0 3ed70a56216667bf7832503b
e7eb38a5849a90d2
git push (show nothing went up)
git push --tags
```

```
git checkout <hash / tag>
```

```
git stash
git stash -l
git stash pop
git stash
git stash apply
```

```
.gitgnore
gitignore website
```

```
edit file
commit
edit file
commit --amend
```

```
branch feat
add 2 commits
switch back to main
git log
git log feat --oneline
git cherry-pick hashco
```

SLIDES

```
edit file A
edit file B
git diff (see both)
git add A
git status
git diff (no longer shows staged)
git diff --staged
```

```
git config -l
git config --global -l
git config alias.st status
git config alias.diffs diff --staged
git config alias.hello "!echo hi"
git dad
```

SLIDES

prepare-commit-msg
```
#!/bin/sh
echo "# Please include a useful commit message!" > $1
```
chmod +x prepare-commit-msg

```
npm init
npx husky init
.husky
talk about pre-commit
```
pre-commit


```
git gc
git maintenance run
git maintenance start
```

```
git bisect start
```

VS Code

-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-

# Resources
* https://git-scm.com/book
* https://try.github.io
* [StackOverflow](http://stackoverflow.com/questions/tagged/git)
