#Caching

You should always try to cache resources as much as possible. Caching helps
reduce the load on the servers. Caching pretty much doesn't have drawbacks,
except maybe the first cache overhead, and cache stampede which can occur in
the event of cache being expired.

## Cache Stampede
Cache stampede is a problem that occurs when for example several clients request
the same content at the same time. While a cache of the content remains in the system
the requests hit the cache and thus it lowers the load on the servers. When on the
other hand the cache expires, if we have many requests coming at the same time,
a parallelized server farm may experience request timeouts, provoked by the cache
stampede. What is happening in the background is that all simultaneous requests
access the required resource, render it and try to cache it in the system, at
basically the same time. This may itself be enough to trigger congestion collapse
of the system.

**Congestion collapse** occurs when multiple requests are maid to the same choke
point in the system, thus ingoing traffic is bigger than outgoing.

As the system is congested, each request is updating the cache, with no way
of knowing that the other requests have updated it, and no outgoing traffic can
reach the client in time, and hence a timeout is observed.

## Workaround / Fix

A possible fix for this may be preparing the new cached version of the document, before the old cache has expired.
