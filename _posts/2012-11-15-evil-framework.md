---
layout: post
title: "Evil Framework"
tagline: "about non orderd but distinct select"
description: "short story about my first problem woth EF"
category: ['C#']
tags: [EF, Entity, Entity Framework, Framework, SQL]
---
{% include JB/setup %}

I was able to create some stuff using EF. I must admit that EF is nice tool. It help a lot with basic daily database work. 
I’m not very experienced ORM user, but must admit - EF is so easy to use and got all features of LINQ expressions.
I was amazed how easy I can add new table to in DB and then just use it. Some problems occurs when DB lose track with code
(e.g. local development db) but are pretty easy to detect. Another great thing in EF is designer. 
Just create desired data model and then generate tables from it. So, why EF is evil?

I have to get some data from DB. To do it I must join 3 tables. Quite easy... but not for me. 
I also have to order data and select them distinct. Still not hard task, less than 10 lines of formatted SQL query. 
I created something similar to

	from table1 t1
	from table2 t2
	from table3 t3
	where 	t1.id == desired.id && 
		t2.table1_id == desired.id &&
		t2.table3_id == table3.id &&
		t3.isDesired == true
	orderby t1.order
	select t1.Object

OK, query worked but as a result I got each value multiple times. No problem, I can use `Distinct()` 
Not so easy. When I tried that my list got shuffled. I was confused and search for solution. 
Firstly I wanted put distinct keyword somewhere in query. But I can’t. Second try was to omit `orderby` in query and put it after list. 
Hopefully I can use one filed in `t1.Object` to store data from `t1.order` and sort by it.
Problem was that you can only call constructors in this select statement - `Object` have only FactoryMethod. 
Because table1 contain small data, I could take `t1` entities and after distinct them and sort, exclude from them list of `Object`s.

Another approach is use grouping showed
[here](http://imar.spaanjaars.com/546/using-grouping-instead-of-distinct-in-entity-framework-to-optimize-performance)
I’ve got working solution so I put a little effort to read this article and promise to fix it when
I do other more important stuff.
