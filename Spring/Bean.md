# 1. ์คํ๋ง ๋น (Spring Bean)

> ๐ Spring IoC ์ปจํ์ด๋๊ฐ ๊ด๋ฆฌํ๋ ์๋ฐ ๊ฐ์ฒด๋ฅผ **Bean**์ด๋ผ ๋ถ๋ฅธ๋ค.



### **IoC ๊ฐ๋จ ์ ๋ฆฌ**
    
>
    ๐ Ioc๋ : โ์ ์ด์ ์ญ์ โ ์ผ๋ก ๊ฐ์ฒด์ ์์ฑ ๋ฐ ์ ์ด๊ถ์ ์ฌ์ฉ์๊ฐ์๋ Spring์๊ฒ ๋งก๊ธด๋ค๋ ์๋ฏธ์ด๋ค. 
>
    
- Spring์ Java Programming๊ณผ ๋ฌ๋ฆฌ ์ง์  new๋ฅผ ์ฌ์ฉํด ๊ฐ์ฒด๋ฅผ ์์ฑ/์ฌ์ฉํ๋ ๊ฒ์ด ์๋๋ผ, Spring์ ์ํ์ฌ ๊ด๋ฆฌ๋นํ๋ ์๋ฐ ๊ฐ์ฒด๋ฅผ ์ฌ์ฉํ๋ค.
    
* โถ ์ด๋ ๊ฒ Spring IoC ์ปจํ๋์ด๋์ ์ํด ์์ฑ๋๊ณ  ๊ด๋ฆฌ(์ธ์คํฐ์คํ, ๊ด๋ฆฌ, ์์ฑ)๋๋ ์๋ฐ ๊ฐ์ฒด๋ฅผ Bean์ด๋ผ ํ๋ค.
    - Bean์ **ApplicationContext.getBean()** ํจ์๋ฅผ ํตํด ์ป์ด์ง๋ ๊ฐ์ฒด์ด๋ค. ๊ทธ๋ฌ๋ฏ๋ก Bean์ ApplicaionContext๊ฐ ์์ฑํ๊ณ  ๊ด๋ฆฌํ๋ ๊ฐ์ฒด์ด๋ค.

<br>

> **<์ฐธ๊ณ >** <br>Spring์ ๊ธฐ๋ณธ์ ์ผ๋ก ๋ชจ๋  Bean์ Singleton์ผ๋ก ์์ฑํ์ฌ ๊ด๋ฆฌํ๋ค. Singletone Bean์ Spring Container์์ ํ ๋ฒ ์์ฑ ํ๋ฉด Container๊ฐ ์ฌ๋ผ์ง ๋๊น์ง ์ ์งํ๋ค๊ฐ Container๊ฐ ์ญ์ ๋๋ฉด Bean๋ ์ ๊ฑฐ ๋๋ค.
> 
> 
> โถ ๊ทธ๋ ๊ธฐ ๋๋ฌธ์ Spring์ ํตํด Bean์ ์ฃผ์ ๋ฐ์ผ๋ฉด ์ด Bean์ ์ธ์ ๋ ์ฃผ์ ๋ฐ๋๋ผ๋ ๋์ผ ๊ฐ์ฒด์์ ์๋ฏธํ๋ค.
> 
> โถ ๋์ผ ๊ฐ์ฒด? ์์ฑ๋ ํ๋์ ์ธ์คํด์ค๋ Single Beans Cache์ ์ ์ฅ๋๊ณ  ํด๋น Bean์ ๋ํ ์์ฒญ๊ณผ ์ฐธ์กฐ๊ฐ ์์ผ๋ฉด ์ด Cacahe์์ ๊ฐ์ฒด๋ฅผ ๋ฐํํด์ ์ฌ์ฉ๋๋ค.
> 
<br>

## โ๏ธ Spring Bean์ Spring IoC Container์ ๋ฑ๋กํ๋ ๋ฐฉ๋ฒ

