# Spring boot

# Spring boot 등장배경

시작하는 입장에서는 많은 설정들이 부담스럽고 실제로 구현해야 하는 비즈니스 로직과는 관련없이 스프링 설정 오류 때문에 초반에 많은 시간을 허비하기도 한다.

—> 이를 해결하기 위한 스프링 부트 

## 스프링 부트의 프로젝트 레이아웃

- 그래들을 이용한 스프링 부트 설정

```java
plugins {
    id 'java'
    id 'org.springframework.boot' version '1.5.8.RELEASE'
}

ext{
    springBootVersion='1.5.8.RELEASE'
}

sourceCompatibility = 1.8
targetCompatibility = 1.8

sourceSets{
    main{
        java {
            srcDir 'src/main/java'
        }
        resources{
            srcDir 'src/resources'
        }
    }
}

repositories {
    jcenter()
}

dependencies {
    compile 'org.springframework.boot:spring-boot-starter-web'
    compile "org.springframework.boot:spring-boot-starter-thymeleaf"
    compile "org.springframework.boot:spring-boot-devtools"

    compile group: 'org.webjars', name: 'webjars-locator', version: '0.32'

    compile 'org.webjars:jquery:3.1.0'
    compile 'org.webjars:bootstrap:3.3.1'
    compile 'org.webjars:materializecss:0.96.0'

    compile 'org.slf4j:slf4j-api:1.7.7'

    testCompile 'junit:junit:4.12'

    //capcha
    compile group: 'com.google.code.maven-play-plugin.org.playframework', name: 'jj-imaging', version: '1.1'
    compile group: 'com.google.code.maven-play-plugin.org.playframework', name: 'jj-simplecaptcha', version: '1.1'
}
```

# Controller

```java
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HomeController {
    @RequestMapping("/")
    public String hello() {
        return "hello";
    }
}
```

- RestController는 데이터를 반환할때 사용, 별도의 뷰를 사용  X

[Controller vs RestController](Spring%20boot/Controller%20vs%20RestController%20.md)

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class UIMain {
    public static void main(String ar[]){
        SpringApplication.run(UIMain.class, ar);
    }
}
```

- 스프링 부트는 기본적으로 WAR가 아니라 JAR형태로 동작
- EnableAutoConfiguration어노테이션은 공통적으로 필요한 DIspatcherServlet 같은 설정을 어노테이션을 이용해 대신할 수 있도록 한다.

## @SpringBootApplication 어노테이션의 역할

스캔 패키지를 지정하는 ComponentScan과 설정임을 나태는 Configuration 그리고 미리 정의된 xxxConfiguration 클래스들을 읽을 수 있도록 하는 EnableautoConfiguration 어노테이션이 필요하다.

이 세가지를 대체하는 것 !! SpringBootApplication

# 템플릿 엔진

- 서식과 데이터를 결합한 결과물을 만들어 주는 도구
- 서식은 html과 같은 마크업에 해당하고 데이터는 데이터베이스에 저장된 데이터를 뜻한다.
- 스프링 부트에서는 JSP를 권장하지 않으므로 타임리프를 사용

즉, 웹 템플릿 엔진은 웹 템플릿들과 웹 컨텐츠 정보를 처리하기 위해 설계된 소프트웨어입니다. 웹 템플릿 엔진은 view code(html)와 data logic code(db connection)을 분리해주는 기능을 합니다.

![Spring%20boot/template.png](Spring%20boot/template.png)

## 템플릿 엔진의 필요성

(1) . 대부분의 Template Engine은 HTML에 비해 간단한 문법을 사용함으로서 코드량을 줄일 수 있습니다.

(2) . 데이터만 바뀌는 경우가 굉장히 많으므로 재사용성을 높일 수 있습니다.

(3) . 유지 보수에 용이합니다.

## 타임리프 속성

### 변수 표현식

- 하나의 변수값은 ${변수명}을 이용하여 데이터를 가져올 수 있다.
- 객체의 프로퍼티를 출력하고자 하는 경우에는 *로 객체이름을 명시한 뒤에 속성값들을 출력한다. or 닷 연산자 사용 가능 (.)

```java
<!DOCTYPE html>
<!-- 타임리프를 명시적으로 사용하기 위한 것--!>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>thymeleaf</title>
</head>
<body>
<div th:object="${product}">
    <p>name: <span th:text="*{name}"></span></p>
    <p>color: <span th:text="*{color}"></span></p>
    <p>price: <span th:text="*{price}"></span></p>

    <div th:if="${product.price} > 3000" th:text="비싸다"/>
    <div th:if="${product.price} > 1500" th:text="적당하다"/>

    <div th:unless="${product.price} >3000" th:text="비싸다"/>
</div>
</body>
</html>
```

### 조건문 표현

- if, unless, case

```html

조건에 부합하면 출력
<div th:if="${product.price} > 3000" th:text="비싸다"/>

if와 반대로 사용하려면 unless
<div th:unless="${product.price} > 3000" th:text="비싸다"/>

```

### 반복문 표현

- each태그를 이용

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>thymeleaf3</title>
    <script type="text/javascript" th:src="@{/webjars/jquery/jquery.min.js}"></script>
</head>
<body>
<table border="1">
    <tr>
        <th>color</th>
        <th>name</th>
        <th>price</th>
    </tr>
    <tr th:each="prod : ${products}">
        <td th:text="${prod.color}"></td>
        <td th:text="${prod.productName}"></td>
        <td th:text="${prod.price}"></td>
    </tr>
</table>
<script type="text/javascript">
    console.log($.fn.jquery);
</script>
</body>
</html>
```
