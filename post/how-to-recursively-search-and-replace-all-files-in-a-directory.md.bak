---
date: 2024-01-06T09:34:16+01:00
title: How to use bash to recursively search and replace a string in all directory files
tags: ["til", "bash"]
---
Another achievement I unlocked with the [recent website
update](/new-website-finally-with-no-analytics/) is the newsletter switch from Substack to
a fantastic and independent provider,
[Buttondown](https://buttondown.email/refer/nicolaiarocci). That required
updating all the "subscribe to my newsletter" links. We're talking 5K posts, all
saved as individual files in the same directory. The bash command that did that
for me is:

```bash
find content/post/*.md -type f -exec \
    sed -i .bak 's|https://nicolaiarocci.substack.com|https://buttondown.email/nicolaiarocci|g' {} +
```

It is pretty straightforward. `find` looks for all markdown files in the
`content/post/` directory. On each file, `sed` performs a search-and-replace
action. Notice that I use `|` instead of the standard `/` as a separator for the
search-and-replace pattern , and that's because the pattern itself has `/`s in
the URLs so I need to differentiate. Also, on macOS, the `-i` parameter requires
a backup file argument ("*.bak") to make a backup copy before the update. This
argument is unnecessary in newer sed versions and will perform an in-place
update if not provided.

Later, I realized I would be better off if I removed the call to action from my
posts and added it to the footer template instead. That way, I'd only have one
place to edit or update it in the future, and my RSS feed (and newsletter
updates,  as they draw from the RSS feed) would be clean of unnecessary spam. In
hindsight, this a move I could've made many years ago (2010?) when I installed
Hugo for the first time, but hey, better late than never. But how could I delete
calls to action from all my 5K posts? With a variation of the above command, of
course:

```bash
find content/post/*.md -type f -exec sed -i .bak '/*Subscribe to.*$/,$d' {} +
```

It is the same logic as above, but we're replacing the matched string with a
"delete all lines till the end of the file" pattern this time. I must admit that
this one was trickier to pull off and required a discrete amount of trial and
error.