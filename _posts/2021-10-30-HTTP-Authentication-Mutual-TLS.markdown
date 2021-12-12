---
layout: post
title: HTTP-Authentication-Mutual-TLS
date: 2021-10-30 23:05:00 +0900
category: Web  
---

# HTTP Authorization

## TLS?

---

- Transport Layer Security (전송계층 보안)
- 즉 클라이언트와 서버간의 별도의 TLS 인증서를 공유하면서 해당 공유서가 인증된 경우에만 통신을 허용한다는것
- 이 기술을 이용하면 외부망에서도 내부망처럼 특정 서버들  끼리만 통신을 할 수 있는 환경을 구축할 수 있다
- TLS의 기반은 PKI와 X.509 인증서임

- 일반적으로 TLS는 클라이언트에서 서버에 대한 증명하도록 되어있고 클라이언트에 대한 인증은 애플리케이션 계층에서 처리하도록 되어 있음
⇒ 애플리케이션 계층은 7계층으로 HTTP 프로토콜에서 알아서 클라이언트를 인증하라는 것으로 우리가 
일반적으로 아는 세션기반 인증, 토큰 기반 인증과 같은 HTTP 프로토콜을 기반의 인증을 통해 클라이언트를 인증하라는 뜻임
- 다만 mTLS는 일반적인 Web Application의 비즈니스 로직에서 인증을 처리하는것과 달리 클라이언트에 대한 인증을 전송계층(4계층), 응용계층(5계층)에서 서버↔ 클라이언트간 상호 인증 기능을 제공한다는 뜻이다

![Untitled](/assets/img/Mutual-TLS/Untitled.png)

- 다만 mTLS는 강력한 보안성을 제공하기 때문에 아주 높은 보안성을 요구하는 시스템이나 B2B 애플리케이션에 사용된다

## 구현

---

![Untitled](/assets/img/Mutual-TLS/Untitled 1.png)

![Untitled](/assets/img/Mutual-TLS/Untitled 2.png)

![Untitled](/assets/img/Mutual-TLS/Untitled 3.png)

## Reference

---

- [X.509란 무엇인가?](https://www.ssl.com/ko/%EC%9E%90%EC%A3%BC-%EB%AC%BB%EB%8A%94-%EC%A7%88%EB%AC%B8/x-509-%EC%9D%B8%EC%A6%9D%EC%84%9C-%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9E%85%EB%8B%88%EA%B9%8C/)
- [x.509 위키](https://ko.wikipedia.org/wiki/X.509)
- [NodeJS mTLS setting](https://medium.com/geekculture/mtls-with-nginx-and-nodejs-e3d0980ed950)
- [kuberntes-Mutual-TLS](https://velog.io/@idnnbi/kuberntes-Mutual-TLS)
- [k8s 인증 완벽이해 #1 - X.509 Client Certs](https://coffeewhale.com/kubernetes/authentication/x509/2020/05/02/auth01/)