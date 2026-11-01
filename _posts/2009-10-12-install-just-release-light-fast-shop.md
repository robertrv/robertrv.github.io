---
title: "Install just release Light Fast Shop"
date: 2009-10-12
categories: 
  - "django"
  - "software-development"
tags: 
  - "django"
  - "ecommerce"
  - "hg"
  - "lsf"
  - "mercurial"
  - "shop"
  - "virtualenv"

---

Recently I've seen the django-lfs \[1\] (Light Fast Shop\[2\]) just released to the public today \[3\]

In order to get your code working you have to follow instalation instructions, but you will probably need something else. I had some problems with missing dependencies (mainly .h, because by default I'm using virtualenv with python2.6, and on my ubuntu everything is ready for python2.5 ... versions can be a nightmare !). So what I did before I got lfs working was:

- sudo apt-get install python2.6-dev    (should be changed in case to 2.5 in case your installation uses 2.5 ... type 'python --version' to know the exact version)
- sudo apt-get install sqlite3 libsqlite3-dev
- sudo apt-get install python-profiler
- apt\-get install mercurial

Finally you can follow the instructions to install lfs using the quickstart \[4\]

And if you want to have some data on this:

./lfs-buildout-quickstart/bin/django loaddata eggs/django\_lfs-0.1.3-py2.6.egg/lfs/core/fixtures/lfs\_initial.xml

The reason why I post this info is because I like the way this is distributed, the infrastructure and some features (as well is much easier to install than satchmo\[5\], sorry :S, which can be a problem in a hosting, specially if is shared):

- jgrowl: Nice jQuery Notification system, who knows me know that I like this useless things !
- All the admin interface tunned with jQuery \[7\]
- the use of portlets
- Completely separate themes \[8\], which can become a possible monetization in the future to work with customization as well at this point
- ....

Things I don't like and probably will be fixed in a future:

- Lack of documentation in the terms of description of the main entities.
- Lack of translation to other language.

[\[1\]](http://bitbucket.org/diefenbach/django-lfs/wiki/Home) project home on bitbucket which has moved from the old [django-lfs](http://code.google.com/p/django-lfs/) google code

[\[2\]](http://www.getlfs.com/) The "commercial" web site to explain and get relevance about the project, nice !

[\[3\]](http://twitter.com/lfsproject/status/4808354159) Twitter post on the project

[\[4\]](http://bitbucket.org/diefenbach/django-lfs/wiki/Quickstart) Install instructions for lfs

[\[5\]](http://www.satchmoproject.com/docs/svn/new_installation.html) Satchmo installation process

[\[6\]](http://stanlemon.net/projects/jgrowl.html) Notification system

[\[7\]](http://demo.getlfs.com/manage/) Admin interface for django-lfs

[\[8\]](http://pypi.python.org/pypi/django-lfstheme/0.1.1) Current django theme
