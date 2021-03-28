---
title: 백기선의 리액티브 프로그래밍 1강 정리
date: 2021-03-27 10:00:00 +0900
categories: [Study, Reactive]
tags: [study, reactive, java, youtube]
comments: true
---

***백기선님의 리액티브 프로그래밍 유튜브 강의를 보고 정리한 내용입니다***<br>
***1강은 튜토리얼 부분이라 키워드 위주로 정리했습니다***<br>
[\[리액터\] 리액티브 프로그래밍 1부 리액티브 프로그래밍 소개 - 백기선](https://www.youtube.com/watch?v=VeSHa_Xsd2U&list=PLfI752FpVCS9hh_FE8uDuRVgPPnAivZTY)

---

1.  **리액터3은 리액티브 스트림의 구현체이다.**<br>

2.  **JVM 기반의 리액티브 프로그래밍이다.**<br>

3.  **선언적인 코드로 비동기적인 파이프라인을 만들 수 있는 패러다임이다.**<br>

4.  **이벤트 기반의 모델이고, 데이터가 consumer한테 push되는 형태로 동작한다.**<br>
    데이터가 사용할 준비가 되어있으면 데이터를 소비할 소비자에게 전달한다.<br>
    
5.  **선언적인 코드란?**
    명령형 = 어떻게 할 것인지를 나타냄<br>
    선언형 = 무엇을 할 것인지를 나타냄<br>
    
6.  **Asynchronous and non-blocking이 핵심이다.**<br>
    low-level의 동기화 코드와 병렬성을 주기위한 코드를 고려하지 않고 작성할 수 있다.<br>
    ( Runnable, Thread등 다루기 어려운 코드들을 작성하지 않아도 된다. )<br><br>
    *   Asynchronus<br>
        비동기적으로 결과값을 받아서 처리하는 것 (콜백, 제공하는 입장)<br>
    *   non-blocking<br>
        어떤 작업때문에 하위의 작업들이 처리되지 못하는 경우가 없는 것(사용하는 입장)<br>
    *   [참고](https://joojimin.github.io/posts/DAILY_COMMENT-2020-12-21/)<br>
    
7.  **Callback 기반의 API와 Future기반의 코드 대체제이다.**<br>

8.  **기존 리액티브 스트림 호환 가능**<br>
    리액터3, RxJava, Akka 등등<br>
    Java9 도입 ( JVM 기반 )<br>
    
9.  **Publisher가 데이터를 제공하지만(퍼블리싱) Subscriber가 동록(구독)하기 전까지는 아무것도 하지 않는다.**<br>
    *   Publisher<br>
        데이터를 보내는 입장<br>
    *   Subscriber<br>
        데이터를 소비하는 입장<br>
    
10. **backpressure**<br>
    데이터를 소비하고 난 후, 소비하는 중에 Subscriber가 소비하는 데이터 관리를 위해 제공하는 피드백<br>
    
    * 무수히 많은 데이터가 publish되어 subscriber가 바빠지면, 처리되지 못하거나(쌓여만 있다), 유실될 위험이 증가한다.<br>
    결국 방식은 non-blocking으로 했지만, 결과는 non-blocking하지 않은 상태가 된다.<br><br>
    이때 feedback으로 데이터양을 조절하거나 후처리를 진행해달라고 요청할 수 있으며 이를 backpressure(압력조절)이라고 한다.<br>
      
11. **operators**<br>
    어떤 처리를 해야하는지... 데이터 하나하나에 어떤 처리를 할지 결정하는 체이닝 방식<br>
    체이닝을 등록할 때마다 새로운 중간 publisher가 생긴다.<br><br>
    
12. “Which of these types are defined in the Reactive Streams specification?”<br>
    1.  Publisher<br>
    2.  Subscriber<br><br>
    
13. “in order to create a Reactive Stream Publisher or Subscriber..”<br>
    1.  … its code must comply with the spec and pass the TCK<br>
        새로운 Publisher와 Subscriber API를 만들려면 TCK 스펙을 완벽히 만족해야한다.<br>
        
    2.  … i should favor using an existing library like Reactor<br>
        현존하는 리액터 라이브러리 사용을 권장한다. (굳이 새로만들지.. 말자...)<br><br>
        
14. 아래 코드를 보고 물음에 답하시오<br>
```java
Flux<String> flux = Flux.just("A");
flux.map(s -> "foo" + s);
flux.subscribe(System.out::println);
```
<br>
위 코드는 의도한바와 다르게 아무것도 출력되지 않는다. 이유가 뭘까?<br><br>

    11번 이슈에서 설명한 내용, 기존 publisher에 데이터 처리 파이프라인을 추가할 경우 sub publisher가 생긴다.<br>
    해당 파이프라인을 subscribe(구독)을 해줘야 의도한 대로 동작할 수 있다.<br>

    ```java
    Flux<String> flux = Flux.just("A");
    Flux<String> subFlux = flux.map(s -> "foo" + s);
    subFlux.subscribe(System.out::println);
    ```
    <br>
    혹은 그대로 체이닝 걸어서
    
    ```java 
    Flux<String> flux = Flux.just("A")
                        .map(s -> "foo" + s);
    flux.subscribe(System.out::println);
    ```
