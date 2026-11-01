---
title: "New MMB may '08: fragmentation solutions?"
date: 2008-05-05
categories: 
  - "mmb"
  - "software-development"
tags: 
  - "fragmemtation"
  - "mobile"

---

Hello Again everybody (yes, everybody is just the 5 friends who read this blog :P).

Today I have gone to the Mobile Monday Barcelona, this time I think there where less people than usual, but as usual we had some talks, some good and some other not as good, most of them related to the way to write application to the most part of existing devices:

<!--more-->

1. An explanation about the Nokia Forum, and also talking about the way the distribute. They still don't have a advertisement model, but they do have a distribution model for the developed applications.
2. [Yahoo! mobile group](http://mobile.yahoo.com/), shown us what they are doing, mainly developing a software for their platform, which will be the same source for web (using witdgets on the [mobile yahoo home page](beta.m.yahoo.com)) and for the local application ([yahoo go!](http://mobile.yahoo.com/go;_ylt=AuZ43kriMFQuVSGDJXAPH6K_tQcJ)). As always are in beta stages, and have some cool widgets or applications \[\*1\]. This approach tries to get a very limited API (just using XForms, nothing of the native features: comunications, contacts, and so), but a large amount of covered devices.
3. The other interesting approach is to use a profiling method. This approach was explained by Vincent Berge from [Mobile Distillery](http://www.mobile-distillery.com/), who showed us some screen cast of its profiler which is able to use just one source code to compile to a broad number of JavaMe devices. What it does is just using a special API for some specific and painful tasks (like bluetooth or NFC) implemented by them, and also have the profiler to let you write your application inside your code discriminating between the type of device you are running. It uses a remote located database (updated by themselves) of more than 1000 of devices with all the features of each device, that lets the profiler compile and generate code for any kind of device (you have to generate for each kind); the key name is Alembic. It also have support for [Brew](en.wikipedia.org/wiki/BREW) and even for google android (but obviously on a beta stage). One of the screen cast shows how to develop with it's platform over Netbeans, which seems to start becoming the standard de-facto IDE for mobile development (and also seems really easy to do it, as all the presentations).
4. Finally there was a short presentation talking about the way that developer and designers should design mobile applications, to avoid the famous devices fragmentation.

I have to say that the second and the third (as you can suppose) where my favorites, seems to be good approaches and even compatible... it will be good to have someone from Google mobile division (although the yahoo guy was a googler before, but now seems to be really yahooed :P).

Some other thing that I want to notice is the fact that the number of mobile devices is about 10 times bigger that the number of personal computer, that's something that nobody (at least nowadays) is taking advantage of !

Thanks for reading, I hope I can post another thing before the next MMB that will be about [microblogging](http://en.wikipedia.org/wiki/Micro-blogging). (the MMB guy also talked about a mobile congress in barcelona about web 2.0, this will be really interesting !).

\[\*1\] Like Yahoo oneSearch, that gives you "intelligent" searches ... like if you search for "fc barcelona" it will return the last and the future results of the soccer club. But also giving located searches.
