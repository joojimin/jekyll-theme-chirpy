---
title: Mac Tomcat https setting
date: 2020-12-21 18:00:00 +0900
categories: [Tech, Tomcat]
tags: [tomcat, tech, https, mac]
comments: true
---

***local tocat을 띄을때 https(default port 443) 요청을 위한 인증서를 셋팅해보자***

---
<br>
1.  ***OpenSSL 설치***<br>
    인증서 암호화를 위한 툴 설치<br><br>
    <code>
    brew install openssl
    </code><br><br>

    * OpenSSL<br>
      OpenSSL은 네트워크를 통한 데이터 통신에 쓰이는 프로토콜인 TLS와 SSL의 오픈 소스 구현판이다.<br> 
      C 언어로 작성되어 있는 중심 라이브러리 안에는, 기본적인 암호화 기능 및 여러 유틸리티 함수들이 구현되어 있다.<br>
      https://ko.wikipedia.org/wiki/OpenSSL
    <br><br><br>
      
2.  ***OpenSSL/bin 폴더로 이동 후 인증서 설치에 필요한 파일 생성***<br><br>
    <code>
    openssl md5 * > rand.dat<br>
    openssl genrsa -des3 1024 > key.pem
    </code><br><br><br>
    
3.  ***CSR 파일 생성***<br>
    인증서 발급을 위한 신청 양식<br><br>
    <code>
    openssl req -new -key key.pem > csr.pem
    </code>
    * 입력하라고 나오는 각 질의에 맞게 입력<br>
    * "A Challenge password"는 enter로 넘어감<br><br><br>

4.  ***인증서 파일 생성***<br><br>
    <code>
    openssl req -key key.pem -x509 -nodes -sha1 -days 365 -in csr.pem -out crt.pem
    </code><br><br><br>
        
5.  ***PKCS12 포멧의 키 저장소 파일 생성(톰캣 저장용)***<br><br>
    <code>
    openssl pkcs12 -export -in crt.pem -inkey key.pem -out .keystore -name tomcat
    </code><br><br><br>
    
6.  ***실행시킬 톰캣에 적용***
    1. move tomcat home directory
    2. move conf directory
    3. edit "server.xml"
    4. "Connector port=8443" 부분 주석 해제
    5. 코드 삽입 <br>
       keystoreFile={위 5번에서 생성한 PKCS12 파일 위치}<br>
       keystorePass={passwd}<br>
       keystoreType="pkcs12"
    6. 톰캣 구동
