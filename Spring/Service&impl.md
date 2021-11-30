# Service

# Spring MVC에서 Service의 역할

## 의문점

MVC패턴에서 비즈니스 로직 구성은 Controller, Service, Dao로 역할을 분산시켜 개발한다.

개발을 할때 Service 인터페이스 클래스를 생성하고 이에 1대1 로 매칭되는 Impl을 새로 구현하여 사용할 뿐.. 이럴거면 Interface를 만들어내는 의미가 있나?? 하나의 규칙을 바탕으로 여러 곳에서 사용해야되는 목적이 있을텐데..

[[Spring] Service와 ServiceImpl](https://itzjamie96.github.io/2021/01/24/spring-service-and-serviceimpl/)

- Service : 역할
- Service Impl : 구현

⇒ 유연하고 변경이 용이하다는 객체지향적인 특징때문에

## Service Model의 역할

DAO는 단일 데이터 접근 로직 → SQL 하나 보내고 결과를 받아오는 것!!

여러 번의 DB접근이 필요하고 어떤 서비스는 병렬식으로 데이터를 가져와야되는 상황이 있다.

1. 하나의 서비스를 위해 여러개의 DAO를 묶은 트랜잭션이 생성되고, Service는 곧 트랜잭션의 단위가 된다.

1. Controller 내부에서 필요한 여러 Service를 구분하는 필요성을 가진다. 비슷한 요청이더라도 내부 로직이 달라야한다면 Controller는 매우 복잡해질 가능성이 있다. 이러한 점을 분리하여 Controller는 단순이 요청을 받아 해당 요청에 맞는 Service에 데이터를 주입하는 역할. Service는 자신이 수행해야 할 서비스를 진행할 뿐이었다.

→ 재사용성을 높인다.

먼저 Service와 DAO로 나뉘는 것은 **"Layered Architecture"**라는 아키텍쳐로 **Presentation Layer, Business Layer, Persistence Layer, Database Layer**로 나뉘어져 있으며, 대형 프로젝트에서 역할에 따라 분류함으로써 각 로직에 대해 복잡성을 줄일 수 있고 테스트 하기 용이합니다.

컨트롤러는 서비스에게 특정 업무를 요청하고, 서비스는 업무를 요청하며 필요한 자료를 DAO에게 요청하거나, 업무를 통해 나온 자료를 DAO를 통해 저장합니다.

[[Spring] MVC : Controller와 Service의 책임 나누기](https://umbum.dev/1066)