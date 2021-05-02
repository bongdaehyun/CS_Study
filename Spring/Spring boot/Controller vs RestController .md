# Controller vs RestController

# 주요한 차이점

- Http Response Body가 생성되는 방식

# @Controller(Spring mvc controller)

## [Controller -View]

전통적인 Spring MVC의 컨트롤러인 @Controller는 주로 View를 반환하기 위해 사용합니다

![Controller%20vs%20RestController%20/Untitled.png](Controller%20vs%20RestController%20/Untitled.png)

1. Client는 URL 형식으로 웹서비스에 요청을 보낸다
2. Mapping되는 Handler와 그 Type을 찾는 DispatcherServlet이 요청을 인터셉트한다.
3. Controller가 요청을 처리한 후에 응답을 DispatcherServlet으로 반환하고, DispatcherServlet은 View를 사용자에게 반환한다.

@Controller가 View를 반환하기 위해서는 ViewResolver가 사용되며, ViewResolver 설정에 맞게 View를 찾아 렌더링합니다.

## [Controller - data]

하지만 Spring MVC의 컨트롤러에서도 Data를 반환해야 하는 경우도 있습니다. Spring MVC의 컨트롤러에서는 데이터를 반환하기 위해 @ResponseBody 어노테이션을 활용해주어야 합니다. 이를 통해 Controller도 Json 형태로 데이터를 반환할 수 있습니다.

![Controller%20vs%20RestController%20/Untitled%201.png](Controller%20vs%20RestController%20/Untitled%201.png)

1. Client는 URL 형식으로 웹서비스에 요청을 보낸다
2. Mapping되는 Handler와 그 Type을 찾는 DIspatcherServlet이 요청을 인터셉트한다.
3. @ResponseBody를 사용하여 Client에게 Json 형태로 데이터를 반환한다.

@RestController가 Data를 반환하기 위해서는 viewResolver 대신에 HttpMessageConverter가 동작합니다. HttpMessageConverter에는 여러 Converter가 등록되어 있고, 반환해야 하는 데이터에 따라 사용되는 Converter가 달라집니다. 단순 문자열인 경우에는 StringHttpMessageConverter가 사용되고, 객체인 경우에는 MappingJackson2HttpMessageConverter가 사용되며, 데이터 종류에 따라 서로 다른 MessageConverter가 작동하게 됩니다. Spring은 클라이언트의 HTTP Accept 헤더와 서버의 컨트롤러 반환 타입 정보 둘을 조합해 적합한 HttpMessageConverter를 선택하여 이를 처리합니다.

---

DispatcherServlet은 MessageConverter는 관리하지 않아서 거치지 않고 데이터를 반환한다.

- 예제코드

```java
@Controller
@RequestMapping("/user")
public class UserController {

    @Resource(name = "userService")
    private UserService userService;
		
		//User라는 데이터를 반환하고자 한다.
    @PostMapping(value = "/info")
    public @ResponseBody User info(@RequestBody User user){
        return userService.retrieveUserInfo(user);
    }
    
    @GetMapping(value = "/infoView")
    public String infoView(Model model, @RequestParam(value = "userName", required = true) String userName){
        User user = userService.retrieveUserInfo(userName);
        model.addAttribute("user", user);
        return "/user/userInfoView";
    }

}
```

---

# @RestController(Spring Restful Controller)

- @Controller + @ResponserBody 합친것
- 클래스 상단에 @RestController 어노테이션을 선언하면 Method마다 @ResponseBody를 붙여 주지 않아도 된다.

## [ RestController ]

@RestController는 Spring MVC Controller에 @ResponseBody가 추가된 것입니다. 당연하게도 RestController의 주용도는 Json 형태로 객체 데이터를 반환하는 것입니다. 개인적으로는 VueJS + Spring boot 프로젝트를 진행하며 Spring boot를 API 서버로 활용할 때 또는 Android 앱 개발을 하면서 데이터를 반환할 때 사용하였습니다.

![Controller%20vs%20RestController%20/Untitled%202.png](Controller%20vs%20RestController%20/Untitled%202.png)

1. Client는 URI 형식으로 웹 서비스에 요청을 보낸다.
2. Mapping되는 Handler와 그 Type을 찾는 DispatcherServlet이 요청을 인터셉트한다.
3. RestController는 해당 요청을 처리하고 데이터를 반환한다.

@RestController 에서 return 되는 값은 View Page를 통해 출력되는 것이 아니라 HTTP ResponseBody에 직접 쓰여지게 된다.

```java
@RestController
@RequestMapping("/user")
public class UserController {

    @Resource(name = "userService")
    private UserService userService;

    @PostMapping(value = "/info1")
    public User info1(@RequestBody User user){
        return userService.retrieveUserInfo(user);
    }

    @PostMapping(value = "/info2")
    public ResponseEntity<User> info2(@RequestParam(value = "userName", required = true) String userName){
        User user = userService.retrieveUserInfo(userName);

        if(user == null){
            return ResponseEntity.noContent().build()
        }

        return ResponseEntity.ok(user)
    }

    @PostMapping(value = "/info3")
    public ResponseEntity<User> info3(@RequestParam(value = "userName", required = true) String userName){
        return Optional.ofNullable(userService.retrieveUserInfo(userName))
                .map(user -> ResponseEntity.ok(user))
                .orElse(ResponseEntity.noContent().build());
    }
}
```

> @Controller와 @RestController는 용도의 차이라고 이해하시면 될 것 같습니다! 예전에 프로그래밍을 할 때에는 jsp나 html과 같은 뷰를 전달해 주었기 때문에 @Controller를 사용해왔었지만, 최근에는 프론트엔드와 백엔드를 따로 두고, 백엔드에서는 REST API를 통해 json으로 데이터만 전달하기 때문에 편리성을 위해 @RestController를 사용하게 되었습니다ㅎㅎ

# 결론

Spring MVC @Controller와 RESTful 컨트롤러인 @RestController의 차이점은 HTTP Response Body가 생성되는 방식이다.

@Controller 는 View Page를 반환하지만, @RestController는 객체(VO,DTO)를 반환하기만 하면, 객체데이터는 application/json 형식의 HTTP ResponseBody에 직접 작성되게 된다.

- spring-boot기반에서는 MessageConverter를 자동으로 셋팅해준다고한다.
