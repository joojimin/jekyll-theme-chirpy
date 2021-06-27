---
title: Transactional
date: 2021-06-27 20:00:00 +0900
categories: [Tech, Spring]
tags: [java, tech, springboot, transactional]
---


##  <span style="color: #aa88aa;">[Spring] @Transactional</span>

### 트랜잭션이란?
* 2개 이상의 쿼리를 하나의 커넥션으로 묶어 DB에 전송하고, <br>
  이 과정에서 에러가 발생할 경우 자동으로 모든 과정을 원래대로 되돌려 놓는다.
* 하나 이상의 쿼리를 처리할 때 동일한 Connection 객체를 공유하도록 한다.

<br><br>

### 트랜잭션의 성질
1. 원자성
    * 한 트랜잭션 내에서 실행한 작업들은 하나로 간주한다. 모두성공, 모두실패
2. 일관성
    * 일관성 있는 데이터베이스 상태를 유지한다.
3. 격리성
    * 동시에 실행되는 트랜잭션끼리는 서로 영향이 없어야한다.
4. 지속성
    * 트랜잭션을 성공적으로 마치면, 결과가 항상 저장되어야한다.

<br><br>

### Spring에서 트랜잭션 처리 방법
* @Transactional을 선언하여 사용하는 방법이 일반적이며, 선언적 트랜잭션이라고 부른다. (@EnableTransactionManagement가 선언되어있어야한다 )
* 클래스, 메서드에 해당 어노테이션을 선언시, 해당 클래스는 트랜잭션 기능이 추가된 프록시 객체가 생성된다.
* PlatformTransactionManager를 사용하여 트랜잭션을 시작하고 정상 여부에 따라 commit 혹은 rollback 한다.

<br><br>

### 다수의 트랜잭션이 경쟁시 발생하는 문제
1. Dirty Read
    * 트랜잭션 A가 어떤 값을 1에서 2로 변경, 트랜잭션 B가 같은 값을 읽는 경우 2로 읽힘
    * 하지만 A가 롤백된다면 B는 잘못된 값을 읽은게 됨.. (데이터 불일치 발생)

<br>    

2. Non-Repeatable Read
    * 한 트랜잭션안에서 다수의 같은 쿼리에 대해 다른 결과값이 나올 수 있다.
    * 중간에 다른 트랜잭션이 값을 바꾸는 경우

<br>    

3. Phantom Read
    * 한 트랜잭션에서 일정 범위의 레코드를 두번 이상 읽을 때 발생하는 데이터 불일치

<br><br>

### 스프링 트랜잭션 속성
1. isolation 격리 수준
    1. <span style="color: #aa5555;">default</span>
        * 기본 격리 수준(DB의 isolation 레벨을 따름)
        
    2. <span style="color: #aa5555;">READ_UNCOMMITTED(level 0)</span>
        * 커밋되지 않은(트랜잭션 처리중인) 데이터에 대한 읽기를 허용(Dirty read) -> 잘 쓰지 않음
       
    3. <span style="color: #aa5555;">READ_COMMITTED(level 1)</span>
        * 트랜잭션이 커밋된 확정 데이터만 읽기 허용 -> Dirty read 방지
       
    4. <span style="color: #aa5555;">REPEATABLE_READ(level 2)</span>
        * 트랜잭션이 완료될 때까지 SELECT 문장이 사용하는 모든 데이터에 shared lock
        * 다른 사용자는 그 영역에 해당되는 데이터에 대한 수정이 불가능 -> Non-Repeatable Read 방지 ( 두 번 쿼리 했을때 일관성 있는 결과를 리턴 )
       
    5. <span style="color: #aa5555;">SERIALIZABLE(level 3)</span>
        * 데이터의 일관성 및 동시성을 위해 MVCC를 사용하지 않음
        * 트랜잭션이 완료될때까지 SELECT 문장이 사용하는 모든 데이터에 shared lock이 걸리므로, 
        * 그 영역에 해당되는 데이터에 대한 수정, 입력이 불가능 -> phantom Read 방지
       
    6. 격리 수준이 올라갈 수록 성능이 저하 될 수 있다.

<br>

