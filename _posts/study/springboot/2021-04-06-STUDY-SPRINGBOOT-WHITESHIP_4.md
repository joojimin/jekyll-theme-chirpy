---
title: 백기선님의 스프링 부트 2.0 Day 4. @SpringBootApplication과 XML 빈 설정 파일 사용하기
date: 2021-04-06 12:49:00 +0900
categories: [Study, Springboot]
tags: [study, springboot, java, youtube]
comments: true
---

***백기선님의 스프링 부트 2.0 유튜브 강의를 보고 정리한 내용입니다***<br>
[스프링 부트 2.0 Day 4. @SpringBootApplication과 XML 빈 설정 파일 사용하기](https://www.youtube.com/watch?v=PicKx3lDGLk&list=PLfI752FpVCS8tDT1QEYwcXmkKDz-_6nm3&index=4)
<br>
<br>
해당 영상은 spring-boot 공식 reference를 보며 학습하는 내용입니다.<br>

---------------------------------------


1.  Configuration, bean 등록시 다른 형식(java 기반, XML 파일, Yaml, Yml 파일 등등)<br>
    을 혼합해서 쓰더라도 반드시 하나의 형식은 메인이 되어야한다.<br>
    <br>

2.  @ImportResource<br>
    xml 기반 설정을 import할 수 있는 어노테이션 ( value의 path는 ClassPath 기준 )<br>
    <br>

3.  Auto-Configuration<br>
    SpringBoot의 auto-configuration 동작은 사용자가 정의한 jar dependency 기준으로<br>
    자동으로 설정한다.<br>
    <br>
    @SpringBootApplication 안에는<br> 
    @EnableAutoConfiguration<br>
    @Configuration이 붙어있어 auto-configuration 동작을 실행한다.<br>
    <br>

4.  Auto-configuration이 설정된 부분에서 custom configuration을 추가하게되면<br>
    기존에 default로 설정됐던 부분은 disable되고 정의된 custom configuration이 설정된다.<br>
    <br>

5.  --debug 옵션을 킨 상태로 application을 실행시키면 어떤 auto-config가 설정되는지 log를 통해 볼 수 있다.<br>
    *   ConditionEvaluationReportLoggingListener<br>
    <br>

6.  특정 config를 disable하려면<br>
    @SpringBootApplication의 exclude method 혹은<br>
    @EnableAutoConfiguration의 exclude method를 사용 혹은<br>
    spring.autoconfigure.exclude 설정을 통해 할 수 있다.<br>
    <br>

7.  Spring boot bean 정의는 기존 spring에서 지원하는 모든 bean 등록 방식이 지원된다.<br> 
    1.  ComponentScan을 통한 어노테이션 스캔<br>
        @Component, @Service, @Repository, @Controller class<br>
        <br>
    2.  @Bean 메서드를 통한 등록<br>
        <br>

8.  Executable JAR( Embedded HTTP Server ) 사용을 통해<br>
    다른 사람과 같은 서버를 구동시킬 수 있으며( 외장 서버를 사용할 경우 외장 서버의 설정도 맞춰야한다. )<br>
    디버깅하기도 간편하다.<br>



