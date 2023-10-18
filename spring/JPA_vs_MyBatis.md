# 영속성

프로그램이 종료되어도 데이터가 사라지지 않고, 특정 위치에 저장되는 특성
자바에서는 데이터의 영속성을 위해 JDBC를 지원한다.

![JDBC 워크 플로우](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FmvJsf%2FbtrbV1OZeUh%2F809rQdvQFFWZ8eJoiWFCg1%2Fimg.jpg)
[출처] https://slideplayer.com/slide/8423691/

위의 그림과 같이 JDBC에서 DB에 접근하여 SQL을 수행하고, 결과값을 다시 dataType으로 매핑시켜줘야 하기 때문에 번거로움이 있다.

ORM과 SQL Mapper은 개발자가 직접 JDBC 프로그래밍을 하지 않도록 기능을 제공해주는 Persistence Framework이다.

# ORM (Object Relation Mapping)

### JPA (Java Persistence API)

### 개념:
- 객체-관계 매핑(Object-Relational Mapping)의 약어로, 자바 애플리케이션의 객체와 데이터베이스 테이블 간의 매핑을 돕는 기술.
- 객체 지향 프로그래밍 언어에서의 클래스와 관계형 데이터베이스의 테이블 사이의 매핑을 추상화하고 자동화하는 방식을 제공.
### 특징:
- 데이터베이스 테이블과 자바 객체 간의 복잡한 매핑 작업을 자동화하여 개발자의 생산성 향상.
- 객체 지향 프로그래밍의 개념을 유지하면서 데이터베이스 조작이 가능.
- JPQL 등의 객체 지향 쿼리 언어 제공으로 데이터베이스 종속성 최소화.
- 엔티티 관리와 생명주기 추적을 통해 일관된 데이터 상태 유지.
- 트랜잭션 관리를 통해 데이터 일관성 보장.

### 대표적인 구현체:
- Hibernate, EclipseLink, OpenJPA 등.

### 사용 방법

![](https://velog.velcdn.com/images/hyuntall/post/b78e266c-3971-4b64-a931-7f625bb97579/image.png)
- Spring Boot build.gradle 파일에 다음과 같은 종속성 추가

![](https://velog.velcdn.com/images/hyuntall/post/91e28f3d-5ab5-4b19-be0c-4ea23f9e0f1c/image.png)
- 다음과 같이 특정 테이블 (in_game_role)에 매핑되는 DTO 생성 및 각 속성 별로 column 매칭

![](https://velog.velcdn.com/images/hyuntall/post/5e64bb7f-9d79-478a-b077-de9e67bb6534/image.png)

- JpaRepository(해당 DTO 타입)를 상속받은 Repository 파일 생성

![](https://velog.velcdn.com/images/hyuntall/post/53c389c9-e27c-49e5-a9ee-53de05145505/image.png)
- 해당 repository 객체의 메서드 실행
메서드 종류:
- save
- delete
- findById
- findAll
- update

# SQL Mapper

### Mybatis

### 개념:
- SQL Mapper는 객체와 SQL 쿼리 간의 매핑을 중심으로 동작하는 기술.
- SQL 쿼리를 직접 작성하고 이를 객체의 메서드에 매핑하여 데이터베이스 작업을 수행.
### 특징:
- SQL 쿼리의 직접 작성과 관리를 개발자에게 맡김.
- 데이터베이스 스키마와의 일치를 위해 개발자가 직접 매핑 작업을 수행해야 함.
- 일반적으로 복잡한 쿼리 작업에 유용하며, 프로젝트의 데이터베이스 구조와 직접적으로 연결됨.

대표적인 구현체:
- MyBatis(SQL Mapper의 대표적인 예시), jOOQ 등.

# 요약:

- ORM은 객체와 데이터베이스 간의 매핑을 자동화하여 개발자에게 편의성을 제공하며, 객체 지향적인 접근 방식을 강조함.
- SQL Mapper는 개발자가 직접 SQL 쿼리를 작성하고 관리하며, 복잡한 쿼리 작업에 적합하며 더 세밀한 제어가 필요한 경우에 사용될 수 있음.
