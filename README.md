# myGit
Git Hub Usage,tricks Notes 

### Create a new branch with git and manage branches
---

In your github fork, you need to keep your master branch clean, by clean I mean without any changes, like that you can create at any time a branch from your master. Each time that you want to commit a bug or a feature, you need to create a branch for it, which will be a copy of your master branch.
When you do a pull request on a branch, you can continue to work on another branch and make another pull request on this other branch.
Before creating a new branch, pull the changes from upstream. Your master needs to be up to date.

Create the branch on your local machine and switch in this branch :
$ git checkout -b [name_of_your_new_branch]

Change working branch :
`$ git checkout [name_of_your_new_branch]`

Push the branch on github :
`$ git push origin [name_of_your_new_branch]`
When you want to commit something in your branch, be sure to be in your branch. Add -u parameter to set upstream.

You can see all branches created by using :
`$ git branch`
Which will show :
`* approval_messages
  master
  master_clean`

Add a new remote for your branch :
`$ git remote add [name_of_your_remote] `

Push changes from your commit into your branch :
`$ git push [name_of_your_new_remote] [name_of_your_branch]`

Update your branch when the original branch from official repository has been updated :
`$ git fetch [name_of_your_remote]`

Then you need to apply to merge changes, if your branch is derivated from develop you need to do :
`$ git merge [name_of_your_remote]/develop`

Delete a branch on your local filesystem :
`$ git branch -d [name_of_your_new_branch]`

To force the deletion of local branch on your filesystem :
`$ git branch -D [name_of_your_new_branch]`

Delete the branch on github :
`$ git push origin :[name_of_your_new_branch]`

The only difference is the : to say delete, you can do it too by using github interface to remove branch : https://help.github.com/articles/deleting-unused-branches.
If you want to change default branch, it's so easy with github, in your fork go into Admin and in the drop-down list default branch choose what you want.

# tmux cheatsheet

As configured in [my dotfiles](https://github.com/henrik/dotfiles/blob/master/tmux.conf).

start new:

    tmux

start new with session name:

    tmux new -s myname

attach:

    tmux a  #  (or at, or attach)

attach to named:

    tmux a -t myname

list sessions:

    tmux ls

kill session:

    tmux kill-session -t myname

In tmux, hit the prefix `ctrl+b` and then:

## Sessions

    :new<CR>  new session
    s  list sessions
    $  name session

## Windows (tabs)

    c           new window
    ,           name window
    w           list windows
    f           find window
    &           kill window
    .           move window - prompted for a new number
    :movew<CR>  move window to the next unused number

## Panes (splits)

    %  horizontal split
    "  vertical split
    
    o  swap panes
    q  show pane numbers
    x  kill pane
    ⍽  space - toggle between layouts

## Window/pane surgery

    :joinp -s :2<CR>  move window 2 into a new pane in the current window
    :joinp -t :1<CR>  move the current pane into a new pane in window 1

* [Move window to pane](http://unix.stackexchange.com/questions/14300/tmux-move-window-to-pane)
* [How to reorder windows](http://superuser.com/questions/343572/tmux-how-do-i-reorder-my-windows)

## Misc

    d  detach
    t  big clock
    ?  list shortcuts
    :  prompt

Resources:

* [cheat sheet](http://cheat.errtheblog.com/s/tmux/)
