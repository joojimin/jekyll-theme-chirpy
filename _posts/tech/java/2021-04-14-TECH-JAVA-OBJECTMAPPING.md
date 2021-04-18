---
title: Object Mapping 어디까지 해봤니?
date: 2021-04-14 23:20:00 +0900
categories: [Tech, Java]
tags: [java, tech, objectmapping, mapstruct]
---

<span style="color: #aa66aa;">Object Mapping 어디까지 해봤니?</span><br>
[참조 링크](https://meetup.toast.com/posts/213)

-----

##  <span style="color: #aa88aa;">Object Mapping 라이브러리인 MapStruct
*   API 버전 별 객체, 비즈니스 로직, 레이어간 객체와 객체간 매핑시 사용한다.
    
##  <span style="color: #aa88aa;">등장 배경</span>
*   Spring Framework 개발 환경을 예로, 각 레이어(Controller, Service, Repository 등)에서<br>
    데이터를 주고 받거나, 비즈니스 로직에서 정의된 객체 타입을 다른 타입으로 변환하는 일이 빈번하게 일어난다.<br>
    <br>
    
##  <span style="color: #aa88aa;">문제점</span>
*   소개된 배경으로 인하여, 그동안 개발자가 코드를 작성할때는 다음과 같은 문제가 생겼다.<br>

    1.  반복적이고, 코드 중복이 발생<br>
        lombok의 @Builder를 이용하여 코드량을 줄일 순 있지만, 이마저도 반복적이고 코드 중복이 쉽게 발생한다.<br>

    2.  실수하기 쉽다.<br>
        
    3.  코드 생산성을 떨어뜨린다.<br>

    4.  비즈니스 로직에 섞여, 코드가 복잡해지고 소개된 모든 이유를 통틀어서 결국 유지보수가 힘들어진다.<br>
    <br>
        
##  <span style="color: #aa88aa;">해결 방법: MapStruct</span>
*   Java 개발 환경에서 객체 간 매핑에 대해 코드를 자동으로 생성해주는 매핑 라이브러리<br>
    Annotation Processor를 사용해 컴파일시 매핑 코드를 생성한다.<br>
    <br>
    
##  <span style="color: #aa88aa;">MapStruct의 장점</span>
1.  컴파일시 설정된 방식으로 오류를 확인할 수 있다. (코드 생성시)
2.  리플렉션을 사용하지 않기 때문에 매핑 속도가 빠르다.
3.  디버깅이 쉽다.
4.  생성된 매핑 코드를 눈으로 직접 확인할 수 있다.
    <br>
    
##  <span style="color: #aa88aa;">사용법</span>
1.  기본적으로 같은 이름, 같은 Type의 속성은 자동으로 매핑된다.
2.  다른 이름의 속성을 매핑하기 위해서는 @Mapping 어노테이션을 이용, source와 target을 지정하여 매핑한다.
3.  여러 개의 객체를 하나로 합치는 작업도 가능
4.  @Mapping 어노테이션의 ignore 기능으로 속성을 무시할 수도 있다.
5.  MapperConfig를 통해 속성을 지정할 수 있다.
    <br>
    
##  <span style="color: #aa88aa;">정책</span>
1.  **unmappedSourcePolicy** <br>
    IGNORE, WARN, ERROR<br>
    매핑시 Soruce.aFiled가 사용되지 않는다면 컴파일 오류<br>
    ERROR로 설정시 매핑되지 않았다면 컴파일 오류가 발생<br>
    
2.  **unmappedTargetPolicy** <br>
    IGNORE, WARN, ERROR<br>
    매핑시 Target.aFiled가 사용되지 않는다면 컴파일 오류<br>

3.  **typeConversionPolicy** <br>
    IGNORE, WARN, ERROR<br>
    타입 변환시 유실이 발생할 수 있을 때 정책<br>
    long -> int로 값을 넘길때 유실이 발생, 이런 경우의 정책을 설정할 수 있다.<br>
        
##  <span style="color: #aa88aa;">전략</span>
1.  **nullValueMappingStrategy** <br>
    RETURN_NULL(default 설정)<br>
    RETURN_DEFAULT<br>
    Source가 null일 때 정책이다.<br>
    
2.  **nullValuePropertyMappingStrategy** <br>
    SET_TO_NULL(default)<br>
    SET_TO_DEFAULT<br>
    IGNORE<br>
    Source의 필드가 null일때 정책
