# An intro to Git

## Not covered
* git config - http://git-scm.com/docs/git-config
* ssh config - https://help.github.com/articles/generating-ssh-keys/

## Intro
What is git? Distributed SCM.

## Creating a repo and our first commit

```
mkdir animals
cd animals
touch animals.txt
git status (see not a repository)
git init
git status (see untracked file)
vi animals.txt
(add some animals)
git status (see untracked file)
git add animals.txt
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
git add animals.txt
git status (see staged changes)
git reset
git status (see unstaged changes)
touch file
git status
git add file
git status (see one staged and one unstaged)
git commit -m 'added a file'
git status (see one unstaged. one committed)
git log (see our commit)
git show (see only our commit)
git status (see one unstaged)
vi animals.txt (add a lion on top)
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
(explain why rebase is prefereable)

# Resources
* https://git-scm.com/book
* https://try.github.io
* [StackOverflow](http://stackoverflow.com/questions/tagged/git)
