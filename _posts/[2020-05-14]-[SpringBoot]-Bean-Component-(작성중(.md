title: "[SpringBoot] Bean vs Component - 작성중"
tag: "SpringBoot"



## 어노테이션 ( Annotation, @ )

프로그램이 거대해 짐에 따라 `XML` 을 이용하여 `IOC Container`를 설정하는 것이 점점 어려워졌고, 때문에 `Annotation(@)` 이란 것이 등장했다. `어노테이션` 코드에 메타데이터를 작성하여 직관적인 코딩이 가능하게 만들어주며 이에 따라 생산성이 증대되는 장점을 가지고 있다.

<br>

<br>

## @Configuration

`@Configuration` 은 스프링 `IOC Container` 에게 해당 클래스를 Bean 구성 Class 임을 알려주는 것이다.

<br>

## @Bean vs @Component

`@Bean` 어노테이션과 `@Component` 어노테이션 둘다 `Spring IOC Container` 에 Bean을 등록하도록 하는 메타데이터를 기입하는 어노테이션이다.

왜 두개나 만들어 놓았을 까? 바로 `둘의 용도가 다르기 때문!`

#### @Bean

`@Bean` 어노테이션의 경우 개발자가 직접 제어가 불가능한 외부 라이브러리 등을 `Bean`으로 등록하기 위해 사용된다.

```java
@Configuration
public class CommonBean {
	@Bean
	public ModelMapper modelMapper() {
		return new ModelMapper();
	}
}
```



