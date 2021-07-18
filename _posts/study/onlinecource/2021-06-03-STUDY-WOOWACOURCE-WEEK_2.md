---
title: 우아한 테크 코스 프로, 2주차 JPA
date: 2021-06-03 09:00:00 +0900
categories: [Tech, Study]
tags: [java, tech, study, onlinecource, woowahan]
---

<span style="color: #aa66aa;">우아한 테크 코스 Pro, 2주차 과제 - JPA</span><br>
* [Step1 - 엔티티 매핑](https://github.com/joojimin/jwp-qna/tree/step1)
* [Step2 - 연관관계 매핑](https://github.com/joojimin/jwp-qna/tree/step2)
* [Step3 - 질문 삭제하기 리팩터링](https://github.com/joojimin/jwp-qna/tree/step3)

---

<code>코스에서 소개된 내용만 간단하게 포스팅하겠습니다. JPA 자세한 내용은 다른 탭에서!!</code>

## JPA 등장 배경
* 객체를 중심의 패러다임(객체 지향)과 테이블 중심의 패러다임은 차이가 있다.

> 객체 지향 패러다임
> * 시스템을 구성하는 객체들에게 적절한 책임을 할당하는 것
> * 상속
>   * 테이블은 상속 관계가 없다.
> * 연관 관계
>   * 객체의 연관관계에는 방향성이 있다.
>   * 테이블의 연관관계는 방향성이 없다.
>   * 객체는 자유롭게 객체 그래프를 탐색할 수 있어야 한다.

<br>

* SQL을 직접 다루게 되면 불편함이 생긴다.
  * 반복적인 작업 ( 새로운 컬럼 추가등의 행위 발생시 관련된 모든 SQL을 수정 )
  * 개발자들이 매핑된 엔티티를 신뢰할 수 없다. ( 런타임시, mapping되는 타이밍에 오류가 잡히므로 )

<br><br>

## JPA 사용시 유의사항
* 일대다 단반향 매핑의 단점
  * 매핑한 객체가 관리하는 외래 키가 다른 테이블에 있다.
  * 연관 관계 처리를 위한 UPDATE SQL을 추가로 실행해야 한다.
  * 일대다 단방향 매핑보다는 다대일 양방향 매핑을 권장한다.

<br>

* Auditing
  * 정해진 엔티티를 생성하거나 변경한 사람, 생성되거나 변경된 시점을 추적하기 위해 제공되는 기능
  * Spring Data JPA가 구현해놓은 <code>AuditingEntityListener</code>를 통해 동작한다.
    * @PrePersist, @PreUpdate가 붙은 메서드를 통해 엔티티가 영속화 되기전에 동작한다.
    * [Spring-data reference - Auditing](https://docs.spring.io/spring-data/jpa/docs/1.7.0.DATAJPA-580-SNAPSHOT/reference/html/auditing.html)
    * [참고 자료 - Auditing](https://gist.github.com/dlxotn216/94c34a2debf848396cf82a7f21a32abe)


<br>

* 연관관계 매핑시 주의사항
```java
@Test
void save() {
    Member member = new Member(1L, "jason"); // (1)

    Station sourceStation = stations.save(new Station("잠실역")); // (2)
    Station destinationStation = stations.save(new Station("몽촌토성역")); // (3)

    Favorite favorite = new Favorite(sourceStation, destinationStation); // (4)
    member.addFavorite(favorite);

    System.out.println("### before merge");
    Member savedMember = members.save(member); // (5)
    System.out.println("### after merge");

    System.out.println("### before transaction commit");
    members.flush(); // transaction commit (6)
    System.out.println("### after transaction commit");
}

```

* 위 코드의 문제점은?
  * <code>saveMember의 favorite에는 아무것도 저장되지 않는다.</code>
  * 영속성 컨텍스트에 member에 추가된 Favoirte이 없으니 member가 영속화될때 저장되지 않는다.
  * 엔티티의 식별자가 null이 아닌 경우 persist()가 아닌 merge()가 동작하며 이때 전달 인자인 entity가 아닌 새로운 인스턴스가 반환된다.

<br>

* 해결책
  * 식별자가 존재하는 엔티티(member)인 경우 먼저 영속(managed) 상태로 만든 후 비즈니스 로직을 수행한다.
  * favorite를 영속(managed) 상태로 만든다.
  * CascadeType.MERGE를 사용한다.

<br><br>

## 미션 진행 회고
* JPA 공부를 좀 더 해야겠다! (인프런 강의 다 듣자!)

<br><br>

## 피드백
* OneToMany 기본 fetch는 LAZY
* ManyToOne 기본 fetch는 EAGAR

