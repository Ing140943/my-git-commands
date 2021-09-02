## 7. Commands for Remotes

1. To list all your remote repositories, with their URL, use:
   ```
   $ git remote -v 
   ```
2. To view details about a rempote repo named `origin`, including all the remote banches and local tracking branches for `origin` is:
   ```
   $ git fetch origin
   ```

3. You commit some files to `dev-foo` and try to "push" them to Github, but it fails:

   ```
   $ cmd>  git checkout dev-foo
   $ cmd>  git push
   fatal:  The current branch dev-foo has no upstream branch. 
   ```
   Explain this error.  
    This error occurs because we create a new branch on the remote but we haven't configured `git`.  So we are only creating a new branch on the local computer.

4. What is the command to push `dev-foo` to `origin` as a new remote branch on `origin`?
   ```
   $ git push -u origin dev-foo
   ```


5. Suppose your remote repository (Github or `origin`) has a branch named `beverages` that you don't have in your local repository.  What is the command to create a new local branch as a copy of the remote `beverages` branch that **tracks** the remote branch?
   - There are many commands that do this.  You can show one or more than one.
   ```
   $ git fetch origin

   $ git branch --track beverages_copy origin/beverages
   ```


6. Consider this situation:
   - you have a local repository including a README.md file.
   - Your local repo is up-to-date with a remote Github repo (has identical README.md)
   - You edit README.md on Github using Github's web interface and save the changes.
   - On your local machine, you edit README.md, commit the changes and push it to Github.    
   What happens when you push? Explain why.     
    It will failed because the information on local is not the same as the information on the remote repository.


7. Suppose you want to move "origin" to a different URL. This can happen when:
   - you change the name of the repo on Github
   - you transfer ownership to someone else
   - you want to move from Github to another site, like Bitbucket
   What is the command to change the URL of "origin" `to https://github.com/newuser/newreponame`
   ```
   $ git remote set-url origin https://github.com/newuser/newreponame
   ```



8. You want to have a *second* remote repository for your work on Bitbucket.  What is the command to add a remote named "bitbucket" with the URL "https://bitbucket.org/your-username/git-commands"
   ```
   $ git remote add bitbucket https://bitbucket.org/your-username/git-commands
   ```

   - What is the command to push the master branch to "bitbucket"?
   ```
   $ git push bitbucket master
   ```




> This actually works.
> Since you already have code in your local repo, you should create an *empty* repo on Bitbucket and "push" to it to copy all your work.
