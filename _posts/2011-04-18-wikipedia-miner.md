---
layout: post
title: "Wikipedia Miner"
date: 2011-04-18
categories: ["PhD", "Technology"]
tags: ["data mining", "Wikipedia"]
author: "melmeric"
permalink: /2011/04/18/wikipedia-miner/
---

I have been playing with [Wikipedia Miner](http://wikipedia-miner.sourceforge.net/) for my new research project. Wikipedia Miner is a toolkit that does many interesting things with Wikipedia. The one I am using is *"wikification"*, that is "The process of adding wiki links to specific named entities and other appropriate phrases in an arbitrary text." It is a very useful procedure to enrich a text. "The process consists of *automatic keyword extraction*, *word sense disambiguation*, and automatically adding links to documents to Wikipedia". In my case, I am more interested in topic detection so I care only about the first two (emphasized) phases.

Even though the software is a great piece of work, and the online demo works flawlessly, setting it up locally is a nightmare. The main reason is the very limited documentation. The main problem is that the Requirements section is missing all the version numbers for the required software.

To prevent others from suffering my same trial, I write here what I discovered about the set up of Wikipedia Miner.

	
- **MySQL**. You can use any version, but beware if you use version 4. Varchars over 255 in length get automatically converted to the smallest text fields that can contain it. Because text fields can not be fully indexed, you need to specify how much of it you want to index. Otherwise you will get this nice exception "java.sql.SQLException: Syntax error or access violation message from server: BLOB/TEXT column used in key specification without a key length". Therefore, to make it work, add the bold/underlined parts (that specify the index length) to WikipediaDatabase.java:150 and recompile.

`
createStatements.put("anchor", "CREATE TABLE anchor ("
+ "an_text varchar(300) binary NOT NULL, "
+ "an_to int(8) unsigned NOT NULL, "
+ "an_count int(8) unsigned NOT NULL, "
+ "PRIMARY KEY (an_text***(300)***, an_to), "
+ "KEY (an_to)) ENGINE=MyISAM DEFAULT CHARSET=utf8;") ;
`
`
createStatements.put("anchor_occurance", "CREATE TABLE anchor_occurance ("
+ "ao_text varchar(300) binary NOT NULL, "
+ "ao_linkCount int(8) unsigned NOT NULL, "
+ "ao_occCount int(8) unsigned NOT NULL, "
+ "PRIMARY KEY (ao_text***(300)***)) ENGINE=MyISAM DEFAULT CHARSET=utf8;");
`
	
- **Connector/J**. Use version 3.0.17 or set the property jdbcCompliantTruncation=false. If you don't you will get a nice "com.mysql.jdbc.MysqlDataTruncation: Data truncation" exception.
	
- **Weka**. Use version 3.6.4, otherwise you will get deserialization exceptions when loading the models (in my case "java.io.InvalidClassException: weka.classifiers.Classifier; local class incompatible: stream classdesc serialVersionUID = 6502780192411755341, local class serialVersionUID = 66924060442623804").

So far I din't have any problems with trove and servlet-api.

This confirms a well know fact: that one of the biggest problems of open source is lack of documentation. I should learn from this experience as well :)

I hope this spares some hours of work to somebody.

And kudos to David Milne for creating and releasing Wikipedia Miner as open source.
This is the proper way to do science!