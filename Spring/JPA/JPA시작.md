# JPA 시작

# 라이브러리

1. 하이버네이트 (JPA 구현체)
2. H2 데이터베이스

```xml
<!-- JPA 하이버네이트 -->
        <!-- https://mvnrepository.com/artifact/org.hibernate/hibernate-entitymanager -->
        <dependency>
            <groupId>org.hibernate</groupId>
            <artifactId>hibernate-entitymanager</artifactId>
            <version>5.3.10.Final</version>
        </dependency>

        <!-- H2 데이터베이스 -->
        <dependency>
            <groupId>com.h2database</groupId>
            <artifactId>h2</artifactId>
            <version>1.4.199</version>
        </dependency>
```

# persistence.xml 설정

```xml
<?xml version="1.0" encoding="UTF-8"?> 
<persistence version="2.2" 
 xmlns="http://xmlns.jcp.org/xml/ns/persistence" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
 xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/persistence http://xmlns.jcp.org/xml/ns/persistence/persistence_2_2.xsd"> 
 <persistence-unit name="hello"> 
 <properties> 
 <!-- 필수 속성 --> 
 <property name="javax.persistence.jdbc.driver" value="org.h2.Driver"/> 
 <property name="javax.persistence.jdbc.user" value="sa"/> 
 <property name="javax.persistence.jdbc.password" value=""/> 
 <property name="javax.persistence.jdbc.url" value="jdbc:h2:tcp://localhost/~/test"/> 
 <property name="hibernate.dialect" value="org.hibernate.dialect.H2Dialect"/> 
 
 <!-- 옵션 --> 
 <property name="hibernate.show_sql" value="true"/> 
 <property name="hibernate.format_sql" value="true"/> 
 <property name="hibernate.use_sql_comments" value="true"/> 
 <!--<property name="hibernate.hbm2ddl.auto" value="create" />--> 
 </properties> 
 </persistence-unit> 
</persistence>
```

---

- Spring을 이용할시에는 깻잎 설정파일에다가 설정하면됨
- JPA만을 이용한 설정을 하기위함

# 데이터베이스 방언

- `JPA는 특정 데이터베이스에 종속 X`

![JPA%20%E1%84%89%E1%85%B5%E1%84%8C%E1%85%A1%E1%86%A8%209d2c7657a7fb4cd886e95f8db2750f3b/Untitled.png](JPA%20%E1%84%89%E1%85%B5%E1%84%8C%E1%85%A1%E1%86%A8%209d2c7657a7fb4cd886e95f8db2750f3b/Untitled.png)

# JPA 구동 방식

![JPA%20%E1%84%89%E1%85%B5%E1%84%8C%E1%85%A1%E1%86%A8%209d2c7657a7fb4cd886e95f8db2750f3b/Untitled%201.png](JPA%20%E1%84%89%E1%85%B5%E1%84%8C%E1%85%A1%E1%86%A8%209d2c7657a7fb4cd886e95f8db2750f3b/Untitled%201.png)

## 주의

1. 엔티티 매니저 팩토리는 하나만 생성해서 애플리케이션 전체에
서 공유
2. 엔티티 매니저는 쓰레드간에 공유X (사용하고 버려야 한다).
3. JPA의 모든 데이터 변경은 트랜잭션 안에서 실행

```java
public class JpaMain {
    public static void main(String[] args) {

        EntityManagerFactory emf=Persistence.createEntityManagerFactory("hello");

        EntityManager em=emf.createEntityManager();
        EntityTransaction tx= em.getTransaction();
        //트랜잭션 연결
        tx.begin();
        /*
        Member member=new Member();
        member.setId(4L);
        member.setName(("HelloA"));
        em.persist(member);

        //트랜잭션 커밋
        tx.commit();
        em.close();
        */
        //정석 코드
        try{
            //insert
//            Member member=new Member();
//            member.setId(4L);
//            member.setName(("HelloA"));
//            em.persist(member);
            /* JPA
            Member findMember=em.find(Member.class,4L);
            //수정
            findMember.setName("SpringJPA");
            */
            //JPQL m-> 멤버 객체 ,페이징.
            List<Member> result=em.createQuery("select m from Member as m",Member.class)
                    .setFirstResult(1)
                    .setMaxResults(2)
                    .getResultList();

            for(Member member:result){
                System.out.println("member.name= "+member.getName());
            }
            //트랜잭션 커밋
            tx.commit();
        }catch (Exception e){
            e.printStackTrace();
            tx.rollback();
        }finally {
            em.close();
        }

        emf.close();
    }
}
```

# JPQL

## why use?

- JPA를 사용하면 엔티티 객체를 중심으로 개발
- 검색 쿼리 문제
- 검색을 할때 도 테이블이 아닌 엔티티 객체 대상으로 검색
- 모든 DB데이터를 객체로 변환해서 검색하는 걸 불가
- 애플리케이션이 필요한 데이터만 DB에서 불러오려면 결국 검
색 조건이 포함된 SQL이 필요

## JPQL

- JPA는 SQL을 추상화한 JPQL이라는 객체 지향 쿼리 언어 제공
- SQL과 문법 유사, SELECT, FROM, WHERE, GROUP BY,
HAVING, JOIN 지원
- JPQL은 엔티티 객체를 대상으로 쿼리
- **객체 지향 SQL**