---
date: 2021-04-29T07:05:25+01:00
title: "Git Worktree vs Git Savepoints"
share: false
tags: ["git", "tools"]
---
The official Git documentation presents the following example as a valid
use-case for the `worktree` command:

> You are in the middle of a refactoring session and your boss comes in and
> demands that you fix something immediately. You might typically use
> git-stash[1] to store your changes away temporarily. However, your working
> tree is in such a state of disarray (with new, moved, and removed files and
> other bits and pieces strewn around) that you don't want to risk disturbing
> any of it. ([source][1])

If you don't know about `worktree`, you should check it out. It is a handy,
powerful yet little known command. I don't use it, however. It will check out
a new branch to a new directory, and I don't like that. I prefer to keep the
simple, default 1:1 relationship between the repository and the file system.
Managing multiple working trees seems like an unnecessary complication when
similar results can be achieved with a few aliases. 

Indeed, for the use-case above, my workflow revolves around three git-aliases.
Over the years, I collected many. Most of them (like the ones mentioned here)
are not my doing. I stumbled upon them somewhere, tinkered as needed, and then
incorporated them into my daily workflow.

## `git save`

This adds all changes, including untracked files, to the staging area and then
commits with a `SAVEPOINT` message. When an emergency hits and I need to
quickly switch context, I'll just `git save` and check out to a new branch to
do whatever I am tasked to do. When I'm done, I'll switch back to my original
branch, `git undo`(see below), and resume work. It's easily configured with:

    $ git config --global alias.save '!git add -A && git commit -m "SAVEPOINT"'

## `git wip` 

`wip` is similar to `save`. It stages all tracked changes and then commits with
a `WIP` message. So yes, it offers the same features as above but leaves
untracked files unstaged, a significant difference. Like above, when done with
the extra work, I'll switch back, `git undo`, and resume. Set it up with:

    $ git config --global alias.wip '!git add -u && git commit -m "WIP"'


## `git undo` 
This alias allows me to quickly resume work after a `save` or `wip`. It undoes
the last commit but keeps its changes, with files unstaged. It can also be used
in other circumstances (for those, however, I have a functionally identical
`r1` alias at hand). Configure with:

    $ git config —-global alias.undo 'reset HEAD^ —-mixed'

## `git wipe` 
This is a special, use-with-caution one. It adds changes in the working tree to
a `WIPE SAVEPOINT` commit, then it wipes the commit. At that point, the working
tree is clean, but I can still go back to that work if the need arises (via
reflog). Seldom used, this `wipe` comes in handy when I have some experimental
code that is not going into production and yet, I want to keep it around. Set
it up with:

    $ git config --global alias.wipe \
        '!git add -A && git commit -qm "WIPE SAVEPOINT" && git reset HEAD~1 --hard'

If you are not familiar with the git reflog, you might want to stay clear from
`wipe`, though. 

One advantage of this workflow is that saved changes will stay with their
relevant branch. When you get back to it, `git log` will hint at what happened
when you left. Assuming it is a private branch, you might even decide to push
it for backup before starting the hotfix work.

*Subscribe to the [newsletter][nl], the [RSS feed][rss], or follow @[nicolaiarocci][tw] on Twitter*

 [1]: https://git-scm.com/docs/git-worktree
 [2]: https://github.com/nicolaiarocci/dotfiles/blob/master/git/gitconfig
 [rss]: https://nicolaiarocci.com/index.xml
 [tw]: http://twitter.com/nicolaiarocci
 [nl]: https://buttondown.email/nicolaiarocci
