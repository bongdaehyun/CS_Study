# Spring Framework

# ๐ฏ๏ธ๋ฑ์ฅ๋ฐฐ๊ฒฝ

1. EJB๋ฅผ ์ฌ์ฉํ์ฌ ์ปจํ์ด๋๋ฅผ ๊ด๋ฆฌํ๊ณ  ์ํฐํ๋ผ์ด์ฆ ์ ํ๋ฆฌ์ผ์ด์์ ๊ฐ๋ฐ์ ํด์ผ๋๋ ๋ฐ ๋ฌด๊ฒ๋ค..
2. ์ข๋ ๊ฒฝ๋ํ๋๊ณ  ๊ฐ์ํ๋ ์ปจํ์ด๋๋ฅผ ์ ํธ.
3. POJO ( ์ผ๋ฐ ์๋ฐ ํด๋์ค)
4. Spring ๋ฑ์ฅ

# โ๏ธIoCํจํด ํ์ฉ

- ํ๋ก๊ทธ๋จ์ ์๋ช ์ฃผ๊ธฐ์ ๋ํ ์ฃผ๋๊ถ์ด ์น ์ ํ๋ฆฌ์ผ์ด์ ์ปจํ์ด๋์ ์๋ค.
- ๋์์ธ ํจํด์ ์์น ์ค์๋ ์์กด ๊ด๊ณ ์ญ์  ์์น.
    1. ํ์ด๋ ๋ฒจ ๋ชจ๋์ ๋ก์ฐ๋ ๋ฒจ ๋ชจ๋์ ์์กดํด์๋ ์๋๊ณ  ๋ชจ๋ ์ธํฐํ์ด์ค์ ์์กดํด์ผ ํ๋ค.
    2. ์ถ์ํ๋ ์ธ๋ถ ์ฌํญ์ ์์กดํด์๋ ์๋๋ค. โ ์ธํฐํ์ด์ค๋ฅผ ํ์ฉํด ๊ฒฐํฉ๋๋ฅผ ๋ฎ์ถ๊ฒ ํ์
- ์๋ฐ์๋ ์ธ์คํด์คํํ๊ธฐ ์ํด์๋ ๊ฐ์ฒด ์์ฑ์ ํ์ํ ์ฝ๋๊ฐ ์๋ฐ๋๋ค.  โ> DI - ์์กด์ฑ ์ฃผ์

## ์ธํฐํ์ด์ค ์ฌ์ฉ

```java
//์ธํฐํ์ด์ค 
public interface WorkManager {
    public String doIt();
}

import javax.annotation.PostConstruct;
import javax.annotation.PreDestroy;

public class WorkService {
    WorkManager workManager;

    public void setWorkManager(WorkManager workManager){
        this.workManager = workManager;
    }

    public void askWork(){
        System.out.println( workManager.doIt() );
    }

    @PostConstruct
    public void onCreated() {
        System.out.println("์ด๊ธฐํ ๋์์ ๋");
    }

    @PreDestroy
    public void onDestroyed() {
        System.out.println("์ข๋ฃ๋์์ ๋");
    }
}

public class BasicApp {
    public static void main(String ar[]){
        WorkService workService = new WorkService();
        WorkManager employee = new Employee();
        WorkManager boss = new Boss();

        workService.setWorkManager(employee);
        workService.askWork();

        workService.setWorkManager(boss);
        workService.askWork();
    }
}
```

- asWork ๋ฉ์๋๋ฅผ ์ฌ์ฉํ ๋ ค๋ฉด Boss์ Emplyee์ ์ธ์คํด์ค ์์ฑ์ด ํ์ํ๋ค..
- ๊ฐ๊ฐ์ ํ์ํ ์ธ์คํด์ค๋ฅผ ์์ฑํด์ผ๋๋ค..

## ์คํ๋ง XML ์ค์ 

- ์คํ๋ง ์ปจํ์ด๋์ ํด๋์ค๋ฅผ ๋ฑ๋กํ๋ฉด ์คํ๋ง์ด ํด๋์ค์ ์ธ์คํด์ค๋ฅผ ๊ด๋ฆฌ
- ๋น์ ๋ฑ๋กํ๊ณ  ์ค์ ํ๋ ๋ฐฉ๋ฒ  XML๊ณผ Annotation

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="boss" class="basic.Boss" init-method="onCreated" destroy-method="onDestroyed"></bean>
    <bean id="employee" class="basic.Employee" init-method="onCreated" destroy-method="onDestroyed"></bean>

    <bean id="myWorkService" class="basic.WorkService">
        <property name="workManager">
            <ref bean="boss"/>
        </property>
    </bean>

    <bean id="yourWorkService" class="basic.WorkService">
        <property name="workManager">
            <ref bean="employee"/>
        </property>
    </bean>

