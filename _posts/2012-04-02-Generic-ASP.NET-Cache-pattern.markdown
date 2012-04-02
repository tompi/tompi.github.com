---
layout: post
title: Generic cache wrapper for the asp.net HttpCache
---
I seem to search for this little nugget every now and again without finding it on the net, so here it is. I really can't take credit for it, I think it was the <a href="http://github.com/bentster" alt="bentster">bentster</a> who wrote it first time I saw it, but not really sure...

What to cache
-------------

Typical usage is data for populating dropdown lists with options which doesn't change too often, like once a day. This is probably the most frequently used data from a database, so making the app hit the db only once per day(per list) can really make a difference if you have some load.

How to cache
------------

The ASP.NET HttpCache is really simple and can be used for all types of .net applications(I have used it mainly in web-apps, but also in a wcf-project). The reason for having the caching logic isolated in a class is it's really easy to get the locking wrong.

Le code
-------

There really isn't much to it, except for the double checking. 

	public class Cache<T> where T : class
	{
		public T Get(object lockObject, string key, Func<T> getFunction, int hoursToCache)
		{
			var result = HttpRunTime.Cache.Get(key);
			if (result == null)
			{
				lock (lockObject)
				{
					result = HttpRunTime.Cache.Get(key);
					if (result == null)
					{
						result = getFunction();
						HttpRunTime.Cache.Insert(key, result, null, DateTime.UtcNow.AddHours(hoursToCache), Cache.NoSlidingExpiration);
					}
				}
			}
			return (T) result;
		}
	}

Your only concern using it is which lock-object to give it. I usually make a "retriever" class for each list I need, and give the cache the typeof(MyListRetriever) to use for locking.

TODO: usage example and lambda with param

