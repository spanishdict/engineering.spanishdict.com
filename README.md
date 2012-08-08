SpanishDict Engineering Blog
============================

Jekyll repository for [engineering.spanishdict.com][eng_blog].

[eng_blog]: http://engineering.spanishdict.com

Development
===========
This site uses [Jekyll][jekyll] to create all the static HTML content.
To hack on the site, please see the available `rake` tasks with:

    $ rake -T

[jekyll]: https://github.com/mojombo/jekyll

Dev. Server
-----------
To run the local development server (useful for live previewing):

    $ rake dev:server

CSS Changes
-----------
We use [Stylus][stylus] for CSS content, but we generate static CSS that is
then saved in source control before pushing up the final site. (This is because
GitHub won't build the CSS dynamically via a plugin). So, if you change any
CSS, make sure to run:

    $ rake gen:css

and commit any changes to `git`.  Also note that if you change the underlying
syntax highlighting CSS, you have to run a separate generate task:

    $ rake gen:css_syntax

and similarly commit any changes.

[stylus]: http://learnboost.github.com/stylus/

404 Page Changes
----------------
GitHub Pages supports 404 pages, but they must be static pages, and not part
of normal site Markdown. Accordingly, we have to also generate these pages.
If you change the default layout or anything in "404.md", run:

    $ rake gen:not_found

and commit any changes.


Working on Changes
==================
You should work in the "`master`" branch for all of your changes. You can
view the live rendered pages in dev. at: http://127.0.0.1:4000 .  When you
are finished, then you can push to the pages branch (next section).

**Note**: Your changes should *first* go in **master**, not **gh-pages**.

Pushing to Live Site
====================
Pushing to the live site is easy, using GitHub [Pages][gh_pages]' magic
"`gh-pages`" branch:

    # Make sure everything is fully committed and pushed in "master" branch.
    $ git status

    # Then switch to gh-pages branch.
    $ git checkout gh-pages

    # Merge changes from master branch
    $ git merge master

    # Push gh-pages branch to create new live site.
    $ git push origin gh-pages

    # Switch back to normal (master) branch
    $ git checkout master

[gh_pages]: http://pages.github.com/
