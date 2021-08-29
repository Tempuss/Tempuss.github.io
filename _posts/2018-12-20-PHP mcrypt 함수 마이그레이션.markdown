---
layout: post
title: PHP mcrypt 함수 마이그레이션
date: 2018-12-20 17:17:00 +0900
category: Web 
---

PHP가 버전 업그레이드를 함에 따라 
레거시 버전 PHP에서 사용하던 mcrypt_encrypt 관련 암호화 함수들을 쓰기 힘들게 됬다





때문에 openssl_encrypt 함수를 



만약 레거시 코드에서 mcrypt_encrypt 암호화 방식에서 AES 암호화로 MCRYPT_RIJNDAEL_128를  사용했다면 


openssl_encrypt에선 AES-256-CBC로 사용하면 레거시 코드와 호환이 가능하다 





복호화도 동일 



php7.2부턴 mcrypt 사용이 불가능 하기 때문에 openssl_encrpyt를 써야 한다 
레거시 코드를 마이그레이션 할때 만약 mcrypt를 사용했다면 참고




