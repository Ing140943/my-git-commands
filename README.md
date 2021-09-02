## Using Git

| Contents about Git             |
|--------------------------------|
|[1. Basics](#1-basics)    |
|[2. Adding and Changing Things](#2-adding-and-changing-things) |   
|[3. Undoing Changes](#3-undoing-changes)     |
|[4. Branch and Merge](#4-branch-and-merge)   |
|[5. Viewing Commits](#5-viewing-commits)  |
|[6. Remote Origin](#6-remote-origin)   | 
|[7. Commands for Remotes](remote-commands.md)|
[Resources](#resources)

### Note on Paths

In this file, directory paths are written with a forward slash as on MacOS, Linux, and the Windows-Bash shell: `/dir1/dir2/somefile`.    
For the MS Windows command prompt, when using the command substitute a backslash: `\dir1\dir2\somefile`.


## 1. Basics

1. When working with Git locally, what are these?  Describe each one in a sentence
   * Staging area -    The staging area is a file that stores information that are goint to be a part of the next commit.
   * Working copy -    The copy of files that we can view and edit can be both tracked and untracked files.
   * master -          The standard name of default git branch.
   * HEAD -            It is the symbolic name for the current commit.

2. A git commit includes the author's name and email.  When you install git on a new machine (or in a new user account) you should perform these 2  git commands to tell git your name and email:
   ```
   # Git configuration commands for a new account

   $ git config --global user.name "username"
   $ git config --global user.email your email

   ```
3. If you want to specify a **different** name and email for a single project (instead of the global values in Item 2 above), in the working directory of that repository enter:
    ```
    # Configuration commands for a single repository

    $ git config --local user.name "username"
    $ git config --local user.email your email

    ``` 
4. There are 2 ways to create a local Git repository.  What are they?
   - The first way is our code is on local computer and we want to put it to github. So there are 5 steps for doing this way.

     1. We have to create a local git repository.
     2. Create an empty repository on github.
     3. Copy the URL of the new Github repository (you can choose either HTTPS or ssh).
     4. Add Github remote repository named "origin" in your local project.
     5. Push the local repository to Github. (We use ``` git push -u origin master ``` only first time then just type ``` git push ```)

   - The second way is to create your local repository on Github. Then type ```git clone``` follows by the Github project URL. If we want to push
    our work to Github just type ```git push```

5. When you create a git repository in a directory named "/project1" by entering `git init`, Git will create a "hidden" directory for the local repository.  Where is the directory for this local repository (write the full path of the repository)?

    It is in the project1 repository. Path: /project1/.git


## 2. Adding and Changing Things

Suppose your working copy of a repository contains these files and directories:
```
README.md
out/
    a.exe
src/a.py
    b.py
    c.py
test/
    test_a.py
    ...
```     

1. What is the command to add README.md and *everything* in the `src` directory to the git staging area?
   ```
   # Git commands for add README.md and everything in the src

   $ git add README.md
   $ git add src

   ```
2. Write the command to add `test/test_a.py` to the staging area (but not any other files).
   ```
   # Git commands for add test/test_a.py

   $ git add test/test_a.py

   ```
3. Write a command to list the files in the staging area.
   ```
   # Git commands for listing the file in staging area

   $ git status

   ```
4. You decide you **don't** want to commit `test/test_a.py` to git.  The command to remove `test/test_a.py` from the staging area is:
   ```
   # Git commands for remove test/test_a.py from staging area

   $ git rm --cached test/test_a.py

   ```
5. The command to commit everything in the staging area to the repository is:
   ```
   # Git commands commit everything in the staging area to the repository

   $ git commit

   ```
6. You **never** want any files in the `out/` directory to be added to git. Describe 2 steps to configure the repo so git always ignores files in the `out/` directory:
   - step one: Create the ```.gitignore``` file in your directory.
   - step two: Add the names or patterns for files and directories that git should ignore.
7. What is the command to move `a.py`, `b.py`, and `c.py` from the `src` directory to the top-level directory of the project, so that they will also be moved in the git repository?
   ```
   # Git commands to move a.py, b.py, and c.py from the src directory to the top-level directory of the project

   $ git mv src/a.py ./a.py
   $ git mv src/b.py ./b.py
   $ git mv src/c.py ./c.py
   $ rm src
   $ git add .
   $ git commit -m "Move file out from the src"
   $ git push
   
   ```
8. Commit this change with the message "moved src directory":
   ```
   $ git commit -m "moved src directory"

   ```
9. To add **all changed files** (but not untracked files) to the stagin area using a single command, enter:

    (After doing this you should use "git status" to verify you didn't add unintended files.)
   ```
   $ git add -u

   ```
10. To **delete** the file `c.py` from your working copy **and** the repository, enter these two commands:
   ```
   # Git command to delete c.py from the working copy and the repository
   
   $ git rm c.py
   $ git commit -m "Delete c.py from repository"

   ```


## 3. Undoing Changes

1. To see the differences between your working copy of `a.py` and the `a.py` in the local repository (current version in the repo) enter:
   ```
   $ git diff a.py

   ```
2. If you decide you don't like the changes to `a.py`, what is the command to **replace** your working copy of `a.py` with the most recent (HEAD) version in the repository?    
   (This also works if you accidentally *delete* a file from your working copy.)
   ```
   $ git checkout HEAD a.py

   ```
3. How do you "undo" a commit? Suppose you want to **discard** some commits and move both HEAD and "master" to an earlier commit (so you can continue working from that commit).  Suppose the commit graph looks like this:
   ```
   aaaaa ---> bbbbb ---> ccccc ---> ddddd [HEAD -> master]
   ``` 
   What are the commands to do this:
   - show all the commits and commit messages so you can find the one you want
      ```
      $ git rev-list --all --remotes --pretty

      ```
   - move HEAD and master to the commit with id bbbbb
      ```
      $ git checkout master
      $ git reset --hard <commit_id>

      ```


## 4. Branch and Merge

1. What is the command to create a new branch named `dev-foo`?
   ```
   $ git branch dev-food

   ```
2. The command to display the name of your current branch is:
   ```
   $ git branch --show-current
   
   ```
3. To list the names of **all** branches, including remote branches, enter:
   ```
   $ git branch -a

   ```
4. To switch your working copy to the branch named `dev-foo` enter:
   ```
   $ git checkout dev-foo

   ```
5. The steps to merge the work from `dev-foo` into the master branch are:
   - write a brief description, with git commands
      First we have to go to master branch by type ```git checkout master```. Then you have to make sure that this file on your master branch is now currently if it not just type ```git pull```(This way is reduce to occur conflict in our merging). Then type ```git merge dev-foo``` to merge dev-foo branch to master.

6. Describe under what conditions a merge may fail.
    It will fail if our branches is conflict. The conflict means that the same file of 2 branches at the same point, there is some differences between them. So we have to choose which part of this code from which branch should be merge.



## 5. Viewing Commits

1. To show the history of a repository in the terminal (command) window, using one line per commit is:
   ```
   $ git log --oneline --graph
   ```
    Some versions of git have an *alias* "log1" for this (`git log1`).

2. To show the history (as above) including all branches in the repository, use:
   ```
   $ git log --oneline
   ```

3. To list all the files in the current branch of the repository, enter:
   ```
   $ git ls-files
   ```

## 6. Remote Origin

1. To view details about a rempote repository named origin, including all the remote banches, and local tracking branches.
   ```
   $ git remote show origin
   ```

---
## Resources

Git Exercise:

[Learn Git Branching](https://learngitbranching.js.org/) the web exercise for practice using git      
[Git Exercise](https://www.w3schools.com/git/git_exercises.asp) exercise for very basic git from W3schools

Learn Git:

[Pro Git Online Book][ProGit] best source for Git. Ch. 2 & 3 contain the essentials. Free e-book download available.     
[Visual Git Reference](https://marklodato.github.io/visual-git-guide) one page with illustrations of git commands.

Try Git:

[Learn Git Interactive Tutorial][LearnGitInteractive] excellent visual tutorial.   
[Git Visualizer][VisualizeGit] execute Git commands and see the results as a graph.    

[ProGit]: https://www.git-scm.com/book/en/v2 "Pro Git online book on Git-scm.com"
[ProGitPdf]: https://progit2.s3.amazonaws.com/en/2016-03-22-f3531/progit-en.1084.pdf "Pro Git v.2 PDF on AWS. Longer, book format."
[LearnGitInteractive]: https://learngitbranching.js.org "Interactive graphical git tutorial"
[VisualizeGit]: http://git-school.github.io/visualizing-git/ "Online tools draws a graph of commits in a repo as you type"
