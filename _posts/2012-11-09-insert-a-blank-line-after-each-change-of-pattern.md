---
layout: post
title: "Insert a blank line after each change of pattern"
date: 2012-11-09
categories: ["Technology"]
tags: ["blank", "text", "vim"]
author: "melmeric"
permalink: /2012/11/09/insert-a-blank-line-after-each-change-of-pattern/
---

```
:g/^\(\w\+\).*\n\1\@!./pu_
```

Inserts a blank after every line that does not start with the same word as the immediately following line.
Extremely useful for .tsv and .csv files.
(might need some tweaking for non-word characters)

Vim awesomeness.