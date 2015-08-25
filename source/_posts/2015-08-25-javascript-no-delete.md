title: Javascript no delete
date: 2015-08-25 22:43:15
categories:
- programming
- note
tags:
- node.js
- note
---

> Operator `delete` is unexpectedly slow!

> Delete is the only true way to remove object's properties without any leftovers, but it works ~ 100 times slower, compared to it's "alternative", setting object[key] = undefined.

http://stackoverflow.com/a/21735614/1904043