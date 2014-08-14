---
layout: post
title: "Python Learning on"
date: 2014-02-08 07:40
comments: true
categories: [python, programming]
---

###Knowledge Points

####list
>creates lists from iterables.

####else Clauses on Loops ([python doc](http://docs.python.org/3/tutorial/controlflow.html#break-and-continue-statements-and-else-clauses-on-loops) equals `if no break else do`)
>When used with a loop, the else clause has more in common with the else clause of a try statement than it does that of if statements: a try statement’s else clause runs when no exception occurs, and **a loop’s else clause runs when no break occurs.**

	for n in range(2, 10):
	  for x in range(2, n):
	    if n % x == 0:
	      print(n, '=', x, '*', n // x)
	      break
	  else:
	    print(n, '是素数')

####varible scope ([view in python doc](http://docs.python.org/3/tutorial/controlflow.html#defining-functions))
>The execution of a function introduces a new symbol table used for the local variables of the function. More precisely, all variable assignments in a function store the value in the local symbol table; whereas variable references first look in the local symbol table, then in the local symbol tables of enclosing functions, then in the global symbol table, and finally in the table of built-in names. Thus, **global variables cannot be directly assigned a value within a function** (unless named in a global statement), although they may be referenced.

####default values in function definition ([Default Argument Values](http://docs.python.org/3/tutorial/controlflow.html#default-argument-values))
>The default values are evaluated(and evaluated only once) at the point of function definition in the defining scope, so that

	i = 5

	def f(arg=i):
	    print(arg)

	i = 6
	f()
>will print 5.
