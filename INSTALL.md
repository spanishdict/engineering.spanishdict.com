Installation
============

This site uses [Jekyll][jekyll] with some extra tweaks, which means a
multi-language environment as follows:

* [RVM][rvm]: A Ruby virtual environment for Rake and the core Jekyll stuff.
* [VirtualEnv][ve]: A Python virtual environment for Pygments.

[jekyll]: https://github.com/mojombo/jekyll
[rvm]: http://beginrescueend.com/
[ve]: http://pypi.python.org/pypi/virtualenv

Ruby Gemset
===========
After you have an appropriate `rvm` environment, activate the environment,
and import our gemset:

    $ rvm gemset import default.gems

Python Requirements
===================
After you have an appropriate `virtualenv` environment, activate the
environment, and install all the requirements:

    $ pip install -r requirements.txt

Node.js Packages
================
Our CSS is statically built using [Stylus][stylus] (*note*: not as a Jekyll
plugin because we want to be able to have GitHub auto-build the site). The
stylus dependencies can be installed to the local repo directory with:

    $ npm install

[stylus]: http://learnboost.github.com/stylus/
