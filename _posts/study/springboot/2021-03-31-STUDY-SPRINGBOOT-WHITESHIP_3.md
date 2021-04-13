---
title: 백기선님의 스프링 부트 2.0 Day 3. 스프링 부트 스타터
date: 2021-03-31 23:58:00 +0900
categories: [Study, Springboot]
tags: [study, springboot, java, youtube]
comments: true
---

***백기선님의 스프링 부트 2.0 유튜브 강의를 보고 정리한 내용입니다***<br>
[스프링 부트 2.0 Day 3. 스프링 부트 스타터 - 백기선](https://www.youtube.com/watch?v=PicKx3lDGLk&list=PLfI752FpVCS8tDT1QEYwcXmkKDz-_6nm3&index=3)
<br>
<br>
해당 영상은 spring-boot 공식 reference를 보며 학습하는 내용입니다.<br>

---------------------------------------

## Sprin-boot-starter 

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-thymeleaf</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-devtools</artifactId>
    </dependency>
</dependencies>
```

1.  **Spring-boot-starter-** 로 시작하는 스타터 의존성들은 SpringBoot를 더 편리하게 만들어 놓은,<br> 
    의존성 집합이다.<br>
    <br>

2.  해당 의존성 집합들은 다른 스타터 의존성들, 기본 Spring-boot-stater-parent와 충돌나지 않게 잘 설정해준다.<br>
    <br>

3.  AutoConfigure module<br>
    라이브러리를 시작할때 필요한 모든 것들을 담고 있는 모듈<br>
    <br>

    @ConfigurationProperties<br>
    정의된 preperties를 Object에 바인딩 받을 수 있다.<br>
    <br>

4.  Technical staters<br>
    기본 default로 설정되는 의존성들을 바꿔낄 수 있는 스타터 집합<br>
    
    *   spring-boot-stater-jetty<br>
        (default: tomcat)<br><br>
    *   spring-boot-stater-log4j2<br>
        (default: logback)<br><br>
    *   spring-boot-stater-reactor-netty<br>
    <br>

5.  Springboot는 코드 구조를 강요하지 않지만, default 패키지를 권장하지 않습니다.<br>
    * default package: 클래스패스 밑에 어떠한 package도 없이 정의되는 class<br>
    <br>

    * @ComponentScan, @EntityScan, @SpringBootApplication등 package 기반으로 스캔하는 동작들의<br>
    불필요한 scan 작업을 줄일 수 있다.<br>
    <br>

6.  @SpringBootApplication이 붙은 main class는 root package 바로 밑에 두는 것을 권장<br>
    그래야 root package 하위의 모든 클래스들을 스캔한다.<br>
    <br>

7.  SpringBoot는 java 기반의 설정(Configuration)을 선호한다.<br>
    기존 Spring처럼 xml 파일 기반의 설정을 사용할 수도 있으나 두 가지 방식중 반드시 한가지를 메인방식으로 정의해야한다.<br>
    <br>

8.  @Configuration 클래스를 하나만 쓸 필요는 없다.<br>
    @Import를 통해 @Configuration이 정의된 클래스에 다른 설정을 끌고 들어올 수 있으며,<br>
    @ComponentScan, 나아가 @SpringBootApplication을 통해 하위 패키지를 스캔하며 설정파일을 로드할 수 있다.<br>
