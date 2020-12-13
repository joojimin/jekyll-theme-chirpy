---
title: SpringBoot Test
date: 2020-12-13 17:45:00 +0900
categories: [Tech, Java]
tags: [java, tech, spring, springboot, junit, test]
---

## 표현방식
**Given-When-Then**<br>
준비-실행-검증의 부분으로 나눠진 테스트 코드로 표현한다.<br>
<br>

## <code>@SpringBootTest</code>
1. **정의**<br>
   통합 테스트를 제공하는 기본적인 스프링부트 테스트 어노테이션<br>
   <br>
2. **의존성**
    * JUnit
    * Spring & SpringBoot test
    * AssertJ
    * Hamcrest
    * Mockito( Java Mocking framework )
    * JSONassert
    * JsonPath<br>
  <br>
3. **Values**
    * properties<br>
      테스트시 property를 주입할 수 있다. ( key = value 방식으로 )<br>
      <br>
    * classes<br>
      어플리케이션 컨텍스트에 로드할 클래스를 지정한다.<br>
      따로 지정하지 않으면 @SpringBootConfiguration을 찾아 로드한다.<br>
      <br>
    * webEnviroment<br>
      어플리케이션이 실행될때의 웹환경을 설정할 수 있다.<br>
      <br>

## <code>@RunWith</code>
JUnit에 내장된 러너를 사용하는 대신 어노테이션에 정의된 러너 클래스를 사용<br>
@SpringBootTest 어노테이션을 사용하려면
JUnit의 SpringJUnit4ClassRunner 클래스를 상속받는 @RunWith(SpringRunner.class)를 꼭 붙여야한다.<br>
<br>

## <code>@ActiveProfile("")</code>
프로파일 환경을 갖는다면, 해당 어노테이션 Value에 원하는 프로파일 환경값을 부여 가능하다.<br>
<br>

## <code>@WebMvcTest</code>
  * MVC를 위한 테스트, 웹에서 테스트하기 힘든 컨트롤러를 테스트하는데 적합하다.
  * 시큐리티 혹은 필터까지 자동으로 테스트하며 수동으로 추가/삭제 가능<br>
  <br>

## <code>@DataJpaTest</code>
  * JPA 관련된 설정만 로드
  * 인메모리 데이터베이스를 이용<br>
  <br>

## <code>@RestClientTest</code>
  * REST 관련 테스트를 도와주는 어노테이션
  * REST 통신의 JSON 형식이 예상대로 응답을 반환하는지 등을 테스트<br>
  <br>

## <code>@JsonTest</code>
JSON의 직렬화, 역직렬화를 수행하는 Json, Jackson의 테스트 제공<br>
<br>

## <code>통합 테스트 환경 제공하기</code>
```java
@RunWith
@SpringBootTest
@AutoConfigureMockMvc
@ActiveProfiles
@Transactional // Test환경의 트랜잭션은 기본적으로 롤백
@Ignore // 자식클래스에서 상속시켜 동작시킬것이므로 Ignore
class IntegrationTest{
    ...
}
```
<br>

## 추가 내용
  * 이번 포스트 내용은 사용법에 관한 것이 였지만, 테스트를 잘하기 위해서는 TDD 개발이론을 습득 해야 할 것 같다.
  * 테스트를 잘하기 위해서는 클래스, 메서드등 기본 단위들이 각자의 관심사에 맞게 잘 나눠져 있어야 한다.<br>
    **단일 책임 원칙**
  * 테스트하기 쉬운 코드가 잘짜여진 코드이다. ( 유지보수에 용이하다 )

