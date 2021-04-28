---
title: 우아한 캠프 프리코스 1주차 피드백
date: 2021-04-28 23:20:00 +0900
categories: [Tech, CodeConvention]
tags: [java, tech, codeconvention]
---

<span style="color: #aa66aa;">우아한 캠프 프리코스 1주차 피드백</span><br>
[참조 링크](https://github.com/joojimin/hackday-conventions-java)

-----

##  <span style="color: #aa88aa;">이름을 통해 의도를 드러내라</span>
*   변수 이름, 함수 이름, 클래스 이름을 짓는데 시간을 투자해라. <br>
    연속적인 숫자를 덧붙인 이름(a1,a2…)<br>
    불용어(info, Data, a, an, the)를 추가하는 방식은 적절하지 못하다.<br>
   
##  <span style="color: #aa88aa;">축약하지 마라</span>
*   의도를 드러낼 수 있다면 이름이 길어져도 괜찮다.<br>
   
##  <span style="color: #aa88aa;">IDE의 code format 기능을 활용해라</span>
*   Cmd+Alt+L ( intelliJ + MAC )<br>
   
##  <span style="color: #aa88aa;">space(공백)도 convention이다.</span>
*   for, while, if문 사이의 space도 convention이다.<br>
   
##  <span style="color: #aa88aa;">구현 순서도 convention이다.</span>
*   상수 또는 클래스 변수
*   인스턴스 변수 
*   생성자
*   메소드<br>
   
##  <span style="color: #aa88aa;">반복하지 마라.</span>
*   중복은 소프트웨어에서 모든 악의 근원이다.<br>
   
##  <span style="color: #aa88aa;">space와 tab 혼용</span>
*   들여쓰기에 space와 tab을 혼용하지 않는다.
*   둘 중에 하나만 사용한다.<br>
   
##  <span style="color: #aa88aa;">의미없는 주석을 달지 않는다.</span>
*   이름을 통해 의도를 드러내면 굳이 주석이 필요없다.<br>
   
##  <span style="color: #aa88aa;">값을 하드코딩 하지마라</span>
*   상수를 만들고 이름을 부여해 변수의 역할이 무엇인지 의도를 드러내라<br>
   
##  <span style="color: #aa88aa;">git commit 메시지를 의미있게 작성</span>
    
##  <span style="color: #aa88aa;">README.md 파일에 작성하는 기능 목록은 기능 구현을 하면서 변경될 수 있다.</span>
*   계속 업데이트해 살아있는 문서를 만들자.<br>
    
##  <span style="color: #aa88aa;">기능 목록 구현을 재검토</span>
*   클래스 설계, 구현, 함수 설계와 구현과 같이 너무 상세하게 작성하지 않는다.<br>
    (언제든 변경가능 하기때문에)
*   정상적인 경우도 중요하지만, 예외적인 상황도 기능 목록에 정리한다.
*   시작단계에서 모두 찾기 힘들기 때문에 기능을 구현하면서 계속해서 추가해 나간다.<br>
    
##  <span style="color: #aa88aa;">README.md를 상세히 작성</span>
*   마크다운 문법으로 어떠한 프로젝트이며, 어떤 기능을 담고 있는지 기술
