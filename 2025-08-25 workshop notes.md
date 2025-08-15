# Live Transcription Notes

[Version Control with Git Workshop Page](https://imageomics.github.io/2025-08-15-osu-online/)

**Instructors**: 
- Matthew Thompson, PhD
- Elizabeth Campolongo, PhD

[Code of Conduct](https://docs.carpentries.org/policies/coc/)

---
## Topics to cover
**Navigating the Shell** (45m)
•	Introducing the Shell
•	Navigating Files and Directories
**Version Control with Git: Command Line** (70m)
•	Automated Version Control
•	Setting Up Git
•	Creating a Repository
•	Tracking Changes
•	Exploring History
•	Ignoring Things
**Version Control with Git: Remotes** (65)
•	Remotes in GitHub
•	Collaborating
•	Conflicts
•	Open Science
•	Citation

## Follow-up Links

Follow up links:
- [github ssh instructions](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)
- Carpentries [image conflicts example](https://swcarpentry.github.io/git-novice/instructor/09-conflict.html#conflicts-on-non-textual-files)
- [GitHub Projects](https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects) are particularly useful for relegating and tracking tasks within GitHub.
- Be sure to add a license to your repo, for information on options see [choosealicense.com](https://choosealicense.com/) or consult with your instution's copyright people.
- [CITATION.CFF](https://citation-file-format.github.io/): tell end-users or people building off your work how to cite it.


## Schedule

| Time              | Content                                  | Instructor  |
| --------          | --------                                 | --------    |
| 9:00-9:20 am      | Course intro and logistics               |             | 
| 9:20-10:05 am     | Navigating the Shell                     | Matt        | 
| 10:05-10:20 am    | Break                                    |             |
| 10:20-11:15 pm    | Version Control with Git: Command Line   | Matt        |
| 11:15-12:15 pm    | Lunch                                    |             |
| 12:15-2:50 pm     | Version Control with Git: Remotes        | Elizabeth   |

(will probably finish post-lunch session well before 2:50)


## Course intro and logistics


## Navigating the Shell

We get access to the operating system through the shell. Bash is the most popular shell.

In the shell, you see a line called the prompt:
```
$
```
In mac zsh the prompt is `%`

`ls` lists out all of the contents in current directory

`ls -F` adds a symbol at the end of each name based on what the file is, e.g.:
- `\` -> Dir
- `@` -> Symbolic link

`ls --help` or `ls -h` shows a help message listing all available options for `ls`, their meanings and sometimes with examples

You can also use `man` to open the manual viewer in Unix/Linux page mode without printing all into the shell
```
man ls
```

`clear` Clears the console output

## Navigating Files and Directories

`cd Desktop` Changes the working directory to `Desktop`

`cd ..` Changes the working directory up one level

`cd .` Stays at current level

`pwd` Prints out the current working directory

`ls -a` / `ls --all` list out all files in the current directory including the hidden files that starts with a dot 

Use the **Tab** key to auto-complete

`~` is the abbreviation for user home directory

`cd -` changes back to the previous directory

Relative and Absolute Paths are two ways of specifying a location in the filesystem
- Absolute: always starts from the **root directory** `/` and spells out the full path to a file or a directory. It does not depend on your where you are, and it's always valid. 
- Relative: describes a location **relative to your current working directory**. The meaning changes depending on where you currently are. 

```
ls -F my_folder      
# "my_folder" is an argument: the target directory
# -F is an option
```

`mkdir thesis` makes a new directory `thesis` in the current working directory

```
cd thesis # enter thesis directory
```

```
mkdir -p dir1/dir2/dir3
```
`mkdir -p ` Creates the specified directory and any missing parent directories in the path, example:

```
mkdir -p ../project/data/experiment1/sample1

ls -F -R ../project
```
```console=
../project:
data/

../project/data:
experiment1/

../project/data/experiment1:
sample1/

../project/data/experiment1/sample1:
```
`-R` stands for recursive. Combine options `ls -RF` works the same

Use the Up-arrow key to go back command history. 

Avoid naming directory with special symbols.

Naming conventions:
- `kebab-case`
- `CamelCase`
- `snake_case`

`nano` is the text editor of choice
```
cd ~/thesis
nano draft.txt
```

## Working With Files and Directories

`rm draft.txt` deletes the draft

`rm -r ~/project` deletes the folder

`cp [source] [destination]` copies files from source to destination

`mv [source] [destination]` moves files or dirs from source to destination

Most filenames are `something.extension`. The extension isn't required, can be any length, doesn't guarantee anything, but is used to indicate the type of data in the file.

# Version Control with Git

## Automated Version Control
Version control tracks changes as checkpoints to revert to.

Changes are tracked as their own entities: **commits**

Commit auto-tracked metadata:
- Unique identifier for the commit (its hash)
- Preceding commit (or commits for merges)
- Author
- File(s) and line number(s) changed
- Date created
- Type of change (added, modified, deleted, … )

The **Repository**:
A complete history of commits and their metadata for a project.

Takeaways:
- Version control is like an unlimited ‘undo’.
- Version control also allows many people to work in parallel.

## Setting Up Git

Things to configure the first time we use git so it knows some of our preferences and a little about us for tracking and repository authentication:
- name & email
- preferred text editor
- to use settings globally (for all the projects we do on this computer in this user account)

Git command structure:

```
git verb option
git: 'verb' is not a git command. See 'git --help'.

The most similar commands are
        grep
        revert
```

```
git --help
```

### Setting up name & email

```
git config --global user.name "YOUR NAME"
git config --global user.email "your@email"

# Pivrate email address to prevent information leakage
git config --global user.email "<your-username>@users.noreply.github.com"
```

If you are on a Linux or macOS machine:
```
git config --global core.autocrlf input
```
If you are on a Windows machine:
```
git config --global core.autocrlf true
```

### Setting up default editor
```
git config --global core.editor "nano -w"
```

### Setting up default branch name

```
git config --global init.defaultBranch main
```

To view and edit the current config 
```
git config --global --edit
```
To just view it
```
git config --list
```

## Creating a Repository

```
cd ~/Desktop
mkdir planets
cd planets/
```
Now, make the `planets/` directory into a Git repository.
```
git init
```
Check what's changed in the repo using `ls`

Use the `-a` flag to see hidden contents
```
ls -a 
```
```console=
.  ..  .git
```

Make a new branch
```
git checkout -b main
# Switched to a new branch 'main'
```

`git status` gives the state of our repository
```console=
On branch main

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

```
cd ~/Desktop/planets
mkdir moons && cd moons
git init
```

```
cd ~/Desktop/planets
rm -rf moons/.git
```

`rm -rf target_dir` Deletes `target_dir` and everything inside it, without asking.

### Tracking Changes

```
cd ~/Desktop/planets
nano mars.txt
```
Save & Exit: Ctrl + O, press enter, Ctrl + X
```
Cold and dry, but everything is my favorite color.
```

Check the file's contents:
```
cat mars.txt
```
Check the git status
```
$ git status
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        mars.txt

nothing added to commit but untracked files present (use "git add" to track)
```
It says the `mars.txt` is untracked. Track the changes `mars.txt`
```
git add mars.txt
```
Check the git status again
```
$ git status
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   mars.txt
```
Now commit changes
```
$ git commit -m "Start notes on Mars as a base"
[main (root-commit) adcc37d] Start notes on Mars as a base
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 mars.txt
```
Check the git status again
```
$ git status
On branch main
nothing to commit, working tree clean
```

Get information about recent activity
```
$ git log
commit a6a6cf6cb409e5743c9530bde0870cfd9a8d30e7 (HEAD -> main)
Author: Matt Thompson <thompson.4509@osu.edu>
Date:   Fri Sep 8 20:53:29 2023 -0400

    Start notes on Mars as a base
```

Adding more

```
nano mars.txt
```
Save & Exit: Ctrl + O, press enter, Ctrl + X
```
The two moons may be a problem for Wolfman.
```
Print the new content
```
cat mars.txt
```
Use `git diff` to review the specific changes that were made:
```
$ git diff
warning: in the working copy of 'mars.txt', LF will be replaced by CRLF the next time Git touches it
diff --git a/mars.txt b/mars.txt
index 077071c..42d92e3 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1 +1,2 @@
 Cold and dry, but everything is my favorite color.
+The two moons may be a problem for Wolfman.
```

Commit only works on changes that are tracked/staged

```
git add mars.txt
```
Now create a new commit
```
$ git commit -m "Note Wolfman's concern about moons"
[main 77a852d] Note Wolfman's concern about moons
 1 file changed, 1 insertion(+)
```


Now add another change to `mars.txt`

```
nano mars.txt
```

Save & Exit: Ctrl + O, press enter, Ctrl + X

```
But the Mummy will appreciate the lack of humidity.
```

Check the diff
```
git diff
warning: in the working copy of 'mars.txt', LF will be replaced by CRLF the next time Git touches it
diff --git a/mars.txt b/mars.txt
index 42d92e3..2a282ee 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1,2 +1,3 @@
 Cold and dry, but everything is my favorite color.
 The two moons may be a problem for Wolfman.
+But the Mummy will appreciate the lack of humidity.
```

Track the changes
```
git add mars.txt
```

`git diff` checks the difference between the active working directory and the staging area

```
git diff # no output after staging
```

`git diff --staged` shows the difference between the last commit and what's staged.
```
$ git diff --staged
diff --git a/mars.txt b/mars.txt
index 42d92e3..2a282ee 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1,2 +1,3 @@
 Cold and dry, but everything is my favorite color.
 The two moons may be a problem for Wolfman.
+But the Mummy will appreciate the lack of humidity.
```
Commit changes
```
git commit -m "Discuss concerns about Mars' climate for Mummy"
[main dd60e0b] Discuss concerns about Mars' climate for Mummy
 1 file changed, 1 insertion(+)
```

Check new git status and log
```
$ git status
On branch main
nothing to commit, working tree clean
```

```
git log
commit dd60e0b8a2663937cba57fde442fd8ede011196d (HEAD -> main)
Author: Matt Thompson <thompson.4509@osu.edu>
Date:   Sat Sep 9 08:11:18 2023 -0400

    Discuss concerns about Mars' climate for Mummy

commit 77a852d8eb4168ab1d4a74faf9a84d91c050ba82
Author: Matt Thompson <thompson.4509@osu.edu>
Date:   Fri Sep 8 21:22:13 2023 -0400

    Note Wolfman's concern about moons

commit a6a6cf6cb409e5743c9530bde0870cfd9a8d30e7
Author: Matt Thompson <thompson.4509@osu.edu>
Date:   Fri Sep 8 20:53:29 2023 -0400

    Start notes on Mars as a base
```

`git log` has lots of options for giving useful information and exploring the history:
- `git log -1`: just the last commit
- `git log --oneline`: show history with each commit condensed into one line
- `git log --graph`: show the DAG
- You can combine these options as long as they make sense: `git log --oneline --graph -1`

### Directories
Git doesn't track empty directories.
```
mkdir spaceships
git status
```
Makes a hidden placeholder file within the new directory
```
cd spaceships
touch .placeholder 
```

```
cd ..
git add spaceships
```

```
$git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   spaceships/.placeholder
```

```
touch spaceships/apollo-11
touch sputnik-1
rm spaceships/.placeholder
```
```
$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   spaceships/.placeholder

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    spaceships/.placeholder

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        spaceships/apollo-11
        sputnik-1
```

```
$ git add spaceships
$ git commit -m "Add some initial thoughts on spaceships."
[main cc39807] Add some initial thoughts on spaceships.
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 spaceships/apollo-11
```

Key commands for so far for this section
```
git status   # Show current branch, staged/unstaged changes, and untracked files
git log      # View commit history
git diff     # Show changes not yet staged (or differences between commits if specified)
git add      # Stage file changes for the next commit
git commit   # Save staged changes as a new commit in the repository
```

#### Exercises for Tracking Changes Episode (4)
[[#Episode 4 - Tracking Changes]]
[[#AE) Episode 4 - Tracking Changes]]

>[!question] 1. **Choosing a Commit Message:**  Which of the following commit messages would be most appropriate for the last commit made to `mars.txt`? 
	1. “Changes”
	2. “Added line ‘But the Mummy will appreciate the lack of humidity’ to mars.txt”
	3. “Discuss effects of Mars’ climate on the Mummy”
> [!answer]-
> 1. ❌Answer 1 is not descriptive enough, and the purpose of the commit is unclear; 
> 2. ❌ Answer 2 is redundant to using “git diff” to see what changed in this commit; 
> 3. ✅ Answer 3 is good: short, descriptive, and imperative.

> [!question] 2. **Committing Changes to Git:** Which command(s) below would save the changes of `myfile.txt` to my local Git repository?
> ```
> $ git commit -m "my recent changes"
> ```
> ```
> $ git init myfile.txt
> $ git commit -m "my recent changes"
> ```
> ```
> $ git add myfile.txt
> $ git commit -m "my recent changes"
> ```
> ```
> $ git commit -m myfile.txt "my recent changes"
> ```

> [!answer]-
> 1. ❌ Would only create a commit if files have already been staged.
> 2. ❌ Would try to create a new repository.
> 3. ✅ Is correct: first add the file to the staging area, then commit.
> 4. ❌ Would try to commit a file “my recent changes” with the message myfile.txt.


### Explore History

```
cd ~/Desktop/planets
nano mars.txt
```
```
An ill-considered change.
```

See the difference between current directory and an old commit
```
git diff HEAD~3 mars.txt
```
To see what the diff was at that point in time 
```
git show HEAD~3 mars.txt
```

"HEAD" refers to the most recent commit. We can refer to the commits explicitly by their commit IDs (first 7 chars or more)

```
git log
<copy commit ID>
git diff <commit ID> mars.txt
```

```
git log --online
```
Restore specific files back to stages previously
```
git restore --source=<comit ID> mars.txt
```

### Igoring things


There are files in our working directory we don't want Git to track, such as:
- .DS_Store
- intermediate analysis files
- Slurm scripts
- A large directory full of data
- cache

We can specify these files and folders in a special file in the repo root: `.gitignore`


```
cd ~/Desktop/planets
mkdir results
touch a.dat b.dat c.dat results/a.out results/b.out
```

```
$ git status
(cardinal_inference) [netzhang@cardinal-login04 planets]$ git status
On branch main

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        a.dat
        b.dat
        c.dat
        results/
        sputnik-1

no changes added to commit (use "git add" and/or "git commit -a")
```

Create a `.gitignore` file
```
nano .gitignore
```
```
*.dat        
results/
```
```
$ git status
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore
```
We should add and commit `.gitignore` so it stays with all versions of the repo.
```
git add .gitignore
git commit -m "Ignore data files and the results folder"
```
We can't add things included in the `.gitignore` file
```
git add a.dat
The following paths are ignored by one of your .gitignore files:
a.dat
hint: Use -f if you really want to add them.
hint: Turn this message off by running
hint: "git config advice.addIgnoredFile false"
```

`git add .` Adds all new changes in your git repo. Check what's ignored 
```
$ git add .
$ git status --ignored
On branch main
Ignored files:
 (use "git add -f <file>..." to include in what will be committed)

        a.dat
        b.dat
        c.dat
        results/

nothing to commit, working tree clean
```


---

## Afternoon Session: Git Remotes with GitHub

### Connect to Remote
Navigate to github page in your web browser
```
https://github.com/<gh_username>
```

Click New Repository
- repo name: `planets-08-25`
- Choose visibility: public/private

On GitHub this is equivalent to 

```
$ mkdir planets
$ cd planets
$ git init
```

Check ssh connection
```
$ ssh -T git@github.com
Hi <gh_username>! You've successfully authenticated, but GitHub does not provide shell access.
```

In your terminal
```
git remote add origin git@github.com:<github-username>/<repo_name>.git
git branch -M main
git push -u origin main
```
Now our local copy of main is associated with the remote GitHub repo . 
show all remotes configured to the local repo.
```
$ git remote -v
origin  git@github.com:<gh_username>/planets-08-25.git (fetch)
origin  git@github.com:<gh_username>/planets-08-25.git (push)
```
If you're using HTTPS mode, you will see something like:
```
$ git remote -v
origin  https://github.com/thompsonmj/planets.git (fetch)
origin  https://github.com/thompsonmj/planets.git (push)
```


Now that the repos have been properly introduced, let's copy our local work to the remote rep

```
git push origin main
```

Refresh the repo page to make sure local repo is pushed to remote.

```
git diff <commit_hash>
```

```
git checkout main
```

To get changes from remote
```
git pull origin main
```
There's noting to update for now. 

### Collaborating

Open two terminals to simulate collaboration. 

In the wolfman terminal, clone the repo from remote

```
$ cd ~
$ git clone git@github.com:<github-username>/planets-08-25.git ~/<desired-path>/wolfman-planets
Cloning into 'wolfman-planets'...
remote: Enumerating objects: 9, done.
remote: Counting objects: 100% (9/9), done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 9 (delta 0), reused 9 (delta 0), pack-reused 0 (from 0)
Receiving objects: 100% (9/9), done.
```

We now have three copies
- original
- remote
- wolfman

Now navigate to the newly cloned wolfman copy

```
cd <path-to-repo>/wolfman-planets
```

Wolfman makes a new file

```
nano pluto.txt
```
```
It is so a planet!
```
ctl-o, ctrl-x

Push the new file to remote repo
```
git add pluto.txt
git commit -m "Add notes about Pluto."
git push origin main
```
Refresh the remote repo in the browser to valdiate the changes. 

Go to the vlad (original) repo to sync the changes
```
cd <path-to-vlad>
```

```
git fetch origin main
```
To see the changes, run:
```
git diff main origin main
```
Merge these changes
```
git pull origin main
```
Now all three repos are in sync

### Conflicts

Come back to wolfman repo

```
cd <path-to-repo>/wolfman-planets
```

Now wolfman adds a line

```
nano mars.txt
```
```
This line added to Wolfman's copy.
```
Update this change to remote
```
git add mars.txt
git commit -m "Add a line in our home copy."
git push origin main
```

Now Vlad wants to make a change. Go to Vlad's terminal
```
nano mars.txt
```
```
We added a different line in the other copy.
```
Stage & Commit this change locally
```
git add mars.txt
git commit -m "Add a line in my copy."
```
Now let's push Vlad's changes to GH remote repo. Vlad got rejected.

Git has rejected the push because it sees there are changes in the remote that haven't be incorporated into the local branch. We have to pull the updates and merge them into the local repo, then push that update.

```
git pull origin main
```
We not see a merge conflict

```
cat mars.txt
```

Observe that `<<<<<<< HEAD` is placed above our changed line, which is separated by a string of `=` from the conflicting line from the remote, followed by more carats and the commit containing the conflict.

Choose how to address this conflict

Let's delete both and replace the line with

```
We removed the conflict on this line.
```

Now stage the change
```
git add mars.txt
```
Check `git status`

```
git commit -m "Merge changes from GitHub."
git push origin main
```

Go to wolfman termnial, and pull from remote repo
```
git pull origin main
```

Takeaway:

Conflicts occur when two or more people change the same lines of the same file.

The version control system does not allow people to overwrite each other’s changes blindly, but highlights conflicts so that they can be resolved.

Conflict resolution costs time and effort. If you find yourself resolving a lot of conflicts in a project, consider these technical approaches to reducing them:
- Pull from upstream more frequently, especially before starting new work.
- Use topic branches to segregate work, then submit pull requests for review before merging to main.
- Make smaller more atomic commits
- Push your work when it is done and encourage your team to do the same to reduce work in progress and, by extension, the chance of having conflicts.
- Where logically appropriate, break large files into smaller ones so that it is less likely that two authors will alter the same file simultaneously.

Conflicts can also be minimized with project management strategies:
- Clarify who is responsible for what areas with your collaborators.
- Discuss what order tasks should be carried out in with your collaborators so that tasks expected to change the same lines won’t be worked on simultaneously.
- [GitHub Projects](https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects) are particularly useful for relegating and tracking tasks within GitHub.


### Follow up links:
- [Collaborative Science Guide](https://imageomics.github.io/Collaborative-distributed-science-guide/): guides to workflows, documentation, and general best-practices for collaborative science. Template site based on Imageomics Guide (co-developed)---Most of this guide is applicable to anyone working more broadly in the field of imageomics or adjacent fields of computer and data science, and it is tailored to help domain scientists bridging that gap.
  - Covers many topics mentioned in this workshop in greater detail with examples. 
- [The Turing Way](https://book.the-turing-way.org/): broad-spectrum community handbook for open science.
- [github ssh instructions](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)
- Carpentries [image conflicts example](https://swcarpentry.github.io/git-novice/instructor/09-conflict.html#conflicts-on-non-textual-files)
- [GitHub Projects](https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects) are particularly useful for relegating and tracking tasks within GitHub.
- Be sure to add a license to your repo, for information on options see [choosealicense.com](https://choosealicense.com/) or consult with your instution's copyright people.
- [CITATION.CFF](https://citation-file-format.github.io/): tell end-users or people building off your work how to cite it.
