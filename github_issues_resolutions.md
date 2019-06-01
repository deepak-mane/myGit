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


## 2. error: Pulling is not possible because you have unmerged files

What is currently happening is, that you have a certain set of files, which you have tried merging earlier, but they threw up merge conflicts. Ideally, if one gets a merge conflict, he should resolve them manually, and commit the changes using git add file.name && git commit -m "removed merge conflicts". Now, another user has updated the files in question on his repository, and has pushed his changes to the common upstream repo.

It so happens, that your merge conflicts from (probably) the last commit were not not resolved, so your files are not merged all right, and hence the U(unmerged) flag for the files. So now, when you do a git pull, git is throwing up the error, because you have some version of the file, which is not correctly resolved.

To resolve this, you will have to resolve the merge conflicts in question, and add and commit the changes, before you can do a git pull.

Sample reproduction and resolution of the issue:
# Note: commands below in format `CUURENT_WORKING_DIRECTORY $ command params`
Desktop $ cd test
First, let us create the repository structure
```
test $ mkdir repo && cd repo && git init && touch file && git add file && git commit -m "msg"
repo $ cd .. && git clone repo repo_clone && cd repo_clone
repo_clone $ echo "text2" >> file && git add file && git commit -m "msg" && cd ../repo
repo $ echo "text1" >> file && git add file && git commit -m "msg" && cd ../repo_clone
Now we are in repo_clone, and if you do a git pull, it will throw up conflicts

repo_clone $ git pull origin master
remote: Counting objects: 5, done.
remote: Total 3 (delta 0), reused 0 (delta 0)
Unpacking objects: 100% (3/3), done.
From /home/anshulgoyal/Desktop/test/test/repo
 * branch            master     -> FETCH_HEAD
   24d5b2e..1a1aa70  master     -> origin/master
Auto-merging file
CONFLICT (content): Merge conflict in file
Automatic merge failed; fix conflicts and then commit the result.
If we ignore the conflicts in the clone, and make more commits in the original repo now,

repo_clone $ cd ../repo
repo $ echo "text1" >> file && git add file && git commit -m "msg" && cd ../repo_clone
And then we do a git pull, we get

repo_clone $ git pull
U   file
Pull is not possible because you have unmerged files.
Please, fix them up in the work tree, and then use 'git add/rm <file>'
as appropriate to mark resolution, or use 'git commit -a'.
Note that the file now is in an unmerged state and if we do a git status, we can clearly see the same:

repo_clone $ git status
On branch master
Your branch and 'origin/master' have diverged,
and have 1 and 1 different commit each, respectively.
  (use "git pull" to merge the remote branch into yours)

You have unmerged paths.
  (fix conflicts and run "git commit")

Unmerged paths:
  (use "git add <file>..." to mark resolution)

        both modified:      file
So, to resolve this, we first need to resolve the merge conflict we ignored earlier

repo_clone $ vi file
and set its contents to

text2
text1
text1
and then add it and commit the changes

repo_clone $ git add file && git commit -m "resolved merge conflicts"
[master 39c3ba1] resolved merge conflicts
```