### 1. ์๋ฐ ์ด๋ธํ์ด์ ์ฌ์ฉ = **์ปดํฌ๋ํธ ์ค์บ**

- ์ด ๋ฐฉ๋ฒ์ **@ComponentScan** ์ด๋ธํ์ด์๊ณผ **@Component** ์ด๋ธํ์ด์์ ์ฌ์ฉํด์ ๋น์ ๋ฑ๋กํ๋๋ก ํ๋ ๋ฐฉ๋ฒ์ด๋ค.
- **Life Cycle CallBack** : Spring IoC ์ปจํ์ด๋๊ฐ IoC ์ปจํ์ด๋๋ฅผ ๋ง๋ค๊ณ  ๊ทธ ์์ Bean์ ๋ฑ๋กํ ๋ ์ฌ์ฉํ๋ Interface๋ค
    - Life Cycle CallBack ์์ ์ค์๋ **@Component** ์ด๋ธํ์ด์์ ์ฐพ์์ ์ด ์ด๋ธํ์ด์์ด ๋ถ์ด ์๋ Class์ ์ธ์คํด์ค๋ฅผ ์์ฑํด Bean์ผ๋ก ๋ฑ๋กํ๋ ์์์ ์ํํ๋ Annotation Processor๊ฐ ๋ฑ๋ก๋์ด ์๋ค.
            
        |Annotaion|Description|    
        |:---|:---|
        | @ComponentScan | ComponentScan์ @Component๊ฐ ๋ถ์ฌ๋ Class๋ฅผ ์ฐพ์ ์๋์ผ๋ก Bean ๋ฑ๋กํ๋ ์ญํ ์ ํ๋ค. ์ฆ, ComponentScan์ด ๋ถ์ด์๋ Class์ package๋ถํฐ ๋ชจ๋  ํ์ package์ Class๋ฅผ ์ฐพ์ ๋ค๋๋ฉด @Component๋ ๋ค๋ฅธ ์ด๋ธํ์ด์์ ์ฌ์ฉํ๋ Class๋ฅผ ์ฐพ๋๋ค. |
        | @Component | Component๋ Bean์ผ๋ก ๋ฑ๋กํ  Class๋ฅผ ์๋ฏธํ๋ค. |
            
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
            

### 2. Bean **Configuration**๋ฅผ ์ฌ์ฉํด ์ง์  Bean ๋ฑ๋กํ๋ ๋ฐฉ๋ฒ

- ์ด ๋ฐฉ๋ฒ์ Java class์์ **@Configuration Annotation**์ ์ฌ์ฉํด์ ์ง์  **@Bean**์ ๋ฑ๋กํด์ฃผ๋ ๋ฐฉ๋ฒ์ด๋ค.
    - @Bean Annotation์ ์ฌ์ฉํด ์ง์  Bean์ ์ ์ํ๋ฉด ์๋์ผ๋ก Bean์ผ๋ก ๋ฑ๋ก๋๋ค.
    
    ```java
    @Configuration
    public class ExampleConfiguration {
        @Bean
        public ExampleController exampleController() {
    	        return new ExampleController;//return๋๋ ๊ฐ์ฒด ExampleController๊ฐ Bean ๋ฑ๋ก๋๋ค.
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
    
    - @Configuration Annotation์ ๋ณด๋ฉด ์ด Annotation๋ ๋ด๋ถ์ ์ผ๋ก @Component๋ฅผ ์ฌ์ฉํ๊ธฐ ๋๋ฌธ์ **@ComponentScan์** ๊ฒ์ ๋์์ด ๋๊ณ , ๊ทธ์ ๋ฐ๋ผ Bean์ ์ ์ํ @Configuration์ด ์ฝํ๋ ๊ทธ ์์ ์ ์ํ Bean๋ค์ด IoC Container์ ๋ฑ๋ก๋๋ ๊ฒ์ด๋ค.