</beans>
```

- beam ํ๊ทธ
    - class : ์ค์  ํด๋์ค ํ์ผ ๊ฒฝ๋ก
    - id : ์ฐธ์กฐ์ ์ฌ์ฉํ  ๊ฐ์ ์๋ ฅ ( ๋ณดํต id๊ฐ์ ํด๋์ค๋ช์ ์๋ฌธ์ ํํ๋ก ์๋ ฅ)
    - new ์ฐ์ฐ์๋ฅผ ์ด์ฉํด์ ์ธ์คํด์ค๋ฅผ ์์ฑ ํ๋ ์์์ ์คํ๋ง์ ์์ํ๋ค.
    - init-method : ์์ฑ์์ 
    - destory-method : ์๋ฉธ๋๋ ์์ 

```java
import basic.WorkService;
import org.springframework.context.support.GenericXmlApplicationContext;

public class XmlSpringApp {
    public static void main(String ar[]){
				
        GenericXmlApplicationContext context = new GenericXmlApplicationContext(
                "classpath:applicationContext.xml"
        );

        WorkService myWorkService = context.getBean("myWorkService", WorkService.class);
        myWorkService.askWork();

        WorkService yourWorkService = context.getBean("yourWorkService", WorkService.class);
        yourWorkService.askWork();
				
				//main์ ์ ์์ ์ผ๋ก ์ข๋ฃ
        context.close();
    }
}
```

- XML ์ค์ ์ ์ด์ฉํ๋ ค๋ฉด GenericXmlApplicationContext

![image/Inheritance.png](image/Inheritance.png)

## ์คํ๋ง JavaConfig

### @Configuration ์ด๋ธํ์ด์

- ๋น ์ค์  ์ ๋ณด๊ฐ ํฌํจ๋ ํด๋์ค์์ ๋ช์
- <bean> ํ๊ทธ โ @Bean๋ก ๋์ฒด

```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Import;

@Configuration
@Import(CompanyConfig.class)
public class BeanConfig {
    @Bean
    public WorkManager employee() {
        return new Employee();
    }

    @Bean
    public WorkManager boss() {
        return new Boss();
    }

    @Bean
    public WorkService yourWorkService() {
        WorkService workService = new WorkService();
        workService.setWorkManager(employee());
        return workService;
    }

    @Bean
    public WorkService myWorkService() {
        WorkService workService = new WorkService();
        workService.setWorkManager(boss());
        return workService;
    }
}

```

```java
public class JavaConfigSpringApp {
    public static void main(String ar[]){
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext();
        context.register(BeanConfig.class);
        context.refresh();

        WorkService yourWorkService = context.getBean("yourWorkService", WorkService.class);
        yourWorkService.askWork();

        WorkService myWorkService = context.getBean("myWorkService", WorkService.class);
        myWorkService.askWork();

        context.close();
    }
}
```

- AnnotationConfigApplicationContext()์ ์ด์ฉํ์ฌ @Bean ์ด๋ธํ์ด์ ๋ก๋

### ์๋ช ์ฃผ๊ธฐ ์ ์ด

```java
//์์ฑ
@PostConstruct
public void onCreated(){
}
//์๋ฉธ
@PreDestroy
public void onDestroyed(){
}

```

# ์คํ๋ง MVC

![image/flow.png](image/flow.png)

์คํ๋ง mvc ์์ฒญ ์ฒ๋ฆฌ ํ๋ฆ๋

## Dispatcher Servlet ์ค์ 

1. web.xml
2. bean์ ์ถ๊ฐ

## ์ปจํธ๋กค๋ฌ์ ๋ทฐ

```java
@Controller
public class IndexController {

	@RequestMapping("/")
    public ModelAndView home(){
       // return new ModelAndView("home");
        ModelAndView mv=new ModelAndView("home");
        mv.addObject("title", "Jpub Spring WEB");
        mv.addObject("today", new Date().toString());

        return mv;
    }
}
```

# ์ธํฐ์ํฐ

- ์ปจํธ๋กค๋ฌ๊ฐ ์์ฒญ์ ์ฒ๋ฆฌํ๊ธฐ ์  ํน์ ํ์ ๋ํด ๋ก์ง์ ์ถ๊ฐํ  ์ ์๋ค.

1. HandlerInterceptorAdaptor 

```java
public class JpubInterceptor extends HandlerInterceptorAdapter {
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        System.out.println("preHandle ๋ฉ์๋ ์คํ");
        return true;
    }

    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
        System.out.println("postHandle ๋ฉ์๋ ์คํ");
    }

    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        System.out.println("afterCompletion ๋ฉ์๋ ์คํ");
    }

    @Override
    public void afterConcurrentHandlingStarted(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        super.afterConcurrentHandlingStarted(request, response, handler);
    }
}
```
