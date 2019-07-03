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

## 2. error: LF will be replaced by CRLF in git - What is that and is it important?

In Unix systems the end of a line is represented with a line feed (LF). In windows a line is represented with a carriage return (CR) and a line feed (LF) thus (CRLF). when you get code from git that was uploaded from a unix system they will only have an LF.

If you want to turn this warning off, type this in the git command line
```
git config core.autocrlf true
```
If you want to make an intelligent decision how git should handle this, read the documentation

Here is a snippet

- Formatting and Whitespace

Formatting and whitespace issues are some of the more frustrating and subtle problems that many developers encounter when collaborating, especially cross-platform. It’s very easy for patches or other collaborated work to introduce subtle whitespace changes because editors silently introduce them, and if your files ever touch a Windows system, their line endings might be replaced. Git has a few configuration options to help with these issues.
```
core.autocrlf
```
If you’re programming on Windows and working with people who are not (or vice-versa), you’ll probably run into line-ending issues at some point. This is because Windows uses both a carriage-return character and a linefeed character for newlines in its files, whereas Mac and Linux systems use only the linefeed character. This is a subtle but incredibly annoying fact of cross-platform work; many editors on Windows silently replace existing LF-style line endings with CRLF, or insert both line-ending characters when the user hits the enter key.

Git can handle this by auto-converting CRLF line endings into LF when you add a file to the index, and vice versa when it checks out code onto your filesystem. You can turn on this functionality with the core.autocrlf setting. If you’re on a Windows machine, set it to true – this converts LF endings into CRLF when you check out code:
```
$ git config --global core.autocrlf true
```
If you’re on a Linux or Mac system that uses LF line endings, then you don’t want Git to automatically convert them when you check out files; however, if a file with CRLF endings accidentally gets introduced, then you may want Git to fix it. You can tell Git to convert CRLF to LF on commit but not the other way around by setting core.autocrlf to input:
```
$ git config --global core.autocrlf input
```
This setup should leave you with CRLF endings in Windows checkouts, but LF endings on Mac and Linux systems and in the repository.

If you’re a Windows programmer doing a Windows-only project, then you can turn off this functionality, recording the carriage returns in the repository by setting the config value to false:
```
$ git config --global core.autocrlf false
```

## 3. error: Your local changes to the following files would be overwritten by merge:Please commit your changes or stash them before you merge.Aborting

You can't merge with local modifications. Git protects you from losing potentially important changes.

You have three options:

1. Commit the change using
```
git commit -m "My message"
```
2. Stash it.
Stashing acts as a stack, where you can push changes, and you pop them in reverse order.

To stash, type
```
git stash
```
Do the merge, and then pull the stash:
```
git stash pop
```
3. Discard the local changes
```
using git reset --hard
or git checkout -t -f remote/branch
```
Or: Discard local changes for a specific file
```
using git checkout filename

```
