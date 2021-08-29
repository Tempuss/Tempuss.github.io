---
layout: post
title: SQL Injection FOUND_ROWS
date: 2019-07-14 12:05:00 +0900
category: Hacking 
---

```mysql
select host from user_tb where host='m0ai' and if(FOUND_ROWS()<1, sleep(1), sleep(2)) && '1'='1';


```
