---
title: 백기선님의 스프링 부트 2.0 Day 2. Executable JAR 어떻게 만들고 어떻게 동작하는가
date: 2021-03-30 22:53:00 +0900
categories: [Study, Springboot]
tags: [study, springboot, java, youtube]
comments: true
---

***백기선님의 스프링 부트 2.0 유튜브 강의를 보고 정리한 내용입니다***<br>
[스프링 부트 2.0 Day 2. Executable JAR 어떻게 만들고 어떻게 동작하는가 - 백기선](https://www.youtube.com/watch?v=PicKx3lDGLk&list=PLfI752FpVCS8tDT1QEYwcXmkKDz-_6nm3&index=2)
<br>
<br>
해당 영상은 spring-boot 공식 reference를 보며 학습하는 내용입니다.

-----

### Creating on Executable Jar
*   실행 가능한 jar 파일 만들기
*   fat JAR<br>
    jar 파일안에 여러 jar파일들이 들어있고, 실행 가능한 의존성 관련 컴파일된 클래스들이 packaging 되어있다.<br>
    <br>
    
### Springboot의 fat Jar 만들기
*   Springboot ClassLoader module에는 실행 가능한 jar 파일이나 war 파일을 지원해주는 기능이 들어있다.<br>
    maven이나 gradle plugin을 이용하면 자동으로 생성 시켜준다.
    <br>
    
### Nested Jar 파일
*   Jar파일 안에 여러 jar 파일들이 packaging 되어 있는 경우 java(JVM)만으로는 읽어낼 방법이 없다.<br>
*   Springboot에서는 org.springframework.boot.loader.jar.JarFile, 자체 loader를 통해<br>
    Nested Jar 파일들을 읽어온다.<br>
*   처음 로딩될때 Fat Jar 파일의 각 클래스를 물리적인 주소로 나눠서 offset을 기록해두고,<br>
    load가 될때 해당 주소의 컴파일된 클래스를 불러온다.<br>
    <br>
    
### Launching Executable Jar file
*   org.springframework.boot.loader.Launcher( Jar or War )<br>
    Executable Jar 파일을 실행시키는 main class<br>
*   @SpringbootApplication 어노테이션이 붙은 클래스를 찾아 main method를 실행시킨다.<br>
    <br>
    
### Build System
1.  dependency, 의존성 관리를 지원하는 Build System을 사용하길 강력히 권장한다고 한다.<br>
2.  Maven 중앙 저장소에 공개된 아티팩트(jar파일)를 가져와 사용할 수 있는 시스템,<br>
    Maven, Gradle중 하나를 선택해서 사용하길 권장한다.<br>
    * 그외의 시스템도 사용 가능하나, 특별히 지원하진 않는다. ( 권장하지 않음 )<br>
    <br>

### Dependency Management
*   SpringBoot가 관리하는 의존성 목록을 지원한다.<br>
    parent version은 명시해야하나, 이외의 version은 custom을 할 경우가 아니면 명시할 필요가 없다.<br>
    <br>
    
### spring-boot-starter-parent
*   Maven 시스템을 사용하는 어플리케이션은, spring-boot-starter-parent을 상속받아서 사용할 수 있는데<br>
    센스있는 default값들을 사용할 수 있다.<br>
*   Java version, encoding, dependencyManaging, resource filtering, plugin, profile등을 설정해주며,<br>
    필요하면 해당 설정을 override해서 custom할 수 있다.<br>
    <br>
    
### 부가 설명
*   Springboot는 slf4j Facade를 앞에 두고 logback, log4j, log4j2등을 사용한다.<br>  
    그러나 다른 ClassLoader를 사용하는 java.util.Logging(시스템 클래스 로더)을 쓰면 안된다.<br>
    <br>
    
*   스냅샷, M 버전, RC 버전의 차이<br>
    1.  스냅샷:    데일리 빌드 수준 ( 개발 버전 )<br>
    2.  M 버전:   적당한 개발 버전 (마일스톤 버전)<br>
        *   스냅샷과 M 버전에 추가된 Class나 interface는 바뀔 가능성이 있다.<br>
    3.  RC 버전:  마일스톤 버전을 한번 더 정리한 버전 ( Release Candidate )<br>
    4.  GA 버전:  메이븐 저장소에 올라가는 최종 릴리즈 버전<br>
    <br>

*   resource filtering( spring-boot-starter-parent )<br>
    ClassPath내 yml, yaml, properties 파일들을 자동으로 읽는다.<br>
    ```xml
    <resources>
      <resource>
        <directory>${basedir}/src/main/resources</directory>
        <filtering>true</filtering>
        <includes>
          <include>**/application*.yml</include>
          <include>**/application*.yaml</include>
          <include>**/application*.properties</include>
        </includes>
      </resource>
      <resource>
        <directory>${basedir}/src/main/resources</directory>
        <excludes>
          <exclude>**/application*.yml</exclude>
          <exclude>**/application*.yaml</exclude>
          <exclude>**/application*.properties</exclude>
        </excludes>
      </resource>
    </resources>
    ```


