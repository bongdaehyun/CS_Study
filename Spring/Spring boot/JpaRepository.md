# JpaRepository

[JpaRepository (Spring Data JPA 2.5.3 API)](https://docs.spring.io/spring-data/jpa/docs/current/api/org/springframework/data/jpa/repository/JpaRepository.html)

```java
public interface UserHistoryRepository extends JpaRepository<UserHistory,Long> {
}
//기본 CRUD 사용 가능
```

[기본 CRUD](https://www.notion.so/0661bd90a1c640abbe103bf596ce6896)

# @Query

## 메서드 이름으로 쿼리 생성

- 메서드 이름만으로 JPQL 쿼리를 생성 → 애플리케이션 로딩 시점에 쿼리를 만들기 때문에 사전에 에러를 잡을 수 있다.

```java
public interface MemberRepository extends JpaRepository<Member, Long> {
    List<Member> findByName(String username);
}

// 실행된 SQL SELECT * FROM MEMBER M WHERE M.NAME = "hello"
```

## @Query, JPQL 정의

- @Query 어노테이션을 사용해서 직접 JPQL을 지정할 수 있다.
- 마찬가지로 Named 쿼리도 애플리케이션 로딩 시점에 파싱을 하므로, 이로 인해 런타임 에러를 내지 않을 수 있다.

```java
public interface MemberRepository extends JpaRepository<Member, Long> {
    
    @Query("select m from Member m where m.username = ?1")
    Member findByUsername(String username, Pageable pageable);
}

```

## QueryDSL

- SQL, JPQL을 **코드로** 작성할 수 있도록 도와주는 빌더 API
- JPA 크리테이라에 비해서 편리하고 실용적이다
- 오픈소스

### SQL, JPQL의 문제점

- SQL, JPQL은 문자열이다. Type-check가 불가능하다.
- 잘 해봐야 애플리케이션 로딩 시점에 알 수 있다. 컴파일 시점에 알 수 있는 방법이 없다. 자바와 문자열의 한계이다.
- 해당 로직 실행 전까지 작동여부 확인을 할 수 없다.
- 해당 쿼리 실행 시점에 오류를 발견한다.

[QueryDSL](https://ict-nroo.tistory.com/117)