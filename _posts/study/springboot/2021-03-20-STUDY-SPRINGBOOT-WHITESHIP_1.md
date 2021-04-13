---
title: 백기선님의 스프링 부트 2.0 Day 1. 스프링 부트 시작하기 정리
date: 2021-03-20 21:12:00 +0900
categories: [Study, Springboot]
tags: [study, springboot, java, youtube]
comments: true
---

***백기선님의 스프링 부트 2.0 유튜브 강의를 보고 정리한 내용입니다***<br>
[스프링 부트 2.0 Day 1. 스프링 부트 시작하기 - 백기선](https://www.youtube.com/watch?v=CnmTCMRTbxo&list=PLfI752FpVCS8tDT1QEYwcXmkKDz-_6nm3&index=1)
<br>
<br>
해당 영상은 spring-boot 공식 reference를 보며 학습하는 내용입니다. 

---

### SpringBoot의 정의
1.  독립적이고, 실제 제품 수준의 Spring 기반 application을 쉽게 만들 수 있게 도와주는 framework<br>
    <br>
2.  java -jar를 통해 쉽게 application을 시작 할 수 있다.<br>
    <br>
3.  기존의 Spring 프로젝트는 기본 구축(Web 설정 등등)을 위해 많은 어려움과 시간을 쏟아야했다.<br>
    이를 쉽게 해주기 위해 SpringBoot가 등장<br>
    <br>
4.  요구 사항이 다양해도, 요구 사항에 따라 다양하고 유연하게 Custom할 수 있다.<br>
<br><br>

### SpringBoot 2.0 스펙
* SpringBoot 2.0.0.RC2
* Java8 or higher
* Spring Framework 5.0.4.RELEASE
* Tomcat 8.5 (Servlet version 3.1)
* Jetty 9.4 (Servlet version 3.1)
* Apache Maven 3.2
* etc...<br>
<br><br>

### Maven 의존성 설정으로 시작하기
1.  Maven, pom.xml으로 Springboot parent 설정과 상속 관계를 만들 수 있다.<br> 
    <parent> 태그를 통해 spring-boot-starter-parent안에 정의된 아티팩트 정보를 상속받을 수 있다.<br>
    * 의존성은 Override를 통해 변경 가능<br>
    
    ```xml
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>{spring-boot.version}</version>
        <relativePath/>
    </parent>
    ```

    <br>
2.  spring-boot-starter-parent를 이용하는 이유는 의존성 관계를 쉽게 풀어내기 위해서<br>
    미리 필요한 정보들을 부모 아티팩트 정보에 정의해두고, 자식 어플리케이션에서는 상속만 받아서 실행 가능<br>
    * 단 maven 상속 관계는 단 하나만 가능하기 때문에 기존에 상속 관계가 존재하면 <dependencyManager> 태그를 이용해<br>
      spring-boot-dependencies 관계를 설정해 사용할 수 있다.<br>
    <br>
3.  어플리케이션 구성에 필요한 spring-boot-starter**들을 지원한다.<br>
    (web, jpa, redis 등등)<br>
    <br>

### Main Class
*   Executable JAR 파일로 packaging하여 시작할 경우, java의 main 클래스처럼 @SpringBootApplication
    어노테이션이 붙은 클래스의 main method를 시작한다.<br>
*   해당 method를 통해 commandLine에서 넘어온 Arguments를 SpringBootApplication에서 사용가능하다.<br>
    <br>
    
### @EnableAutoConfiguration
*   SpringBoot가 제공해주는 어노테이션<br>
*   SpringBoot에게 사용자가 어떤 설정을 원하는지 알려주는 역할<br>
    ( 기본적으로 SpringBoot가 제공해주는 설정을 사용하라는 어노테이션 )<br>
*   어떤 의존성이 ClassPath내에 존재하느냐에 따라 동작 방식 결정<br>
*   dependency로 어떤 starter를 설정해줬느냐에 따라 Auto로 설정해준다. <br>
