# Git

Git is the most widely used [version control](Version%20Control.md) system in the world. It was created by Linus Torvalds, the creator of the [Linux](Linux.md) kernel, back in 2005. Today, most software projects, both commercial and open source, rely on Git for version control and it integrates well into many operating systems as well as text editors and IDEs.

Git is designed on a distributed architecture, meaning that rather than the version history being stored on only one single place, every copy of a repository also contains the history of all changes.

# Terminology

## Repository

A repository (repo) is just a folder (usually the root folder of your project) which contents are being tracked by Git. This folder contains all the files, sub-folders and metadata of the project.

## Commit

A commit is a snapshot of the state of all files inside the repo after some changes have been made.

## Remote

A remote is a link from your local repo to a remote repo which is usually stored on a server. Most remotes are stored on online platforms like [GitHub](https:github.com) or [GitLab](https:gitlab.com). A remote allows for an online backup of your code and has many benefits for collaboration.

# Basic Git commands

- `git init`: Initialises a new repo in the current folder
- `git clone <url>`: Clones the remote repo at `<url>` to your local machine
- `git remote add origin <link>`: Adds a new remote at `<link>` to your local repo

---

- `git status`: Shows all modified files in the current repo
- `git add <file>`: Adds `<file>` to the next commit
- `git reset <file>`: Removes `<file>` from next commit
- `git commit -m "<msg>"`: Creates a new commit with `<msg>` as information
- `git log`: Shows the commit history on the current branch

---

- `git branch <branch_name>`: Creates a new branch
- `git checkout <branch_name>`: Switches to the selected branch
- `git branch -d <branch_name>`: Deletes the selected branch
- `git checkout -b <branch_name>`: Shortcut to create a new branch and switch to it

---

- `git push`: Pushes all local commits to the remote
- `git pull`: Pulls all changes on the remote to the local repo