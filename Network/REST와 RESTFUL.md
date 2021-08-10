# REST와 RESTFUL

# REST

![REST%E1%84%8B%E1%85%AA%20RESTFUL%2024d6b254003a4df4b7050fbd39ee9451/Untitled.png](REST%E1%84%8B%E1%85%AA%20RESTFUL%2024d6b254003a4df4b7050fbd39ee9451/Untitled.png)

## 정의

자원을 이름(자원의 표현)으로 구분하여 해당 자원의 상태(정보)를 주고 받는 

모든 것을 의미한다.

- 자원의 표현에 의한 상태 전달
    - 자원의 표현
    - 상태(정보) 전달

HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고, HTTP Method(POST, GET, PUT, DELETE)를 통해 해당 자원에 대한 CRUD Operation을 적용하는 것을 의미한다.

- CRUD Operation
    - Create : 생성(POST)
    - Read : 조회(GET)
    - Update : 수정(PUT)
    - Delete : 삭제(DELETE)
    - HEAD: header 정보 조회(HEAD)

## 장단점

### 장점

- HTTP 프로토콜의 인프라를 그대로 사용하므로 REST API 사용을 위한 별도의 인프라를 구출할 필요가 없다.
- HTTP 프로토콜의 표준을 최대한 활용하여 여러 추가적인 장점을 함께 가져갈 수 있게 해준다.
- HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.
- Hypermedia API의 기본을 충실히 지키면서 범용성을 보장한다.
- REST API 메시지가 의도하는 바를 명확하게 나타내므로 의도하는 바를 쉽게 파악할 수 있다.
- 여러가지 서비스 디자인에서 생길 수 있는 문제를 최소화한다.
서버와 클라이언트의 역할을 명확하게 분리한다.

### 단점

- 표준이 존재 X
- HTTP Method 형태가 제한적
- 구형 브라우저가 아직 제대로 지원해주지 못한다는 부분이 존재

## 구성요소

1. 자원 : URL
    - Client는 URI를 이용해서 자원을 지정하고 해당 자원의 상태(정보)에 대한 조작을 Server에 요청한다
2. 행위 : HTTP Method
    - GET, POST, PUT, DELETE
3. 표현 
    - Client가 자원의 상태(정보)에 대한 조작을 요청하면 Server는 이에 적절한 응답(Representation)을 보낸다.
    - REST에서 하나의 자원은 JSON, XML, TEXT, RSS 등 여러 형태의 Representation으로 나타내어 질 수 있다
    - JSON 혹은 XML를 통해 데이터를 주고 받는 것이 일반적이다.

## REST 특징

1. Server-Client
2. Stateless
3. Cacheable
4. Layered System
5. Code-On-Demand
6. Uniform Interface(인터페이스 일관성)
    - HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용 가능

# REST API

![REST%E1%84%8B%E1%85%AA%20RESTFUL%2024d6b254003a4df4b7050fbd39ee9451/Untitled%201.png](REST%E1%84%8B%E1%85%AA%20RESTFUL%2024d6b254003a4df4b7050fbd39ee9451/Untitled%201.png)

> API : 데이터와 기능의 집합을 제공하여 컴퓨터 프로그램간 상호작용을 촉진하며, 서로 정보를 교환 가능하도록 하는 것

REST API의 정의

- REST 기반으로 서비스 API를 구현한 것
- 최근 OpenAPI, 마이크로 서비스 등을 제공하는 업체 대부분은 REST API를 제공

![REST%E1%84%8B%E1%85%AA%20RESTFUL%2024d6b254003a4df4b7050fbd39ee9451/Untitled%202.png](REST%E1%84%8B%E1%85%AA%20RESTFUL%2024d6b254003a4df4b7050fbd39ee9451/Untitled%202.png)

## 특징

- 사내 시스템들도 REST 기반으로 시스템을 분산해 확장성과 재사용성을 높여 유지보수 및 운용을 편리하게 할 수 있다.
- REST는 HTTP 표준을 기반으로 구현하므로, HTTP를 지원하는 프로그램 언어로 클라이언트, 서버를 구현할 수 있다.
- 즉, REST API를 제작하면 델파이 클라이언트 뿐 아니라, 자바, C#, 웹 등을 이용해 클라이언트를 제작할 수 있다.

# REST FUL

- RESTful은 일반적으로 REST라는 아키텍처를 구현하는 웹 서비스를 나타내기 위해 사용되는 용어이다.
    - ‘REST API’를 제공하는 웹 서비스를 ‘RESTful’하다고 할 수 있다.
- RESTful은 REST를 REST답게 쓰기 위한 방법으로, 누군가가 공식적으로 발표한 것이 아니다.
    - 즉, REST 원리를 따르는 시스템은 RESTful이란 용어로 지칭된다

## 목적

- 이해하기 쉽고 사용하기 쉬운 REST API를 만드는 것
- RESTful한 API를 구현하는 근본적인 목적이 성능 향상에 있는 것이 아니라 일관적인 컨벤션을 통한 API의 이해도 및 호환성을 높이는 것이 주 동기이니, 성능이 중요한 상황에서는 굳이 RESTful한 API를 구현할 필요는 없다.