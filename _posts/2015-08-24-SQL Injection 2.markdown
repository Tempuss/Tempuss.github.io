---
layout: post
title: SQL Injection 2
date: 2015-08-24 12:26:00 +0900
category: Hacking 
---
보통 많은 개발자들이 SQL Injection을 막기위해 Magic_Quotes_gpc라는 PHP의 옵션을 사용했었다.

'나 sql injection에 사용되는 특수문자의 앞에 \를 추가해서 필터링 하는 방식이었다. 

하지만 magic_quotes_gpc에는 취약점이 많았다. 

GET/POST/Cookie로 받는 방식만 필터링을 했었다. 또한 DB에서 가져오는 값에서는 escaping 되지 않았기 

때문에 많은 사람들이 magic_quotes_gpc기능을 끄고 mysql_real_escape_string함수를 사용하는 편이 더 안전하다고 추천한다. 하지만 아직은 많은 사람들이 magic_quotes_gpc를 믿고 있다. 또한 많은 개발자들이

magic_quotes_gpc만 믿어서 그런진 몰라도 PHP 5.4 부터는 아예 삭제되었다. 



magic_quotes_gpc를 우회하는 가장 쉬운방법은 멀티바이트 인코딩을 사용하는 것이다.

mb_convert_encoding이라는 함수를 사용하는 환경에서만 가능하다. 언어셋을 바꾸는 함수이다.

만약 magic_quotes_gpc가 on 되어있는 서버에 인젝션을 날리게 되면

1\' 이렇게 인식한다. 



그런데 여기에다가 %bf%5C라는 값을 넣어주면은 우회가 된다.

%bf%5c라는 값을 한글자로 인식해버린다. %5c는 \이다 %bf%5c%27에서 \를 무시해버려서 우회가 가능하다.



addslashes()라는 함수도 있다. 하지만 이 함수도 비슷한 방법으로 우회가 가능하다.



때문에 인젝션을 막을떄는 addslashes()나 magic_quotes_gpc등을 믿지말고

mysql_real_escap_string함수를 사용하는 것이 가장 안전하다. 



 그외에도 다양한 내용이 있지만 기억나는대로 추가하겠습니다.



