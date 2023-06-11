Title: Publishing this blog
Date: 2023-06-11
Tags: blog, quickblog, github-pages

In my previous post, I got quickblog working! Woo! But I still need somewhere
to publish it... so you wonderful people can read it!

I’ve chosen to use [github pages](https://pages.github.com/).

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
Browse... [https://tim-brown.github.io](https://tim-brown.github.io)

Woo hoo! It’s alive!

## And finally a bit of tidyup...

```bash
cd …/my-blog
git add .gitignore bb.edn posts/2023-06-11-publishing.md
```

# TODOs
- backlink to previous article (and figure out how to make that work both
  locally and on production site)

# Call to Action
