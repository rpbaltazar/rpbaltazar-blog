---
id: 80
title: Finding duplicates in PostgresSQL
date: 2014-06-10T08:37:49+00:00
author: rpbaltazar
layout: post
guid: http://balazar.net/random/?p=80
permalink: /2014/06/10/finding-duplicates-in-postgressql/
categories:
  - Computer Science
  - Databases
tags:
  - databases
  - duplicates
  - postgresql
  - rails
  - sql
---
Recently I had the task of finding some duplicate entries in a PostgreSQL database.  
We are using it in our production server and some old entry was duplicate.  
As we needed to be sure that there were none, here&#8217;s what I did to find it out

`<br />
select * from (<br />
  SELECT id,<br />
  ROW_NUMBER() OVER(PARTITION BY merchant_Id, url ORDER BY id asc) AS Row<br />
  FROM Photos<br />
) dups<br />
where<br />
dups.Row > 1<br />
` 

OVER PARTITION works similarly to a GROUP BY but without getting the records merged in one entry

References:  
http://www.postgresql.org/docs/9.1/static/tutorial-window.html  
http://stackoverflow.com/questions/14471179/find-duplicate-rows-with-postgresql