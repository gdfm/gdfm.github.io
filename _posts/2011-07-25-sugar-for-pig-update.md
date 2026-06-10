---
layout: "post"
title: "Sugar for Pig update"
date: "2011-07-25 21:26:17"
last_modified_at: "2011-07-25 21:26:17"
author: "melmeric"
permalink: "/blog/2011/07/sugar-for-pig-update/"
categories:
  - "technology"
tags:
  - "gsoc"
  - "pig"
  - "syntactic-sugar"
comments: false
---

Actually it should not be an update, but a wrap-up, as I basically have finished my project for this year. My last patch already got a [+1](http://www.apache.org/foundation/voting.html) and it's just waiting for the tests to finish to be committed.
I completed my selected tasks [PIG-1926](https://issues.apache.org/jira/browse/PIG-1926) and [PIG-1904](https://issues.apache.org/jira/browse/PIG-1904) (see my [previous post](/blog/2011/04/sugar-for-pig-gsoc11/) for an explanation of what they do), plus some more small fixes here and there: [PIG-2156](https://issues.apache.org/jira/browse/PIG-2156) [PIG-2136](https://issues.apache.org/jira/browse/PIG-2136) [PIG-2060](https://issues.apache.org/jira/browse/PIG-2060) [PIG-2026](https://issues.apache.org/jira/browse/PIG-2026) [PIG-2025](https://issues.apache.org/jira/browse/PIG-2025) [PIG-2024](https://issues.apache.org/jira/browse/PIG-2024)
I also gave some longer term ideas on how to refactor the grammar to make it safer and easier to modify, and on some new features: [PIG-2138](https://issues.apache.org/jira/browse/PIG-2138) [PIG-2123](https://issues.apache.org/jira/browse/PIG-2123) [PIG-2119](https://issues.apache.org/jira/browse/PIG-2119) [PIG-2047](https://issues.apache.org/jira/browse/PIG-2047)
However, given that I have still 1 month left before the official end of the GSoC, I will tackle the rest of the "Sugar" projects listed on the [PIG GSoC page](http://wiki.apache.org/pig/GSoc2011), which means adding syntax support for Tuple/Map/Bag conversions: [PIG-1387](https://issues.apache.org/jira/browse/PIG-1387)
All my fixes will go in Pig 0.10, as 0.9 has already been branched and will be out very soon.
Working on the front end has been a very interesting and enriching experience.

- I got to learn how to use ANTLR (my mentor called me an "ANTLR expert" :P).
- I learned how Pig scripts are compiled and how to work with the logical, physical and mapreduce levels.
- I have a full understanding of the workflow and the dataflow of the operators in Pig. I am sure this will come in handy in the future.
- I also increased my proficiency in Pig/Latin scripting.
- Finally, I really got to seriously use and appreciate git. It makes working on different patches at the same time a breeze.

See you in a month for the actual wrap-up!
