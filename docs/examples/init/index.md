---
layout: default
---

# Init From the Ground Up

This is an example program that works similarly to `git init`.
Many of the options available to the git command line tool map easily to concepts in libbtc.

Note that a large portion of the code deals with the command-line interface.
This article is about the portions of the code that deal with libbtc, so we'll be skipping all the argument parsing and such.

## Main

Let's skip the frontmatter, and jump straight to the meat of this thing.
The `main` function starts off with some boilerplate and a bit of command-line parsing noise, which we'll ignore for the purposes of this article.

```c
int main(int argc, char *argv[])
{
	
```

## What's next?
Go [back to the Learning center](/docs) for more, or check out [the API documentation](http://libbtc.github.io/libbtc/).
