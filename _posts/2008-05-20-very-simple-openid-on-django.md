---
title: "very simple openid on django"
date: 2008-05-20
categories: 
  - "software-development"
tags: 
  - "django"
  - "openid"

---

As most of you know, I am learning a some bits of django, and some other things.

I am just wanted to share how incredibly easy is to use [openid](http://en.wikipedia.org/wiki/OpenID) inside a [django](http://www.djangoproject.com/) application. It's really nice to have login users without the need to ask them username/password. This is the way openid works, you just have to login on any openid server, and when you use this openid authorization authentication to login on a website that supports openid, the second one _consume_ the authorization authentication from the first openid _server_.

In terms of django and open id, what we have is [djagno-openid](http://code.google.com/p/django-openid/) which let us become a openid consumer and also [django-openid-auth](http://code.google.com/p/django-openid-auth/), which integrates django-openid and [django authentication](http://www.djangoproject.com/documentation/authentication/). It means that when you login with the open id (for me, my open id is http://robertrv.wordpress.com ... ), this openid is linked to the user on the django authentication system, being able to have all the roles (super user, stuff .. etc)

To have it working, what we have to do is mainly use the django-openid-auth [documentation](http://django-openid.googlecode.com/svn/branches/auth-integration/openid.html), where explains the following steps:

- Install [python-openid](http://www.openidenabled.com/python-openid/) (version 1.2 or 2, I tried with 1.2). The documentation says that you have to download the "combo" package, but I didn't found it ... so I installed other two other packages:
    - [urljr](http://openidenabled.com/files/python-openid/files/python-urljr-1.0.1.tar.gz)
    - [yadis](http://openidenabled.com/files/python-openid/files/python-yadis-1.1.0.tar.gz)
- There is a dependency not explained on the documentation: [elementtree.ElementTree](http://effbot.org/media/downloads/elementtree-1.2.6-20050316.tar.gz)
- Then you need the [django-openid](http://code.google.com/p/django-openid/).
- Finally the proper [django-openid-auth](http://code.google.com/p/django-openid-auth/)
- And now, you have an example application on the django-openid-auth named: djopenid\_example. But to have it working you have to apply this [patch](http://code.google.com/p/django-openid-auth/issues/detail?id=18) to the file djopenid\_example/djopenid/views.py

And then you will have the openid working ! I'll try in the future post some more comments to explain how to create users directly with this openid, now is mandatory to create an user and link it to some openid.

UPDATE 20/05/2008: Thanks bosco, obviously is just _authentication_, the _authoritzation_ in this case is internally managed by the openid consumer, in this case django (NOTE: is not good to post so late at night).
