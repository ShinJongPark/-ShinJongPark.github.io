---
title: "[SpringBoot] EnableAutoConfiguration, ComponentScan "
tag: "SpringBoot"
author : ""
article_header:
  type: overlay
  theme: dark
  background_color: '#123'
  background_image:
    gradient: 'linear-gradient(135deg, rgba(34, 139, 87 , .4), rgba(139, 34, 139, .4))'
    src: /assets/images/logo/green.jpg
---
<br>

> SpringBoot에서 web 프로젝트를 최초로 생성하면 ProjectNameApplication 클래스가 기본적으로 생성되며, main() 메소드로 실행할 수 있다.
>
> ```java
> import org.springframework.boot.SpringApplication;
> import org.springframework.boot.autoconfigure.SpringBootApplication;
> 
> @SpringBootApplication
> public class ProjectNameApplication {
> 
> 	public static void main(String[] args) {
> 		SpringApplication.run(ProjectNameApplication.class, args);
> 	}
> }
> ```
>
> 따라서, 기본적으로 제공되는 메인 클래스를 실행하면 내장 톰캣이 구동되어 웹 어플리케이션을 실행시킬 수 있다. (원하면 일반 자바 애플리케이션으로 실행시킬 수 도 있다.)
>
> 스프링 부트는 기본적인 기능의 class들을 빈으로 **자동설정**하여 사용자가 아무런 설정 없이도 실행할 수 있게 한다.
>
> 어떻게 **자동설정**이 구현되어 있을지 알아보고자 한다.

<br>

<br>

## @SpringBootApplication 어노테이션

> `@SpringBootApplication` 는 이 클래스가 스프링 부트로 만든 애플리케이션의 시작 클래스임을 의미하며, 웹 애플리케이션에서 주로 사용하는 `@SpringBootConfiguration`, `@ComponentScan` , `@EnableAutoConfiguration`을 기본적으로 포함하고 있다.
>
> ```java
> @Target(ElementType.TYPE)
> @Retention(RetentionPolicy.RUNTIME)
> @Documented
> @Inherited
> @SpringBootConfiguration
> @EnableAutoConfiguration
> @ComponentScan(excludeFilters = { @Filter(type = FilterType.CUSTOM, classes = TypeExcludeFilter.class),
> 		@Filter(type = FilterType.CUSTOM, classes = AutoConfigurationExcludeFilter.class) })
> public @interface SpringBootApplication {
> 	~
> }
> ```
>
> 자동 설정에 가장 중요한 것은 위에서 이야기한 세개의 어노테이션이며, 실제로 메인 클래스에 `@SpringBootApplication` 을 삭제하고 세개의 어노테이션만 추가해도 결과는 동일하다.
>
> <br>
>
> ### @SpringBootConfiguration
>
> `@Configuration` 기능과 동일하다. 환경설정 빈 클래스를 표현하는 어노테이션이며, Spring Boot에서 사용하기 때문에 이름만 `SpringBootConfiguration`로 변경한 것이다.
>
> <br>
>
> ### @EnableAutoConfiguration
>
> 스프링 부트의 `자동설정` 관련 어노테이션이다.
>
> `자동설정`은 애플리케이션 운용에 필요한 빈들을 초기화하는 기능을 제공한다.
>
> `spring-boot-autoconfigure-x.x.x.RELEASE.jar` 파일에 포함되어 있으며, META-INF 폴더에 `spring.factories` 파일이 있는데, 열어보면 수많은 클래스들이 빈 설정 파일로서 `@Configuration`을 가지고 있다.
>
> 따라서, 메인 클래스를 실행하면 `@EnableAutoConfiguration`에 의해 수많은 `설정`들이 조건에 따라 Bean을 등록한다.
>
> <br>
>
> ### @ComponentScan
>
> 스프링에 의하면 클래스 위에 @Contoller를 설정했다 하더라도 XML 설정 파일에`<context:component-scan>`을 설정하지 않으면 컨테이너가 컨트롤러를 빈으로 등록하지 않는다.
>
> 스프링 부트에서는 컴포넌트 스캔을 자동으로 처리되고 있다.
>
> <br>
>
> @ComponentScan을 설정하면 해당 패키지에 속해있는 @Component 어노테이션을 가진 클래스를 Bean으로 등록한다.
>
> @Configuration, @Repository, @Service, @RestController 등의 어노테이션이 붙은 클래스 객체를 메모리에 올리는 역할을 한다.
>
> 해당 패키지가 아닌 다른 패키지에 클래스를 작성하면 스프링 컨테이너는 해당 클래스를 빈으로 등록하지 않는다.
>
> 만약 다른 패키지의 클래스를 스캔 대상으로 포함시키려면 메인 클래스에 `@ComponentScan` 을 추가하고 스캔하고자 하는 패키지를 지정해야한다.
>
> ```java
> import org.springframework.boot.SpringApplication;
> import org.springframework.boot.autoconfigure.SpringBootApplication;
> import org.springframework.context.annotation.ComponentScan;
> 
> @SpringBootApplication
> @ComponentScan(basePackages= {"com.packex1","com.packex2"})
> public class ProjectNameApplication {
> 	/*
> 	*/
> }
> ```
>
> <br>
>
> ```java
> @Target(ElementType.TYPE)
> @Retention(RetentionPolicy.RUNTIME)
> @Documented
> @Inherited
> @SpringBootConfiguration
> @EnableAutoConfiguration
> @ComponentScan(excludeFilters = { @Filter(type = FilterType.CUSTOM, classes = TypeExcludeFilter.class),
> 		@Filter(type = FilterType.CUSTOM, classes = AutoConfigurationExcludeFilter.class) })
> public @interface SpringBootApplication {
> /*
> */
> }
> 
> ```
>
> 위의 `@ComponentScan`은  `excludeFilters`을 사용하여  `TypeExcludeFilter` 와 `AutoConfigurationExcludeFilter` 를 제외하고 나머지 객체들을 스캔해서 초기화하도록 설정한 것이다.
>
> <br>
>
> <br>

<br>

> 스프링 부트는 스프링 컨테이너를 구동할 때 **두 단계**로 나누어 객체들을 초기화(생성)한다.
>
> 두 단계로 나누는 이유는 애플리케이션을 운영하기 위해서는 두 종류의 Bean이 필요하기 때문이다.
>
> 하나는 `@ComponentScan` 으로 `@Component`가 붙어있는 클래스를 빈으로 등록하고,
>
> `@EnableAutoConfiguration` 으로 미리 정의되어있는 자바 설정파일(@Configuration)을 빈으로 등록하는 역할을 수행한다.

<br>

<br>

<br>

<br>

> by 스프링부트 퀵스타터 (RubyPaper)