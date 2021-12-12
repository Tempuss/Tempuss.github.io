---
layout: post
title: HTTP Authorization
date: 2021-10-17 23:05:00 +0900
category: Web  
---

# HTTP Authorization

## 1. Basic 인증

---

- 클라이언트에서 사용자 이름과 암호를 base64인코드 하고 인증하는 방식
- 사실상 평문에 가깝다 보니 스니핑 공격에 취약하고 널리 쓰이지 않는 인증 방식
- 연관된 인증 방식들
    - Apache와 Basic 인증으로 접근 제한
    - nginx와 Basic 인증으로 접근 제한
    - [URL에 인증 정보를 사용하여 접근](https://developer.mozilla.org/ko/docs/Web/HTTP/Authentication#url%EC%97%90_%EC%9D%B8%EC%A6%9D_%EC%A0%95%EB%B3%B4%EB%A5%BC_%EC%82%AC%EC%9A%A9%ED%95%98%EC%97%AC_%EC%A0%91%EA%B7%BC%ED%95%98%EA%B8%B0)
        - ctf에 가끔 나왔던 인증 방식으로 현재 크롬 버전에서는 기능상 제거를 시작함
        
        ```jsx
        https://username:password@www.example.com/
        ```
        

    ![Untitled](/assets/img/HTTP-Authentication/Untitled.png)

## 2. Digest 인증

---

- 사용자 정보를 조합하여 md5해시를 만든 후 인증하는 방식
- 절대 비밀번호를 네트워크를 통해 보내지 않겠다는 마인드의 인증 방식

![Untitled](/assets/img/HTTP-Authentication/Untitled 1.png)

## 3. Form base 인증

---

- 사용자 정보를 전송 후 세션과 쿠키를 이용한 인증 방식

![Untitled](/assets/img/HTTP-Authentication/Untitled 2.png)

## 4. Bearer 인증

---

- 사용자 정보를 이용한 인증 후 짧은 유효기간의 토큰을 발급하여 인증하는 방식
- jwt 토큰은 그 종류 중 1개
- 이때 토큰은 header, token, signature로 구성되어 있으며 실제 문자열 방식은 아래와 같음
    
    헤더에는 **토큰 타임과 해싱 알고리즘 정보**를 저장하고, payload에는 담고자 하는 일부 **사용자 식별 정보 + 추가 정보**가 담기며 Signature에는 header에 명시된 해싱 알고리즘으로 **해싱된 해시값**이 저장된다
    
    이때 해싱할때는 보통 서버측만 알고 있는 secret 값을 salt 값으로 사용해서 무결성을 보장한다
    (이렇게 될 경우 secret 값을 모르면 클라이언트 측에서는 토큰에 대한 조작이 불가능해 진다)
    
    ![Untitled](/assets/img/HTTP-Authentication/Untitled 3.png)

    

![Untitled](/assets/img/HTTP-Authentication/Untitled 4.png)


## 5. HOBA 인증

---

- 전자 서명 기반 인증 (RFC 7486)
- 관련 자료가 별로 없음;; 추가 리서치 필요

## 6. Mutual 인증

---

- SSL인증서를 이용한 클라이언트-서버 상호 인증 (draft-ietf-httpauth-mutual)

## 7. AWS4-HMAC-SHA256 인증

---

- AWS 전자 서명 기반 인증 ([링크](https://docs.aws.amazon.com/AmazonS3/latest/API/sigv4-auth-using-authorization-header.html))

### Reference

---

- [토근 기반 인증에서 bearer는 무엇일까?](https://velog.io/@cada/%ED%86%A0%EA%B7%BC-%EA%B8%B0%EB%B0%98-%EC%9D%B8%EC%A6%9D%EC%97%90%EC%84%9C-bearer%EB%8A%94-%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C)
- [HTTP 인증 방식에 대해 설명](https://velog.io/@rmfrn2901/HTTP-%EC%9D%B8%EC%A6%9D-%EB%B0%A9%EC%8B%9D%EC%97%90-%EB%8C%80%ED%95%B4-%EC%84%A4%EB%AA%85)
- [HTTP 표준 문서](https://developer.mozilla.org/ko/docs/Web/HTTP/Authentication)
- [토근 기반 인증에서 bearer는 무엇일까?](https://velog.io/@cada/%ED%86%A0%EA%B7%BC-%EA%B8%B0%EB%B0%98-%EC%9D%B8%EC%A6%9D%EC%97%90%EC%84%9C-bearer%EB%8A%94-%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C)
- [인증 방식과 프로세스 비교](https://velog.io/@ljinsk3/%EC%9D%B8%EC%A6%9D-%EB%B0%A9%EC%8B%9D%EA%B3%BC-%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4-%EB%B9%84%EA%B5%90)
- [jwt 공식](https://jwt.io/) 문서
- [[JWT] JSON Web Token 소개 및 구조](https://velopert.com/2389)
- [https://showerbugs.github.io/2017-11-16/OAuth-란-무엇일까](https://showerbugs.github.io/2017-11-16/OAuth-%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C)
- [HTTP Digest 인증 문제 경험기](https://remocon33.tistory.com/631)
- [다이제스트 인증 (1) - 다이제스트 인증과 특징](https://feel5ny.github.io/2019/11/24/HTTP_013_01/)

