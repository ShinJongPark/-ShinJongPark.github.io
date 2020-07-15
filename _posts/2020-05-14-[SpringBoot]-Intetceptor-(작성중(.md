title: "[SpringBoot] Intecepter - 작성중"
tag: "SpringBoot"



## Filter 와 Interceptor 비교

필터는 DispatcherServlet 앞에서 먼저 동작하며, 인터셉터는 DispatcherServlet에서 Controller(Handler) 사이에서 동작한다.

- 필터 ( Filter )
  - `웹 어플리케이션의 Context`의 기능
  - 스프링 기능을 활용하기에 어려움
  - 일반적으로 인코딩, CORS, XSS, LOG, 인증, 권한 등을 구현
- 인터셉터 ( Interceptor )
  - `스프링의 Spring Context`의 기능
  - 스프링 컨테이너이기에 다른 빈을 주입하여 활용성이 좋음
  - 다른 빈을 활용 가능하기에 인증, 권한 등을 구현함



## Interceptor 추가 및 설정

### dependency

스프링부트에서는 spring-webmvc가 spring-boot-starter-web에 포함되어 있다.

<br>

### Interceptor

기본 인터페이스는 `HandlerInterceptor`  이고, 추상클래스인 `HandlerInterceptorAdapter`를 다음과 같이 구현한다.

<br><br><br>