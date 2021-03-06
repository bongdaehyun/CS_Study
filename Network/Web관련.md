# 8주차

# 디자인 패턴

- 기존에 잘 설계된 코드나 큰 틀들을 잘 접목하여 결국 효율적이며 좋은 코드들을 재사용하기 용이하도록 도와주기 위한 방법론

## why ?

효율적이며 좋은 코드들의 재사용

1. **코드가 명확하고 단순**하여야 한다.

2. 각 **모듈 및 객체는 최소한의 기능**만을 하도록 세분화한다.

3. **재사용성**이 높아야 한다.

4. **유지보수**가 적거나 쉬어야 한다.

5. **리소스의 낭비가 없거나 최소화**하여야 한다.

## SOLID원칙

- 디자인 패턴들은 SOLID 원칙에 입각해서 만들어진 것!

### SRP(Single Responsibility Principle) : 단일 책임 원칙

객체는 단 하나의 책임만 가져야 한다는 원칙

**응집도를 높게, 결합도는 낮게** 설계

### OCP(Open-Closed Principle) : 개방-폐쇄 원칙

기존의 코드를 변경하지 않으면서, 기능을 추가할 수 있도록 설계가 되어야 한다는 원칙

→만족하는 설계, 캡슐화를 통해 여러 객체에서 사용하는 같은 기능을 인터페이스에 정의

### LSP(Liskov Substitution Principle) :리스코프 치환원칙

자식 클래스는 최사한 자신의 부모 클래스에서 가능한 행위는 수행할 수 있어야 한다는 원칙

→ 가급적 오버라이드를 피해라

### ISP (Interface Segregation Principle) : 인터페이스 분리 원칙

자신이 사용하지 않는 인터페이스는 구현하지 말아야 한다는 설계 원칙

### DIP(Dependency Inversion Principle) : 의존 역전 원칙

객체들이 서로 정보를 주고 받을 때 의존 관계가 형성되는데, 이 때 객체들은 나름대로의 원칙을 갖고 정보를 주고 받아야 한다는 설계 원칙

- 추상성이 낮은 클래스보다 추상성이 높은 클래스와 의존 관계를 맺어야 한다는 것

# Singletone

인스턴스가 오직 1개만 생성하여 그 메모리에 인스턴스를 만들어 사용하는 디자인 패턴

### 이유

1. 메모리 낭비 방지
2. 다른 클래스의 인스턴스들이 데이터를 공유하기 쉽다. → 전역 인스턴스이므로
3. DBCP처럼 공통된 객체를 여러개 생성해서 사용할때 → 안드로이드앱

> 고정된 메모리 영역을 얻으면서 한번의 new로 인스턴스를 사용하기 때문에 메모리 낭비를 방지할 수 있음, 또한 싱글톤으로 만들어진 클래스의 인스턴스는 전역 인스턴스이기때문에 다른 클래스의 인스턴스들이 데이터를 공유하기 쉽다.

→ 그래서 안드로이드 앱을 만들때 자주사용

### 장점

두 번째 이용시부터는 객체 로딩 시간이 현저하게 줄어 성능이 좋아진다

### 문제점

싱글톤 인스턴스가 너무 많은 일을 하거나 많은 데이터를 공유시킬 경우 다른 클래스의 인스턴스들 간에 결합도가 높아져 개방 -폐쇄 원칙을 위배

→ 수정이 어려워지고 테스트하기 어려워진다.

멀티스레드 환경에서 동기화처리를 안하면 인스턴스가 2개 생성

# JWT

기존에는 json으로 보내는 방식→단순한 문자열이기때문에 정보를 담거나 할 수 없다.

기존 방식의 문제 : 토큰을 관리할 방법이 없다. 토큰에 대해서 만료  X

### Json Web Token

클레임 기반 : 사용자 정보나 데이터속성을  JSON형식으로 저장 , 토큰안에 여러 정보를 담을 수 있다.

Header : 토큰의 타입 ,Signature를 해싱하기 위한 알고리즘을 지정

Payload :토큰에서 사용할 정보인 클레임

→ 등록된 클레임: 토큰 정보를 표현하기 위해 이미 정해진 종류, 공개 클레임 : 공개용, 비공개클레임 : 서버와 클라이언트 사이에 임의로 지정한 정보를 저장

Signature(HS256,SHA256)

### 단점

- Self-contained: 토큰 자체에 정보를 담고 있으므로 양날의 검이 될 수 있다.
- 토큰 길이: 토큰의 페이로드(Payload)에 3종류의 클레임을 저장하기 때문에, 정보가 많아질수록 토큰의 길이가 늘어나 네트워크에 부하를 줄 수 있다.
- Payload 인코딩: 페이로드(Payload) 자체는 암호화 된 것이 아니라, BASE64로 인코딩 된 것이다. 중간에 Payload를 탈취하여 디코딩하면 데이터를 볼 수 있으므로, JWE로 암호화하거나 Payload에 중요 데이터를 넣지 않아야 한다.
- Stateless: JWT는 상태를 저장하지 않기 때문에 한번 만들어지면 제어가 불가능하다. 즉, 토큰을 임의로 삭제하는 것이 불가능하므로 토큰 만료 시간을 꼭 넣어주어야 한다.
- Tore Token: 토큰은 클라이언트 측에서 관리해야 하기 때문에, 토큰을 저장해야 한다.

# HTTP status code

- 내가 했던 것들 봣던것들위주

### 200 OK

요청이 성공

### 400 Bad Request

서버에가 요청하여 이해할수 없다.

### 401 Unauthorized

비인증 

### 403 Forbidden

접근할 권리가 없다.

401과 다른점: 서버가 클라이언트가 누군지 알고있다.

### 404 Not Found

요청리소스를 찾을 수 없다.

### 500

웹사이트 서버에 문제가 있음

### 405 Method Not Allowed

요청한 get메소드가 API와 다를 경우..