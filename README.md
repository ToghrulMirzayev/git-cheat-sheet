# GIT CHEAT SHEET

<p align="left"> <a href="https://www.python.org" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/1119b9f84c0290e0f0b38982099a2bd027a48bf1/icons/git/git-original.svg" alt="python" width="200" height="200"/>

## Basic GIT commands

* You want to clone repository from remote to your local
```
git clone https://github.com/<username>/<repo name.git>
```

* You want to stage your changes
  * stage all files
    ```
    git add .
    ```
  * stage exact particular file
    ```
    git add <file name>
    ```
    
* You want to commit your changes
```
git commit -m "message that describe your changes"
```

* You want to push your changes to remote repository
  * To push changes to the default branch which is matching to your local branch name
    ```
    git push
    ```
  * To push changes to the particular remote branch that is not matching your local branch name
    ```
    git push origin <branch-name>
    ```

* You want to pull new changes to your local repository
  * To pull changes from the default branch which is matching your local branch name
      ```
      git pull
      ```
  * To pull changes from the particular remote branch that is not matching your local branch name
    ```
    git pull origin <branch_name>
    ```

* You want to check status of files in your branch
```
git status
```

* You want to configure your account details
  * add username
  ```
  git config --global user.name "name surname"
  ```
  * add email
  ```
  git config --global user.email "email"
  ```

## Branches

* You want to check all branches in your local repository \
`Note`: `*` pointed to the branch on which you are working right now
```
git branch
```

* You want to create new branch
```
git checkout -b <branch-name>
```

* You want to switch to another branch
```
git checkout <branch-name>
```

* You want to check all remote branches
```
git branch -r
```

* You want to check new branches created by your teammates that you don't have on your local
```
git fetch origin
```

* You want to merge branches through commandline
```
git merge <branch-name>
```

# Temporarily saving changes in your working directory

* You already implemented code, but you want to pull remote changes before pushing your local changes \
Please follow below commands to use `stash` command
  * Save your local changes
  ```
  git stash
  ```
  * Pull new changes from remote repository
  ```
  git pull
  ```
  * Add your local changes to the newest version of code
  ```
  git stash pop
  ```

# Rollback changes both locally and remotely

* You want to reset your local changes \
Follow below steps:
  * get logs with standard command
  ```
  git log
  ```
  * get logs prettified in one line and with special format
  ```
  git log --pretty=format:"%h - %s : %ad [ %an ]" --date=short 
  ```
  * Reset your local changes to particular commit
  ```
  git reset --hard <commit-hash>
  ```

* You already pushed your changes to remote branch and want to reset it as well \
Assuming you already done resetting in your local. Do below command to set the same commit as a HEAD in your remote branch
```
git push origin HEAD --force
```

# Data recovery

* You want to execute data recovery \
Follow below steps:
  * The first step in data recovery is to identify the commit where the data was last known to be correct. Use below command to view the commit history and identify the commit hash associated with the correct data
  ```
  git log
  ```
  * Next, create a new branch from the identified commit to ensure that you don't overwrite any existing data. Use below command to create a new branch and switch to it.
  ```
  git checkout -b recovery-branch <commit-hash>
  ```
  * Once you have created the recovery branch, you can restore the deleted or modified data from the identified commit. You can use the git checkout command with the path to the file or directory that you want to restore.
  ```
  git checkout <commit-hash> -- <path/to/file-or-directory>
  ```
  * After restoring the data, you need to commit the changes to the recovery branch and push them to the remote repository \
  To do that please refer to related set of commands
  * Now you can even merge the changes with main branch
  To do that please refer to related command

## Tagging branches

* You want to tag your branch \
Please follow below steps then:
  * Switch to branch that to be tagged
  ```
  git checkout <branch-name>
  ```
  * Tag your branch
  ```
  git tag -a <tag-name> -m "<tag-message>"
  ```
  * Push tag
  ```
  git push origin <tag-name>
  ```

# Patch applying 

* You want to apply the patches \
Follow below steps
  * Make sure you are on the branch that contains the changes you want to create patches for. \
  Use below command to list all branches and see the branch on which you are working right now. It will be indicated by `*`
  ```
  git branch
  ```

  * Generating patches can be done in different ways. Let's see 2 options below: 
    * Patch for range of changes
    ```
    git format-patch <commit-range> --output-directory=<output-dir>
    ```
    `Notes`:
    Replace `<commit-range>` with the commit range for the changes you want to create patches for. For example, to create patches for the changes in the last 3 commits, you can use `HEAD~3..HEAD` as the commit range. 
    Replace `<output-dir>` with the directory where you want to save the patches.
    * Single patch file
    ```
    git format-patch -1 <commit-hash> --output-directory=<output-dir>
    ```
    `Note:`
    In above example we are going to do the same for single change

  * To apply patches do below sub-steps:
    * Change to the repository where you want to apply the patches using below command
    ```
    git checkout <branch-name>
    ```
    * Now you can apply patches that wew generated by below command
    ```
    git am <path-to-patch>
    ```
    `Note:`
    Replace <path-to-patch> with the path to the patch file you want to apply
