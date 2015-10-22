---
layout: toc
---

<h1>libbtc Samples</h1>

<h2 id="best_practices">Best Practices</h2>

<h3 id="best_practices_init">Initialize the library</h3>

The library needs to keep some global state and initialize its
dependencies. You must therefore initialize the library before working
with it

```C
btc_start(); //will initialize ecc environment, etc
```

Usually you don't need to call the shutdown function as the operating
system will take care of reclaiming resources, but if your application
uses libgit2 in some areas which are not usually active, you can use

```C
btc_stop();
```

to ask the library to clean up the global state. The cleanup will be
performed once there have been the same number of calls to
`btc_stop()` as there were for `btc_start()`.

<h3 id="best_practices_freeing">Freeing</h3>

Anytime libbtc fills in a non-`const` pointer for you, you should be using a `_free` call to release the resource.

```c
btc_tx *repo = NULL;
btc_tx_init(&repo, "/tmp/…", false);
/* … */
btc_tx_free(repo);
```

([`_free` APIs](http://libbtc.github.com/libbtc/#HEAD/search/_free))

