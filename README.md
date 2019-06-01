# myGit
Git Hub Usage,tricks Notes 


## Bitbucket & Git
                                                          
### set up local repo                                                 
```
git clone https: <remote repo>
git checkout -b <new_branch_name>       # create and push a branch
```                                                   
### typical change & check-in
```
git checkout <branch>
git add <files>
git commit -m 'commit message'
git push origin <branch> - changes show up on remote
                             

git branch -a            # show all local and remote branches
git branch <branch name> # switch to this branch

git status
git status -sb

git remote -v            # show remote origin info
```
### reset what the origin is
```
git remote remove origin
git remote add origin ssh://git@xwtcvpgit:7999/pup/puppet-appdynamics.git

git push -u origin <new_branch_name>    # -u does a --set-upstream

git fetch --                 # get rid of all local branches that aren't remote:
git remote prune origin      # get rid of local branches that are stale

git reset <file>             # undo an add
```
### squashing commits on a branch
```git rebase -i HEAD~5                   # number is number of commits to squash```
### interactive vi sessions to do 'reword' and 'fixup' or 'squashes'
```git push origin <branch-name> --force```

### rebasing with master to get latest changes
```
git fetch
git rebase origin/production
git push origin <branch-name> --force
```


###  to revert current local area to the latest on remote...
```
git fetch origin
git reset --hard origin/master
```
### delete a remote branch and then delete local copy...
```
git push origin --delete <branch name>
git branch -D <branch name>
```
### tag a repo
```
git checkout master
git pull
git tag # lists all tags
git tag -a -m "Some message" 0.0.0 # this is the new version number
git push --tags
```
### move a tag
```
git tag --force v1.0 <ID-of-commit-127>
git push --force --tags
```
### pretty print log information
```
git log --pretty=oneline --abbrev-commit
git log --oneline
```


### Create a new branch with git and manage branches
---

In your github fork, you need to keep your master branch clean, by clean I mean without any changes, like that you can create at any time a branch from your master. Each time that you want to commit a bug or a feature, you need to create a branch for it, which will be a copy of your master branch.
When you do a pull request on a branch, you can continue to work on another branch and make another pull request on this other branch.
Before creating a new branch, pull the changes from upstream. Your master needs to be up to date.

- Create the branch on your local machine and switch in this branch :

```$ git checkout -b [name_of_your_new_branch]```

- Change working branch :
```$ git checkout [name_of_your_new_branch]```

- Push the branch on github :
```$ git push origin [name_of_your_new_branch]```
When you want to commit something in your branch, be sure to be in your branch. Add -u parameter to set upstream.

- Create a new branch:
```git checkout -b feature_branch_name```

- Edit, add and commit your files.Push your branch to the remote repository:
```git push -u origin feature_branch_name```

- You can see all branches created by using :
```$ git branch```
- Which will show :
* approval_messages
  master
  master_clean

- Add a new remote for your branch :
```$ git remote add [name_of_your_remote] ```

- Push changes from your commit into your branch :
```$ git push [name_of_your_new_remote] [name_of_your_branch]```

- Update your branch when the original branch from official repository has been updated :
```$ git fetch [name_of_your_remote]```

- Then you need to apply to merge changes, if your branch is derivated from develop you need to do :
```$ git merge [name_of_your_remote]/develop```

- Delete a branch on your local filesystem :
```$ git branch -d [name_of_your_new_branch]```

- To force the deletion of local branch on your filesystem :
```$ git branch -D [name_of_your_new_branch]```

- Delete the branch on github :
```$ git push origin :[name_of_your_new_branch]```

The only difference is the : to say delete, you can do it too by using github interface to remove branch : [deleting-unused-branches](https://help.github.com/articles/deleting-unused-branches.)
If you want to change default branch, it's so easy with github, in your fork go into Admin and in the drop-down list default branch choose what you want.

### Delete branch with git and manage branches
---
How do I delete a Git branch both locally and remotely?

```
$ git push --delete <remote_name> <branch_name>
$ git branch -d <branch_name>
```
Note that in most cases the remote name is origin.

 - Delete Local Branch
To delete the local branch use one of the following:

```
$ git branch -d branch_name
$ git branch -D branch_name
```
Note: The -d option is an alias for --delete, which only deletes the branch if it has already been fully merged in its upstream branch. You could also use -D, which is an alias for --delete --force, which deletes the branch "irrespective of its merged status." [Source: man git-branch]

 - Delete Remote Branch 
As of Git v1.7.0, you can delete a remote branch using

```
$ git push <remote_name> --delete <branch_name>
```
which might be easier to remember than

```
$ git push <remote_name> :<branch_name>
```
which was added in Git v1.5.0 "to delete a remote branch or a tag."

Starting on Git v2.8.0 you can also use git push with the -d option as an alias for --delete.

Therefore, the version of Git you have installed will dictate whether you need to use the easier or harder syntax.

 - Delete Remote Branch
    - Deleting Remote Branches
            Suppose you’re done with a remote branch — say, you and your collaborators are finished with a feature and have merged it into your remote’s master branch (or whatever branch your stable code-line is in). You can delete a remote branch using the rather obtuse syntax git push [remotename] :[branch]. If you want to delete your server-fix branch from the server, you run the following:

```$ git push origin :serverfix```
To git@github.com:schacon/simplegit.git
 - [deleted]         serverfix
Boom. No more branch on your server. You may want to dog-ear this page, because you’ll need that command, and you’ll likely forget the syntax. A way to remember this command is by recalling the git push [remotename] [localbranch]:[remotebranch] syntax that we went over a bit earlier. If you leave off the [localbranch] portion, then you’re basically saying, “Take nothing on my side and make it be [remotebranch].”

I issued git push origin :bugfix and it worked beautifully. Scott Chacon was right—I will want to dog ear that page (or virtually dog ear by answering this on Stack Overflow).

Then you should execute this on other machines

```git fetch --all --prune```
to propagate changes.
