---
layout: post
title: Mysql 프로시저 생성시 특수문자 escape
date: 2017-08-03 17:44:00 +0900
category: Hacking 
---

```
` 
```
```grave accecnt``` or ```back quote``` 라고 한다

애를 파라미터로 입력받는 변수 앞뒤에 넣어서 지정하면 어지간한 injection은 다 막는듯 하다



자세한건 나중에







=> 내용수정 (2018.12.20)

일단 MYSQL 공식 문서에선 back quote 를 문자열 혹은 프로시저 파라미터 변수의 구분값으로 쓴다는 내용은 못찾았다

injection을 막아주지도 못한다 

다만 잘 알려지지 않은 구분자다 보니 일반적인 ' or '1'='1 이런식으로 공격을 날리면 먹히지 않는다

결론

=> injection을 막아주진 못하지만 잘 알려지지 않은 구문자다 보니 공격할때 써볼 것 같진 않다




