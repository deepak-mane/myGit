# GitHub encountered Issues while working and there resoluitons

## 1. git error: failed to push some refs to

Problem: For some reason, I can't push now, whereas I could do it yesterday. Maybe I messed up with configs or something.
This is what happens:
When I use the git push origin master
```
$ git push origin master
To github.com:deepak-mane/my-ang-receipe-app.git
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'git@github.com:deepak-mane/my-ang-receipe-app.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

```
Solution

If the GitHub repo has seen new commits pushed to it, while you were working locally, I would advise using:
```
git pull --rebase
git push
```
The full syntax is:
```
git pull --rebase origin master
git push origin master
```
That way, you would replay (the --rebase part) your local commits on top of the newly updated origin/master (or origin/yourBranch: git pull origin yourBranch).

See a more complete example in the chapter 6 Pull with rebase of the Git Pocket Book.

I would recommend a:
```
git push -u origin master
```
That would establish a tracking relationship between your local master branch and its upstream branch.
After that, any future push for that branch can be done with a simple:

git push
See "Why do I need to explicitly push a new branch?".

Since the OP already reset and redone its commit on top of origin/master:
```
git reset --mixed origin/master
git add .
git commit -m "This is a new commit for what I originally planned to be amended"
git push origin master
There is no need to pull --rebase.
```
Note: git reset --mixed origin/master can also be written git reset origin/master, since the --mixed option is the default one when using git reset.



