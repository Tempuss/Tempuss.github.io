---
layout: post
title: PHP Type Confusion 
date: 2018-12-20 16:18:00 +0900
category: Hacking 
---
PHP는 자료형을 선언하지 않는 언어이다 보니 
데이터를 비교할때 ==(느슨한 비교, 내부의 데이터만 비교) 보다는 ===(강력한 비교, 자료형과 데이터가 모두 일치해야 참)를 사용하는것이 좋다


실제 예로 



```
<input type="text" value=[]>
```

같이 front에서 배열 형태로 보내는 값을 back 단에서 ==으로 비교하게 될 경우에 문제가 생긴다





예를 들어
```
"abcd" == "abcd"  (True)
```
이렇게 비밀번호를 입력받아 비교하는 로직이 있을경우에 

front 쪽에서 배열로 보내서 비교를 하게되면 


```
[] == "abcd" (True)
```


True를 반환해버리는 오류가 발생한다 
PHP는 자료형이 없기때문에 특히나 조심해야 하는 부분

물론 이게 터질만큼 대충 짜논 사이트가 많지는 않겠지만 워낙 레거시 스타일로 작성된 PHP 사이트가 많아서 터질 가능성도 있다 혹은 오류가 나거나

참고 
http://phpcheatsheets.com/compare/


