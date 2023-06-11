Title: Publishing this blog
Date: 2023-06-11
Tags: blog, github-pages, quickblog

In my previous post, I got quickblog working! Woo! But I still need somewhere
to publish it… so you wonderful people can read it!

I’ve chosen to use [github pages](https://pages.github.com/).

<!-- end-of-preview --> 

I’ve been giving some thought to how to structure my code; and I have decided
to try:
* this repo [tim-brown/my-blog](https://github.com/tim-brown/my-blog)
  where I can manage the blog’s source etc.
* my personal pages repo
  [tim-brown/tim-brown.github.io](https://github.com/tim-brown/tim-brown.github.io),
  as a submodule of **my-blog**

I think that &mdash; in the spirit of simplicity &mdash; having the pages repo
composed with the blogging repo in this way is explicit, and (once I’ve got my
head around [git submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules)).

It also has the advantage that, should I ever want to make **my-blog** private, I can.

# So what have I done?

## Set up my-blog repo with my quickblog blog

&#x2611; Did that in the last post.

## Create an empty repo for pages
As per the instructions on github, I have created an empty repo: 
[tim-brown/tim-brown.github.io](https://github.com/tim-brown/tim-brown.github.io).

## Make it a submodule of my-blog

```bash
cd my-blog
git submodule add git@github.com:tim-brown/tim-brown.github.io.git 
git commit -m 'publish: add personal pages submodule'
git push
```

## Change the publshing target for quickblog

I now want to publish to the `tim-brown.github.io` submodule, rather than
`public`, which is what quickblog does by default.

Change to `bb.edn`:

```clojure
  :init (def opts {:blog-title …
                   :blog-description …
                   :blog-root …
                   :out-dir "tim-brown.github.io"})
```

I also need to tidy up the old `public` directory. We put it into `.gitignore`
last time; so this is just cleanup:
```bash
rm -rf public
```

## And publish?!

I think all I now need to do is commit and push the changes in `tim-brown.github.io`.

Fingers crossed:
```bash
git add .
git commit -am 'initial blog commit'
git push
```
Browse… [https://tim-brown.github.io](https://tim-brown.github.io)

Woo hoo! It’s alive!

## And finally a bit of tidyup…

```bash
cd …/my-blog
# changes we made to :out-dir
git add bb.edn
# the new post
git add posts/2023-06-11-publishing.md
# the new submodule commit
git add tim-brown.github.io
```

(This is a bit misleading, because as I continue to write this entry &mdash; after publication, I continue to get):
```bash
git status

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
  (commit or discard the untracked or modified content in submodules)
	modified:   tim-brown.github.io (modified content)
```

`(modified content)` is because I have a `bb quicklog watch` tracking changes in my post,
and building the site into the submodule. This is great… it means I have to continue to
commit and push the submodule until the published site matches the source.

So I won’t bore you with “going through the cycle until it’s all settled”.

# Call to Action

I’m going to put an explicit CTA at the end of each of my blog posts.
Not so you buy something (not that I have anything to sell &mdash; yet),
but because there is no point me writing here if you don’t take anything
from it.

So today… I’m asking you to feed back any bugs you find on this site.
Let me know on the Disqus below (and prove it works).

# For the future (and to-do list)
- backlink to previous article (and figure out how to make that work both
  locally and on production site)
- this looks eminently scriptable; for now I’ll probably bump along manually
  building the site (the publish workflow is, after all, an “end of day” activity)…
  I want to get on with some proper content!
