---
date: 2021-07-30T07:05:25+01:00
title: "How to remove a file from Git history"
share: false
tags: ["til", "git", "tools"]
---
Today I learned how to remove a file from a git repository while also cleaning
it from the history. When you delete it with `git rm` or `git rm --cached`,
tracks remain in the commit history (the reflog). That might not be a big deal,
but if the file has sensitive contents that you want to disappear from version
control entirely, then you also want it cleaned from the reflog. That's when
[`git filter-branch`][1] comes to the rescue.

To be on the safe side, I first cloned the repository to a test directory:

    $ git clone <REPOSITORY> test
    $ cd test

Once into the test directory, this is the command that saved the day:

    # make sure you insert the whole file path, relative to the repository root
    $ git filter-branch --force --index-filter \
      "git rm --cached --ignore-unmatch PATH-TO-THE-FILE" \
      --prune-empty --tag-name-filter cat -- --all

The command above will go through the history, find all commits where the file
is involved, and alter them to eliminate the file. Yes, history changes,
so a force-push will be required at the end.

To test that the file has indeed been removed, I used `git blame`:

    $ git blame PATH-TO-THE-FILE
    fatal: no such path 'PATH-TO-THE-FILE' in HEAD

If the file needs to stay in the local directory, you can add it to
`.gitignore`:

    $ echo "PATH-TO-THE-FILE" >> .gitignore
    $ git add .gitignore
    $ git commit -m "add FILE to .gitignore"

Once everything was ready, I went back to the original clone directory,
replayed all the above, then force-pushed back to the remote:

    $ git push origin --force --all

If you have remote tags, those need to be force-pushed as well:

    $ git push origin --force --tags

In my case, the repository is private with no forks, so the changing
history was not a big deal for the few colleagues with access to it. Of
course, any other existing clone will need to be updated[^2].

In so many years with git, this is the very first time I had to do something
similar. Typically, you don't commit sensitive data to version control, but we
all make mistakes every once in a while, don't we?

*Subscribe to the [newsletter][nl], the [RSS feed][rss], or follow @[nicolaiarocci][tw] on Twitter*

 [1]: https://git-scm.com/docs/git-filter-branch
 [^2]: Keep in mind, eventual stashed changes will be lost after `git filter-branch`. Make sure you unstash before issuing the command.
 [rss]: https://nicolaiarocci.com/index.xml
 [tw]: http://twitter.com/nicolaiarocci
 [nl]: https://buttondown.email/nicolaiarocci
