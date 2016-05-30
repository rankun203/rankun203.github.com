title: Node.JS Tips
date: 2015-09-05 08:44:14
categories:
- node.js
- note
tags:
- javascript
- node.js
- note
---

## Express

- Route name couldn't be `/accounts`, 404 raised after that.

## Node.JS

- Cross require lead target class becomes an empty Object!
  > In order to prevent an infinite loop, an unfinished copy of the a.js exports object is returned to the b.js module. b.js then finishes loading, and its exports object is provided to the a.js module. ----https://nodejs.org/api/modules.html
