---
title: Google Convention을 적용해보자
date: 2021-07-06 21:40:00 +0900
categories: [Tech, CodeConvention]
tags: [java, tech, convention]
---

## 도입 배경
1. 동일한 코드 스타일을 지원
2. Github에서 코드가 이쁘게(?) 나온다 (PR시 편리함)

## google code style guide ( intellJ 기준 )

* [https://google.github.io/styleguide/javaguide.html](https://google.github.io/styleguide/javaguide.html)
* xml 다운로드(아래 링크에서 다운)<br>
  [https://github.com/google/styleguide/blob/gh-pages/intellij-java-google-style.xml](https://github.com/google/styleguide/blob/gh-pages/intellij-java-google-style.xml)

## intelliJ 설정

### Preferences -> Code Style

![20210706TechJavaCodeStyle02.png](/img/20210706TechJavaCodeStyle02.png)

<br>
### 톱니바퀴 -> import scheme -> intelliJ IDEA code style xml

![20210706TechJavaCodeStyle03.png](/img/20210706TechJavaCodeStyle03.png)

![20210706TechJavaCodeStyle04.png](/img/20210706TechJavaCodeStyle04.png)

<br>
### 다운받은 xml 파일 import

## 추가 설정

### tab 설정

* IDEA 마다 tab 설정이 다르기 때문에 github이나 이클립스 java 파일을 불러오면 난리남.. 보편적으로 쓰이는 java tab size를 적용하여 이를 방지
* **Preferences -> Code Style -> Java**
  * Tab size: 4
  * indent: 4
  * Continuation indent 8

![20210706TechJavaCodeStyle05.png](/img/20210706TechJavaCodeStyle01.png)

## PS

### 마법의 자동 줄 맞춤: Option + Command + L

### 컨벤션으로 빼고 싶은거나 더 맞췄으면 싶은 것들 얘기해주세요\~
