---
title: Optional 바르게 쓰자.
date: 2020-12-12 22:10:00 +0900
categories: [Tech, Java]
tags: [java, tech, optional]
comments: true
---

```java
import java.util.Optional;

Opitonal.of(...);
Optional.ofNullable(...);
Optional.isPresent();
Optional.orElse(...);
Optional.orElseGet(...);
Optional.orElseThrow(...);
```


## 만들어진 의도
* 메서드가 반환할 결과값이 ‘없음’을 명백하게 표현할 필요가 있고, <br>
  단 null을 반환하면 에러를 유발할 가능성이 높은 상황이다.<br>
  그를 해결하고자 메서드의 반환 타입으로 Optional을 사용하자는 것이 주된 목적이다.<br><br>

## 사용시 주의사항
1. <code>isPresent()-get() 대신 orElse(), orElseGet(), orElseThrow()</code><br>
   이왕 비싼 Optional 쓰는김에 코드라도 줄이자!!<br>
   <br>
   ```java
   // Worst case
   if(Optional.isPresent()){
        return ...
   }else{
        return ...
   }
   ```
   ```java
   // Good case
   return Optional.orElse(...);
   ```
   <br>
2. <code>orElse(new Object..) 대신 orElseGet(()-> new Object…)</code><br>
   orElse method는 Optional에 값이 있든 없든 무조건 실행한다<br>
   따라서 새로운 객체를 만드는 연산을 수행해야하는 경우는 orElseGet method로 없을때만 사용하게 해야한다.<br>
   <br>
   ```java
   // Worst case
   Optional.orElse(new Object(...));
   ```
   ```java
   // Good case
   Optional.orElseGet(new Object(...));
   ```
   <br>
3. <code>단지 값을 얻을 목적이라면 Optional 대신 null 비교</code><br>
   Optional은 비싸다.<br>
   따라서 단순히 값 또는 null을 얻을 목적이라면 Optional 대신 null 비교를 쓰자.<br>
   <br>
   ```java
   // Worst case
   Optional.ofNullable(object).orElse(...);
   ```
   ```java
   // Good case
   object != null ? object : ... ;
   ```
   <br>
4. <code>컬렉션을 반환할땐 Optional 대신 비어있는 컬렉션 반환하자</code><br>
   컬렉션 반환은 null이 아니라 비어있는 컬렉션을 반환하는 것이 좋을 때가 많다.<br>
   따라서 컬렉션은 Optional로 감싸서 반환하지 말고 비어있는 컬렉션을 반환하자.<br>
   <br>
   ```java
   // Worst case
   return Optional.ofNullable( Collections );
   ```
   ```java
   // Good case
   return Collections != null ? Collections : Collections.emptyList();
   ```
   <br>
5. <code>Optional을 필드로 사용 금지</code><br>
   Optional은 필드에 사용할 목적으로 만들어지지 않았으며,Serializable을 구현하지 않았다.<br>
   따라서 Optional은 필드로 사용하지 말자.<br>
   <br>
6. <code>Optional을 생성자나 메서드 인자로 사용 금지</code><br>
   Optional을 생성자나 메서드 인자로 사용하면, 호출할 때마다 Optional을 생성해서 인자로 전달해 줘야한다.<br>
   굳이 비싼 Optional을 인자로 사용하지 말고 호출되는 쪽 null 체크 책임을 남겨두자 ( Optional은 비싸다.. )<br>
   <br>
7. <code>Optional을 컬렉션의 원소로 사용 금지</code><br>
   컬렉션에는 많은 원소가 들어갈 수 있다.<br>
   따라서 비싼 Optional을 원소로 사용하지 말고 원소를 꺼낼때나 사용할 때 null 체크하는 용도로 사용하는 것이 좋다.<br>
   <br>
8. <code>of(), ofNullable() 혼동주의</code><br>
   of(X)는 X가 null이 아님이 확실할 때만 사용해야 하며, X가 null이면 NullPointException<br>
   ofNullable(X)는 X가 null일 수도 있을때만 사용해야하며, null이 아님이 확실하면 of(X)를 써야한다.<br>
   <br>
9. <code>Optional&lt;T&gt; 대신 OptionalInt, OptionalLong, OptionalDouble을 쓰자</code><br>
   Optional에 담길 값이 int, long, double이라면 Boxing/Unboxing이 발생하는 Optional<T>를 사용하지말고<br>
   OptionalInt, OptionalLong, OptionalDouble을 사용하자<br>
   Boxing, UnBoxing은 성능에 영향을 미친다.<br><br>

## 추가로 공부해야할 내용
* Optional이 비싼 이유도 정리해야겠다. (Stream을 이용해서 인걸로 추측중..)<br>
<br>

## 참조 문헌
<ul>
  <li>
    <a href="http://homoefficio.github.io/2019/10/03/Java-Optional-%EB%B0%94%EB%A5%B4%EA%B2%8C-%EC%93%B0%EA%B8%B0/">
      Java Optional 바르게 쓰기<br>
      http://homoefficio.github.io
    </a>
  </li>
  <li>
    <a href="https://dzone.com/articles/using-optional-correctly-is-not-optional">
      26 Reasons Why Using Optional Correctly Is Not Optional<br>
      https://dzone.com/
    </a>
  </li>
</ul>
