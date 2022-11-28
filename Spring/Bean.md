# 1. 스프링 빈 (Spring Bean)

> 📌 Spring IoC 컨테이너가 관리하는 자바 객체를 **Bean**이라 부른다.



### **IoC 간단 정리**
    
>
    📌 Ioc란 : “제어의 역전” 으로 객체의 생성 및 제어권을 사용자가아닌 Spring에게 맡긴다는 의미이다. 
>
    
- Spring은 Java Programming과 달리 직접 new를 사용해 객체를 생성/사용하는 것이 아니라, Spring에 의하여 관리당하는 자바 객체를 사용한다.
    
* ▶ 이렇게 Spring IoC 컨테너이너에 의해 생성되고 관리(인스터스화, 관리, 생성)되는 자바 객체를 Bean이라 한다.
    - Bean은 **ApplicationContext.getBean()** 함수를 통해 얻어지는 객체이다. 그러므로 Bean은 ApplicaionContext가 생성하고 관리하는 객체이다.

<br>

> **<참고>** <br>Spring은 기본적으로 모든 Bean을 Singleton으로 생성하여 관리한다. Singletone Bean은 Spring Container에서 한 번 생성 하면 Container가 사라질 때까지 유지하다가 Container가 삭제되면 Bean도 제거 된다.
> 
> 
> ▶ 그렇기 때문에 Spring을 통해 Bean을 주입 받으면 이 Bean은 언제나 주입 받더라도 동일 객체임을 의미한다.
> 
> ▶ 동일 객체? 생성된 하나의 인스턴스는 Single Beans Cache에 저장되고 해당 Bean에 대한 요청과 참조가 있으면 이 Cacahe에서 객체를 반환해서 사용된다.
> 
<br>

## ✔️ Spring Bean을 Spring IoC Container에 등록하는 방법

### 1. 자바 어노테이션 사용 = **컴포넌트 스캔**

- 이 방법은 **@ComponentScan** 어노테이션과 **@Component** 어노테이션을 사용해서 빈을 등록하도록 하는 방법이다.
- **Life Cycle CallBack** : Spring IoC 컨테이너가 IoC 컨테이너를 만들고 그 안에 Bean을 등록할때 사용하는 Interface들
    - Life Cycle CallBack 작업 중에는 **@Component** 어노테이션을 찾아서 이 어노테이션이 붙어 있는 Class의 인스턴스를 생성해 Bean으로 등록하는 작업을 수행하는 Annotation Processor가 등록되어 있다.
            
        |Annotaion|Description|    
        |:---|:---|
        | @ComponentScan | ComponentScan은 @Component가 부여된 Class를 찾아 자동으로 Bean 등록하는 역할을 한다. 즉, ComponentScan이 붙어있는 Class의 package부터 모든 하위 package의 Class를 찾아 다니면 @Component나 다른 어노테이션을 사용하는 Class를 찾는다. |
        | @Component | Component는 Bean으로 등록할 Class를 의미한다. |
            
        ```java
        package hello.hellospring.controller;
        
        import hello.hellospring.service.MemberService;
        import org.springframework.beans.factory.annotation.Autowired;
        import org.springframework.stereotype.Controller;
        
        @Controller
        public class MemberController {
        
            private final MemberService memberService;
        
            @Autowired
            public MemberController(MemberService memberService) {
                this.memberService = memberService;
            }
        }
        ```
            

### 2. Bean **Configuration**를 사용해 직접 Bean 등록하는 방법

- 이 방법은 Java class에서 **@Configuration Annotation**을 사용해서 직접 **@Bean**을 등록해주는 방법이다.
    - @Bean Annotation을 사용해 직접 Bean을 정의하면 자동으로 Bean으로 등록된다.
    
    ```java
    **@Configuration**
    public class ExampleConfiguration {
        **@Bean**
        public ExampleController exampleController() {
    	        return new ExampleController;//return되는 객체 ExampleController가 Bean 등록된다.
        }
    }
    ```
    
    ```java
    @Component
    public class Example implements ExampleTest {
       @Autowired
       private ExampleController controller;
       ...
    }
    ```
    
    - @Configuration Annotation을 보면 이 Annotation도 내부적으로 @Component를 사용하기 때문에 **@ComponentScan의** 검색 대상이 되고, 그에 따라 Bean을 정의한 @Configuration이 읽힐때 그 안에 정의한 Bean들이 IoC Container에 등록되는 것이다.