Title: My first blog entry for a while
Date: 2023-06-06
Tags: clojure, blogging

So... I’ve decided to get back on the blogging horse, but I’ve been dragging my feet a bit figuring out what blogging platform to use.

I’ve had previous experience with gitlab pages... and a long time ago [racket frog](https://docs.racket-lang.org/frog/index.html). Which is awesome, but as far as I can tell, no longer supported by the author. And my general trajectory is Clojure-wards.

I need a blogging tool, implemented in Clojure, that will work with gitlab pages.  
A quick google search of “babashka blog framework” threw up [quickblog](https://github.com/borkdude/quickblog). Deep breath, what’s that going to look like?

The readme looks really simple (disclosure, I already have babashka and Clojure installed on my local machine, and I’m pretty happy with the idea of configuring my environment with a `bb.edn` (or `deps.clj`)). So:

* Created an empty github repo to hold the blog
* I basically copied the `bb.edn`
* Customised it with an updated github sha (`792f952be8fe0f3326b293dde3251f6a09deaf0c` today, who knows what it will be for you)
* And pretty well, this thing works out of the box!

Further customisation of `bb.edn` was to “personalise” the blog:
* Updated the `:blog-title` and `:blog-description` keys

And after that:
```bash
bb quickblog new --file "2023-06-06-test.md" --title "My first blog entry for a while"
```
created a new file in (an automatically created) `posts/`.

I edit the new file in one terminal; and in another I run:
```bash
bb quickblog watch
```

And now I have the blog post... with live updates; and a few todos:

* Write the content!
* Discuss (I need to set up Disqus)
* Publishing to pages
* PR to allow `:footnote?` to be passed to `md/md-to-html-string`: I tried to use a footnote, but instead it gave me superscript. That’s a choice that should be given to the author of the document.
* Styles and favicons

## Write the content

On it --- that’s what this post is!

## Setting up Disqus

* set up (or revive) the Disqus account
* set up a “site”
* follow the install instructions for “Universal Code” for the site
* add the code Disqus provides to `templates/post.html` (wherever you think you need it)
* I had to change the code to set the `this.page.url` and `this.page.identifier`. To do this, you need to activate the `disqus_config` section of the universal code and replace it with:
   ```javascript
   var disqus_config = function () {
     this.page.url = sharingUrl; 
     this.page.identifier = "{{file}}";
   };
   ```
  this only goes so far, though because I couldn’t find a way to get the page’s URL into the page template using the _Selmer_ templating (worth further investigation). I could get it in `templates/base.html`; so around line 29 there...
  ```html
   {% if sharing.url %}
       <meta name="twitter:url" content="{{sharing.url}}">
       <meta property="og:url" content="{{sharing.url}}">
       <script>const sharingUrl = "{{sharing.url}}"</script>
   {% endif %}
  ```

I have to figure out what the “Discus this post” link is.

## Publishing on pages

I am now at: `Tue  6 Jun 20:14:23 BST 2023` --- 2 hours in (and that includes blogging!)

I don’t have this pushed up to github pages yet... that’s one for tomorrow. But, wow... so far this has been properly smooth!
I’m impressed.

## First... check it in!

So far, I’ve generated the following files:
```
.
./posts
./posts/2023-06-06-test.md
./templates
./templates/post.html
./templates/post-links.html
./templates/tags.html
./templates/index.html
./templates/style.css
./templates/base.html
./.work
./.work/2023-06-06-test.md.pre-template.html
./.work/cache.edn
./.gitignore
./LICENSE
./README.md
./public
./public/planetclojure.xml
./public/atom.xml
./public/tags
./public/tags/clojure.html
./public/tags/clojure-blogging.html
./public/tags/blogging.html
./public/tags/index.html
./public/archive.html
./public/2023-06-06-test.html
./public/index.html
./public/style.css
./bb.edn
```

I need to `.gitignore`:
* `.work`
* `public` (dunno if I have to un-gitignore this later... we’ll see)

The rest needs to be source controlled.

Great... committing my blog for the evening!
```bash
git add .gitignore README.md bb.edn posts/ templates
```
