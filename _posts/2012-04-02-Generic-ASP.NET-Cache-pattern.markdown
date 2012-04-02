---
layout: post
title: Generic cache wrapper for the asp.net HttpCache
---
I seem to search for this little nugget every now and again without finding it on the net, so here it is...

What to cache
-------------

Typical usage is data for populating dropdown lists with options which doesn't change too often, like once a day. This is probably the most frequently used data from a database, so making the app hit the db only once per day(per list) can really make a difference if you have some load.

How to cache
------------

The ASP.NET HttpCache is really simple and can be used for all types of .net applications(I have used it mainly in web-apps, but also in a wcf-project). The reason for having the caching logic isolated in a class is it's really easy to get the locking wrong.

Le code
-------

There really isn't much to it, except for the double checking. 

	Somecode('hmm');

Your only concern using it is which lock-object to give it. I usually make a "retriever" class for each list I need, and give the cache the typeof(MyListRetriever) to use for locking.

Here's a simple example:

	Somemorecode('haha', 1);


