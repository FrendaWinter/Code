# Git

Status: Not started

```powershell
# Remove file change
git checkout HEAD^ /path/to/file or git checkout HEAD~2 /path/to/file
git commit --amend
git push -f

# Revert a merged commit (has been merged already)
git revert -m 1 <commit-hash> 
git push -u origin <branch>

# Ref link https://stackoverflow.com/questions/7099833/how-do-i-revert-a-merge-commit-that-has-already-been-pushed-to-remote

# Unmerge one commit
git reset --hard HEAD~1

git config --global user.name "Manh Duong"
git config --global user.email "manh.duong@opswat.com"

git config --local user.email "gaconnoone1999@gmail.com"
git config --local user.name "Frenda Winter"

git commit --amend --author="Frenda Winter <gaconnoone1999@gmail.com>"

# Git blame from line to line
git log -u -L <upperLimit>,<lowerLimit>:<path_to_filename>

# Choose version of file when merge
git checkout --ours B
git checkout --theirs B

```

```powershell
# Show status -> What will change after commit
git status
 
# Add file to commit
git add ${specific file}
# Add specific code block to the commit -> Choose what block will be added
git add -p ${specific file}
 
# Git Commit -> Write the committing message clear and understandable
git commit
git status # Recheck the commit
```

```bash
# Branches basic flow
 
# Create
git branch ${branch name} # Or 
git branch ${branch name} ${commit code} # Create new branch on the specific revision
 
# Switching branches
git checkout ${other branch} # Or
git switch ${other branch}
git status # Check the switched
 
# Rename branch
git branch -m ${new name} # Change the name of the current using (HEAD) branch
git branch -m ${branch that you want to change name} ${new name} 
 
# Publishing branches
git push -u origin ${local branch}
 
# Tracking branches 
git branch --track ${local branch} origin/${remote branch} # Track branch from remote repo
git checkout --track ${remote branch} 
 
# Pulling + pushing branches
## If u setup the tracking correctly like above -> It just
git pull
git push
 
git branch -v # Show
```

```bash
# Some advance of branch
 
# Delete branch
git branch -f ${branch name} # local one
git push origin --delete ${branch name} # remote one
 
# Merging branches -> Integrating changes from another branch into ur current local HEAD branch
git checkout # Switch to the branch you want to receive the changes
git merge ${branch that u want to merge into}
 
# Rebase
git checkout ${branch name} # Switch to the branch you want to rebase
git rebase ${branch name} 
 
# Comparing branches
git log ${branch one}..${branch two}
 
# Undo the merge anh rebase
git merge --abort
git rebase --abort
```

```bash
# Some tips
 
# History
git log --oneline --decorate --all --graph --simplify-by-decoration
 
# Show last commit message
git show -s --format=%s
 
# Git add . + Git commit
git commit -am "${message}"
 
# Git custom command
git config --global alias.ac "commit -am"
-> git ac "${message}"
 
# Change the message of the lasted commit
git commit --amend -m "${message}"
git commit --amend # Open editor
# Undo a commit with a new commit
git revert "${message}"
 
# Save change in local
git stash
git stash pop # Or u can name it
git stash save ${name}
git stash list
git stash apply ${index of changes}
 
# Undo all Modified
git reset --hard
```

```bash
# Git stash
git stash save "{message}"
git stash list
git stash apply "{stash_id}"
git stash pop
git stash show
git stash branch <name>
git stash clear
git stash drop
```

```powershell
# Rebase master
git checkout master  # Checkout master to change current head to master
git pull --rebase    # Get all new change from remote origin/master
git checkout -       # Re-checkout previours branch (the branch you want to rebase)
git rebase master    # Rebase code
git push --force-with-lease   # Push code change
```

```bash
# Combind merge into 1 commit
git merge {{branch}} --squash 
```

```bash
# Reset local branch matching with remote
git fetch origin
git reset --hard origin/<<branch>>
## To clean other file that not match with remote
git clean -f # Remove ## Should check before remove
git clean -n -f # Check what file will be remove

# Ref link: https://stackoverflow.com/questions/1628088/reset-local-repository-branch-to-be-just-like-remote-repository-head
```

```bash

```

```bash
# Squash commit into one

git log --oneline
git rebase -i HEAD~6  # 6 is number of commit of the branch
# Change commit that you want to squash to s
# Save the change 
# Create new commit message 
# Push the change
git push --force-with-lease 
```

```bash
# Changing the message of the most recently pushed commit

# Changing message
git commit --amend
# Re-push to remote
git push --force-with-lease origin <<Branch>>
```

```markdown
# Git clone with depth 1 -> Only pull last cinnit info -> Avoid large repo pull
git clone --depth=1 git@bitbucket.org:metascan/fv-vcrom.git
```