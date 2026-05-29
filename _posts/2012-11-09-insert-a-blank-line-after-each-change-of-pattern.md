---
layout: "post"
title: "Insert a blank line after each change of pattern"
date: "2012-11-09 22:20:20"
last_modified_at: "2012-11-09 22:23:46"
author: "melmeric"
permalink: "/blog/2012/11/insert-a-blank-line-after-each-change-of-pattern/"
categories:
  - "technology"
tags:
  - "blank"
  - "text"
  - "vim"
category_names:
  - "Technology"
tag_names:
  - "blank"
  - "text"
  - "vim"
comments: false
sitemap: false
wp_id: 893
wp_slug: "insert-a-blank-line-after-each-change-of-pattern"
permalink_slug: "insert-a-blank-line-after-each-change-of-pattern"
wp_url: "https://gdfm.me/2012/11/09/insert-a-blank-line-after-each-change-of-pattern/"
---

<pre>:g/^\(\w\+\).*\n\1\@!./pu_</pre>
Inserts a blank after every line that does not start with the same word as the immediately following line.
Extremely useful for .tsv and .csv files.
(might need some tweaking for non-word characters)
Vim awesomeness.
