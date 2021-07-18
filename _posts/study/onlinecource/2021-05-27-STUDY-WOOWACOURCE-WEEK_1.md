---
title: 우아한 테크 코스 프로, 1주차 로또 TDD 회고
date: 2021-05-27 09:00:00 +0900
categories: [Tech, Study]
tags: [java, tech, study, onlinecource, woowahan]
---

<span style="color: #aa66aa;">우아한 테크 코스 Pro, 1주차 과제 - 로또 TDD</span><br>
* [Step1 - 학습 테스트 실습](https://github.com/joojimin/java-lotto/tree/step1)
* [Step2 - 문자열 덧셈 계산기](https://github.com/joojimin/java-lotto/tree/step2)
* [Step3 - 로또(자동)](https://github.com/joojimin/java-lotto/tree/step3)
* [Step4 - 로또(2등)](https://github.com/joojimin/java-lotto/tree/step4)
* [Step5 - 로또(수동)](https://github.com/joojimin/java-lotto/tree/step5)

---

## TDD란?
* TDD: TFD(Test First Development) + 리팩토링
* 프로그래밍 의사 결정과 피드백 사이의 간극을 의식하고 이를 제어하는 기술 <br>
  ( 테스트 기술이 아니다. 설계 기술이며, 분석 기술이다. )

<br><br>

## 도입 배경
* 디버깅 시간을 줄여준다.
* 동작하는 문서 역할을 한다.
* 리팩토링에 대한 두려움을 없애준다. <br>
  ( 개인적으로 가장 큰 장점이 아닐까 싶음.. )

<br><br>

## 구현 싸이클
1. **실패하는 테스트를 먼저 구현한다.**
    * 실패하는 단위 테스트를 작성할 때까지 프로덕션 코드(production code)를 작성하지 않는다.
    * 컴파일은 실패하지 않으면서 실행이 실패하는 정도로만 단위 테스트를 작성한다.
2. **테스트가 성공하도록 프로덕션 코드를 작성한다.**
    * 현재 실패하는 테스트를 통과할 정도로만 실제 코드를 작성한다.
3. **테스트 코드와 프로덕션 코드를 리팩토링한다.**

<br><br>

## 미션 진행 회고
* **가장 중요한 건 테스트가 쉬운 코드가 작성되는게 아닐까 싶다.**
  * Service Layer에 있는 기존의 로직들은 테스트하기 어렵다. <br>
    ( 비즈니스 로직과 각종 인프라 스트럭처 로직등이 뒤섞여 있음 )
  * 따라서 비즈니스 로직이 Domain에 위치하는 것이 좋다.
* 테스트 불가능한 영역과 가능한 영역 파악
  * Random, shuffle, 날짜, 콘솔 입력 등은 테스트 불가능한 영역 <br>
    ( 비즈니스 로직에서 분리가 되어야한다. )
* 원시값(primitive)과 컬렉션(일급 컬렉션) Wrapping 하자!!
  * 불필요하게 오픈되는 메서드를 방지할 수 있으며, Wrapping된 클래스 내부에 응집도가 높은 비즈니스 로직을 넣을 수 있다.
  * [일급 컬렉션을 사용하는 이유](https://woowacourse.github.io/tecoble/post/2020-05-08-First-Class-Collection/)
  * [일급 컬렉션 소개와 써야할 이유](https://jojoldu.tistory.com/412)

## 피드백
* 동료 개발자들과 컨벤션을 맞춰 가독성 및 코드 이해도를 높이자<br>
  https://naver.github.io/hackday-conventions-java/
* NPE를 유발하는 코드를 지양하자.
  * NULL을 바로 리턴 ( Default value 혹은 Optional을 활용하자 )
* 매직 넘버, 매직 스트링을 그 자체로 쓰는 것은 의미를 알아보기 힘들다. <br>
  * 상수화(final static), Enum을 통한 의미 부여를 하자 <br>
    ( 1을 그대로 쓰기보다, MIN이라는 네이밍을 주는 것 자체로 명확해진다. )