2. propagation, 전파옵션
    * 트랜잭션 동작 도중 다른 트랜잭션을 호출하는 상황에 선택할 수 있는 옵션이다.
    
     1. <span style="color: #aa5555;">REQUIRED(default)</span>
        * 부모 트랜잭션 내에서 실행하며, 부모가 없는 경우 새로운 트랜잭션 생성
         
     2. <span style="color: #aa5555;">SUPPORTS</span>
        * 이미 시작된 트랜잭션이 있으면 참여, 없으면 트랜잭션 없이 진행
       
     3. <span style="color: #aa5555;">REQUIRES_NEW</span>
        * 부모 트랜잭션을 무시하고 무조건 새로운 트랜잭션이 생성
       
     4. <span style="color: #aa5555;">MANDATORY<span>
        * 이미 시작된 트랜잭션이 있으면 참여, 없으면 예외발생 (독립적으로 실행되면 안될때 사용)
       
     5. <span style="color: #aa5555;">NOT_SUPPORTED</span>
        * 트랜잭션 사용안함 ( 이미 진행중인 트랜잭션은 보류시킨다 )
       
     6. <span style="color: #aa5555;">NEVER</span>
        * 트랜잭션 사용안함 ( 이미 진행중인 트랜잭션이 있는 경우 예외 발생 )
       
     7. <span style="color: #aa5555;">NESTED</span>
        * 이미 트랜잭션이 있으면, 중첩 트랜잭션을 시작
        * 부모(이미 시작된 트랜잭션)의 커밋과 롤백에 영향을 받지만, 자신의 커밋과 롤백은 
        * 부모에게 영향을 주지 않는다.( 로그 저장같은 작업이 해당 )

<br>

3. readOnly 속성
    * 트랜잭션을 읽기 전용으로 설정할 수 있다,
    * 성능 최적화를 위해 특정 트랜잭션 작업안에서 쓰기 작업이 일어나는 것을 방지
    * 읽기 전용 트랜잭션이 실행된 후에 수정이 발생하면 예외가 발생

<br>

4. 트랜잭션 롤백 예외
    * 선언적 트랜잭션에서는 런타임 예외가 발생하면 롤백한다.
    * 예외가 전혀 발생하지 않거나, 체크 예외가 발생하면 커밋
        * 체크 예외가 커밋되는 이유는, 진짜 예외적인 상황에서 사용된다기 보다 리턴값을 대신해서 비즈니스적 의미를 담은 결과를 돌려주는 용도로 많이 사용되기 때문
        * rollbackFor, rollbackForClassName 앨리먼트를 이용하여 예외를 지정하면 해당 체크 예외는 롤백대상이 된다.=> 반대로 noRollbackFor 도 있다.
    
5. timeout 속성
    * 지정한 시간 내에 해당 메소드 수행이 완료되지 않은 경우 rollback

<br>

### Propagation 파헤쳐보기 ( feat: NESTED )

#### 첫번째 상황
```java
public class TestClass1 {

    private final TestClass2 testClass2;
    
    @Transactional
    public void test1() {
        try {
            testClass2.test2();
        } catch (RuntimeException ex) {
            // do something
        } finally {
            // do something
        }
    }   
}
```

```java
public class TestClass2 {

    @Transactional
    public void test2() {
        throw new RuntimeException();
    }   
}
```

* 설명
    * test1 method에서 test2 method의 결과에 따라 추가 작업해야한다.
    * 하지만 test2에서 runtimeException을 발생시키면 이미 롤백 마킹이 된다. (기본 전략: 런타임 예외, 롤백)
    * 따라서 이미 롤백 마킹이 된 트랜잭션을 통해서는 DB에 CRUD를 진행할 수 없다.
    
<br>

* 해결책
    * 이때 이용하는 것이 Nested 옵션 ( 중첩 트랜잭션 )
    * 자식(test2)의 트랜잭션은 부모(test1)의 트랜잭션에 영향을 받지만, 자식의 트랜잭션이 부모의 트랜잭션에는 영향을 미치지 않는다.
    * 즉 test2에서 RuntimeException이 발생해 Rollback이 되도 부모(test1)에서는 DB에 do something을 진행할 수 있다.
    
```java
public class TestClass2 {

    @Transactional(propagation = Propagation.NESTED)
    public void test2() {
        throw new RuntimeException();
    }   
}
```

* 추가 지식
    * 처음 Nested를 접했을 때 중첩 트랜잭션이니까 자식 트랜잭션이 새로 생성되는 것이라고 생각했다.
    * Spring 로그를 보며 트랜잭션 ID를 추적해보니 같은 트랜잭션을 이용하고 있었다!!
    * 결론은 innoDB(Mysql)의 savepoint를 이용하여 중첩되는 순간을 스냅샷으로 찍어두고, <br>
    해당 중첩이 롤백되면 savepoint로 rollback시켜 트랜잭션 전체에 영향을 미치지 않게 하는 방식이였다!!
