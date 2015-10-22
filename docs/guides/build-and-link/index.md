---
layout: default
---

# How to Build libbtc

There is no One True Way™ to use an open-source C library.
This article provides some guidance on how to use libbtc with various build/project tools.

## Basic Build

libbtc is developed with autotools, and this will be the easiest way to build a binary from the source.
Once you have autotools installed, performing a libbtc build is fairly simple.

```bash
$ ./autogen
$ ./configure
$ make
$ make check
```

## Advanced Build

TBD

# Linking and Usage

Once you have a build, you probably want to use it from within your application.
You'll need to include `btc/btc.h`, and link to the binaries you built previously.