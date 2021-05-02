# Rest API

# API(Application Programming Interface)란

- 데이터와 기능의 집합을 제공하여 컴퓨터 프로그램간 상호작용을 촉진하며, 서로 정보를 교환가능 하도록 하는 것
- REST API의 정의
REST 기반으로 서비스 API를 구현한 것
최근 OpenAPI(누구나 사용할 수 있도록 공개된 API: 구글 맵, 공공 데이터 등), 마이크로 서비스(하나의 큰 애플리케이션을 여러 개의 작은 애플리케이션으로 쪼개어 변경과 조합이 가능하도록 만든 아키텍처) 등을 제공하는 업체 대부분은 REST API를 제공한다.

# Rest(Representational State Transfer)

- 분산 네트워크 프로그래밍의 아키텍쳐 스타일 —>기본적으로 웹의 기존 기술과 HTTP 프로토콜을 그대로 활용하기 때문에 웹의 장점을 최대한 활용할 수 있는 아키텍처 스타일이다.
- 자원을 이름(자원의 표현)으로 구분하여 해당 자원의 상태(정보)를 주고 받는 모든 것을 의미한다.

---

## 특성

1.  클라이언트/서버 : 클라이언트와  서버가 서로 독립적으로 구분되어야 하고 서버 또는 클라이언트 증설 시에 서로간의 의존성 때문에 확장에 문제가 되는 일이 없어야 한다.
2. 상태없음 : 클라이엍느와 서버 간의 통신 시에 상태가 없어야한다. 서버는 클라이언트의 상태를 기억할 필요가 없다. 
3. 레이어드 아키텍쳐(계층화) : 서버와 클라이언트 사이에 게이트웨이, 방화벽, 프록시가 있는 것처럼 다계층 형태로 레이어를 추가하거나 수정하거나 제거할 수 있고 확장성이 있어야 한다.
4. 캐시 : 서버의 응답들은 캐시를 가지고 있거나 없거나 둘 중의 하나인데, 캐시를 가지고 있을 경우에는 클라이언트가 캐시를 통해서 응답을 재사용할 수 있고 이를 통해서 서버의 부하를 낮추어서 서버의 성능이 향상
5. 코드 온 디멘드(Code on demand) : 요청이 오면 코드를 준다는 의미로 특정 시점에 서버가 특정 기능을 수행하는 스크립트 또는 플러그인을 클라이언트에 전달해서 동작하게 함. ex) js —>반드시 충족할 필요는 없다.
6. 통합 인터페이스 : 서버와 클라이언트 간의 상호 작용은 일관된 인터페이스들 위에서 이뤄져야 한다.

## 규칙

1. 리소스 식별 : URL와 같은 고유 식별자를 통해 표현
2. 표현을 통한 리소스 처리 :  데이터에 대해서 json,xml,html페이지와 같이 다양한 콘텐츠 유형을 표현 but 데이터는 변경되지 않는다.
3. 자기 묘사 메세지 : http header에 메타 데이터 정보를 추가해서 실제 데이터와는 관련없지만 데이터에 대한 설명을 나타내는 정보를 담을 수 있다.
4. 애플리케이션의 상태에 대한 하이퍼미디어 : 웹은 여러 페이지들과 그 페이지들을 이동할 수 있는 링크 정보들로 구성

# 리소스

- 리소스 식별자 URL
- URL 템플릿 : PathVariable 사용 ex) blog.example.com/name/20150603
- Json 형태를 자주 사용
    - Accept : text/xml, application/xml, application/json

# Rest api 만들기

- RestController : 별도의 ResponseBody 어노테이션을 사용하지 않고 RestAPI 만듬
- ResponseBody  : 실행결과에 대한 처리를 위한 어노테이션 , 실행결과를 view를 거치지 않고 Http Response body에 직접 입력된다.

```java
		private final AtomicLong counter = new AtomicLong();
		@RequestMapping(value = "/todo")
    public Todo basic(){
        return new Todo(counter.incrementAndGet(),"라면사오기");
    }

    @RequestMapping(value = "/todop", method = RequestMethod.POST)
    public Todo postBasic(@RequestParam(value = "todoTitle") String todoTitle){
        return new Todo(counter.incrementAndGet(), todoTitle);
    }
```

## Http method

- Get : 조회
- post : 생성
- put : 업데이트 요청

## 응답헤더 활용

응답헤더는 클라이언트에게 메터정보로 활용될 수 있다.

클라이언트에서 헤더정보를 먼저 읽을 수 있으므로 본문 내용을 읽을 필요가 없어서 통신 효율이 좋고 요청 결과에 대한 명확한 결과를 전달할 수 있다.

ResponseEntity는 HttpEntity를 상속받은 클래스로 Http 응답에 대한 상태값을 표현할 수 있음

```java
@ApiResponse(code = 400, message = "파라메터를 입력하지 않으셨습니다.")
    @RequestMapping(value = "/todor", method = RequestMethod.POST)
    public ResponseEntity<Todo> postBasicResponseEntity(@RequestParam(value = "todoTitle") String todoTitle){
        return new ResponseEntity(new Todo(counter.incrementAndGet(), todoTitle), HttpStatus.CREATED);
    }
```

## URL 템플릿 활용

- @PathVariable 활용

```java
		@RequestMapping(value = "/todos/{todoId}", method = RequestMethod.GET)
    public Todo getPath(@PathVariable int todoId){
         Todo todo1 = new Todo(1L, "문서쓰기");
         Todo todo2 = new Todo(2L, "기획회의");
         Todo todo3 = new Todo(3L, "운동");

        Map<Integer,Todo> todoMap = new HashMap();
        todoMap.put(1, todo1);
        todoMap.put(2, todo2);
        todoMap.put(3, todo3);

        return todoMap.get(todoId);
    }
```

# HATEOAS를 이용한 자기 주소정보 표현

```java
@RequestMapping(value = "/todoh", method = RequestMethod.GET)
public ResponseEntity<TodoResource> geth(@RequestParam(value = "todoTitle") String todoTitle){
    TodoResource todoResource = new TodoResource(todoTitle);
    todoResource.add(linkTo(methodOn(BasicController.class).geth(todoTitle)).withSelfRel());

    return  new ResponseEntity(todoResource, HttpStatus.OK);
}
```