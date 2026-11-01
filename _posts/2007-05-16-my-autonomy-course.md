---
title: "My autonomy course"
date: 2007-05-16
categories: 
  - "software-development"

---

If you say, _what a hell is that ?_ then you are in the same position as me when I started the course... today I have started my [Autonomy](http://www.autonomy.com) course (well, the course is from the 15th to the 18th of May), which is related to my job, in fact is a course that my boss decided that I have to go, then asked me if I is all right to me ... I am learning Autonomy and that realizing that things works in that way in London! The course is in Cambridge, a really beautiful place, but if you go from the station to the office and back again then is not that nice....

Well, Autonomy is a big _and expensive_ piece of software with the main purpose of indexing things (but my teacher will say that is also to categorize, suggest, and homogenize data), the good point of this software is that can be parametrized to access lot of different kind of data, what means that the data source can be heterogeneous. Let's think about a typical medium/large company (an small one would never be able to reach this kind of software) building process: <!--more-->

1. It normally starts as an small (or not so small) company, but from the first point this companies needs some kind of IS (Information System) support, which normally is the cheapest and the fast => M$ Access !

3. Then it starts growing, what means that it increase the number of customers, the number of employees, etc. And even it just extends its market. From the IT point of view, the best would be to have an integrated software for this, but this rarely happens, what use to happen is to have different software for different (but related) things
4. This process is more emphasized when the company is bigger, and normally never stops.

What we can see here is the normal perspective of any medium/big company, the problem is when we want to integrate all the data, like the different products coming from the different data sources, also take lot of time learning what is the correct format and transforming from one data to another, the solutions is suppose to be _Autonomy_. In fact that is what Autonomy people told as _the hidden 80%_, which is in average the part of company data that is unstructured (word, excel, pdf, etc...).

This search engine (because I would say that has hardly lot of similarities with Google/Yahoo/etc, but directed to companies), is able to _connect_ with lot of different data sources, like simply reading from the file system, or from any kind of database (let's say that this database can be Oracle, mysql, etc, etc.... or share point, ldap, etc ... ), and the last and probably the most impressive connector from autonomy is the _Http Fetch Connector_ which can index content on internet! Which means an spider to index this content inside our search engine.

Another good point of Autonomy is that it can search over different type of files (they say about 700), which means that this search engine can read a pdf, ppt, doc, excel, ps and extract the data itself (which will be searchable), store the most important data and save any link (this has to be parametrized a bit) to the original file. Also it can do the inverse process, display the pdf/ppt/xls ... as an html file, which is useful to highlight the keywords we are searching (again in the same way google does). The most impressive file types that this software recognize are the media types ... yes, it can index directly sound files (mp3, wav, etc....) extracting the information, and also (never seen) video files extracting possible textual information (car plate number) or face recognition information ... this can be directly plugged to read information coming from internet (ie: from the online TV's)

Also interesting is the types of queries, it has the typical queries and also something named "Conceptual" query, which is very similar to the google way of query. If you ask for Carrot, it can retrieve also documents talking about what the rabbits eat, because rabbits and carrots are conceptually near. This conceptually near can be extended to the users of the search machine, i.e: we can

As a fast comparison with Google Search Engine, we can have also Alerts (that alerts us when the number of results has changed), also we can have a desktop version of the search engine, we can have the mobile version to access the data, etc, etc. Also have some API to access it, even though the API is just a wrapper which sends direct HTTP request to the engine.

As you can see this software seem to be really good software engine, but has lot of problems on the administration part ... all the configuration files are a bit cryptic and not very well documented. If I have the opportunity to suffer it more probably I will explain it better, and with more knowledge about it.

Update _2007-05-19_ I have finalized the course, the global idea of the course is to have an overview of the main capacities of this software, was a bit "step-by-step" based, and sometimes we where just like machines, without thinking that much ... and the time was really just, but I have done it and this is enough.

About the project, well, seem to be really one of the most powerful products related with document searching. I really like the idea of auto-index new data from the company, or the idea of fetching WWW documents (document can be text, pdf, audio or video!), or even the possibility to index really big amount of data (like 10-20 billions of documents, in a big clustered scenario) and the inherited security from the document files, but of course one thing is what they say and another thing is who complex is to get this working.

The bad point is the documentation, when we where doing things the teacher knows hardly all the commands, but to learn how to do things by our-self would not be as easy, also where to find documentation is not really easy, they have different documentation in different places per each product. Another bad point, as all the big software products, is that they are planning to do lot of things but most of them are not finished, like the new DashBoard to control all the software (we have done hardly everything by hand).

The final perception of the software is that is really a good piece of software but you need some time to use it, and to get real benefit of it.
