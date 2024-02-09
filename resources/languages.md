# Language/Shell Specific References

- [bash](https://www.gnu.org/software/bash/manual/bash.html)
- [C](https://www.gnu.org/software/gnu-c-manual/gnu-c-manual.html)
- [Python](https://docs.python.org/3/)
<!-- - [Pandas](https://pandas.pydata.org/)
- [Matplotlib](https://matplotlib.org/)
- [Seaborn](https://seaborn.pydata.org/) -->
<!-- - [Sci-kit Learn](https://scikit-learn.org/stable/) -->

## Bash commands


```{list-table}
:header-rows: 1

* - command
  - explanation
* - `pwd`
  - print working directory
* - `cd <path>`
  - change directory to path
* - `mkdir <name>`
  - make a directory called name
* - `ls`
  - list, show the files
* - `touch`
  - create an empty file
* - `echo 'message'`
  - repeat 'message' to stdout
* - `>`
  - write redirect
* - `>>`
  - append redirect
* - `rm file`
  - remove (delete) `file`
* - `cat`
  - concatenate a file to standard out (show the file contents)
```

## git commands
```{list-table}
:header-rows: 1

* - command
  - explanation
* - `status`
  - describe what relationship between the working directory and git
* - `clone <url>`
  - make a new folder locally and download the repo into it from url, set up a remote to url
* - `add  <file>`
  - add file to staging area
* - `commit -m 'message'`
  - commit using the message in quotes
* - `push`
  - send to the remote
* - `git log`
  - show list of commit history
* - `git branch`
  - list branches in the repo
* - `git branch new_name`
  - create a `new_name` branch
* - `git checkout -b new_Name`
  - create a `new_name` branch and switch to it
* - `git pull`
  - apply or fetch and apply changes from a remote branch to a local branch
* - `git commit -a -m 'msg'`
  - the `-a` option adds modified files (but not untracked)
```