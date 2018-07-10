**Git Cheat sheet**

**Generic Terms:**\
**Pull**: sync b/w local and remote repository\
**Push**: Copies from local to remote permanently\
**HEAD**: Pointer to latest commit.


**Git Configuration**:\
check either in _/etc/gitconfig_ or  _$HOME/.gitconfig_

**To configure your git repository on workstation**
```
$ git config --global user.name "xxxx"
$ git config --global user.email "xxxx"
$ git config --global branch.autorebase always  // Avoids merge conflicts
$ git config --list  // View rest of the configurable options
```

**Creating new repository at Git Server**
```
$ mkdir project.git
$ cd project.git
$ git --bare -init
Add ssh keys of user to authorized_key
On Client Workstation
$ git remote add origin gituser@git.server.com:project.git

```
**Git Commands:**
- **See the current status of working git directory**
```
$ git status 
// ?? Filename --> New file, not yet added to staging area
// A Filename --> Added to staging area

```
- **Get details of a particular commit**\
`$ git show commit-id  `
                 
- **Add modified file to staging area**\
`$ git add .  (or) git add filename`

- **Commit Commands**
```
$ git commit -a -m         // git add + git commit -m 
$ git commit --amend   // combines the staged changes with previous commit and replaces 
                                     // previous commit with resulting snapshot
```

- **To halt current work, but keep a record of modified data. Takes modified tracked files, stage changes and save them on stack of unfinished changes that you can reapply**
```
$ git stash list
$ git stash                             // tracked modifications
$ git stash -u                        // untracked + tracked
$ git stash -a                       // untracked + ignored
$ git stash save msg          // msg helps in case of multiple stashes
$ git stash pop                  // To pop out saved changes in stack, done normally after git pull 
$ git stash pop stash@{2}   // Specific stash to be popped out
$ git stash drop stash@{2}
$ git stash clear

```
- **Log operations:**
```
$ git log -n limit
$ git log --oneline
$ git log --stat
$ gt log --grep="pattern"

```
- **Removing untracked files from working git directory**\
`git clean
`
- **Working with remotes**
```
$ git remote -V
$ git remote add <name> <url>
$ git branch -r  // List all remote branches
$ git pull         //  git fetch + git merge
$ git push <remote> <branch> // e.g. git push origin master, remember git clone automatically creates 
                                                   // a remote connection called origin
$ git remote show <remote>  // e.g.  git remote show origin
```

- **Working with branches**
```
git checkout <branch-name> // checks out remote branch in working directory
git checkout -b <branch-name> // create a new directory
```

_Remember before changing branch git forces you to commit or stash any changes in working directory
When we checkout a particular commit "$ git checkout commit-id" a detached branch is created._

-  **Resetting changes of working directory not yet shared with anyone (e.g  local commit not pushed to origin yet)**
```
$ git reset HEAD --soft  --> Stage snapshot and working dir are not altered
$ git reset HAED --hard --> Staged and work dir both updated to match specific commit (changes in working dir discarded)
$ git reset HEAD --mixed --> Work dir not affected, staged snapshot is updated to match specific commit. This is default behavior (changes preserved in working dir but not marked for commit)

```
- **Undo a commit and redo**
```
$ git commit -m "Something terribly misguided"
$ git reset HEAD~                          
<< edit files as necessary >>                        
$ git add .                  
$ git commit -c ORIG_HEAD     
```                             

- **File level and commit level operations:**
```
$ git reset  --> commit-level  --> Throw away changes in private branch
$ git reset   --> File-level --> Unstage the file
$ git checkout --> commit-level --> Switch branch or inspect old snapshot
$ git checkout --> File level --> Unstage  + discard changes 
$ git revert  --> commit level --> Undo commit in a public branch
$ git revert --> File level --> Not Applicable
```

- **Working with Forks**:\
Keeping your forked repository in sych with the original repository 
```
$ git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git
$ git fetch upstream
$ git checkout master
$ git merge upstream/master
$ git push
```
