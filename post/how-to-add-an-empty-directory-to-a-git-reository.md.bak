---
date: 2021-03-22T07:05:25+01:00
title: "How to add an empty directory to a Git repository"
share: false
tags: ["til", "git"]
---
How do you add an empty directory to a Git repository? It's a classic, and yet,
I have to look it up every single time. Git does not support this out of the
box:

> Currently the design of the Git index (staging area) only permits files to be
> listed, and nobody competent enough to make the change to allow empty
> directories has cared enough about this situation to remedy it. Directories
> are added automatically when adding files inside them. That is, directories
> never have to be added to the repository, and are not tracked on their own.
> You can say `git add <dir>` and it will add the files in there. **If you really
> need a directory to exist in checkouts you should create a file in it**.
> .gitignore works well for this purpose; you can leave it empty or fill in
> the names of files you do not expect to show up in the directory.
> ([source][1])

The same answer offers a workaround: just save an empty .gitignore file into
the directory. At that point, `git status` shows the file as untracked. We can
add it to the repository, and *presto*, our folder ends up captured in version
control. 

I don't like using .gitignore for this. That file serves a different,
unrelated goal. Finding it in an otherwise empty directory would cause
puzzlement to my colleagues and my future self in six months. For better
semantic and clarity, what I do is add a `.keep` file instead:

    $ touch mydir/.keep

Same trick. Better semantics. When I pull this repository in six months, I will
immediately grasp what's going on (an alternative would be a README.md file
with an explanation.)

Of course, if the dir is meant to fill-up over time, but we still want to
ignore its future contents in version control, then .gitignore is the right
tool for the job. Something like this would work (I [dug it up][2] on Stack
Overflow, where else):

    # Ignore everything in this directory
    *
    # Except this file
    !.gitignore

I should probably adopt the #tirl tag, as in "Today I Re-Learned."


*Subscribe to the [newsletter][nl], the [RSS feed][rss], or follow @[nicolaiarocci][tw] on Twitter*

 [1]: https://git.wiki.kernel.org/index.php/GitFaq#Can_I_add_empty_directories.3F
 [2]: https://stackoverflow.com/questions/115983/how-can-i-add-an-empty-directory-to-a-git-repository
 [rss]: https://nicolaiarocci.com/index.xml
 [tw]: http://twitter.com/nicolaiarocci
 [nl]: https://buttondown.email/nicolaiarocci
