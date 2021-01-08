>```java
>import org.springframework.web.bind.annotation.GetMapping;
>import org.springframework.web.bind.annotation.RestController;
>
>@RestController
>public class BoardController {
>	
>	@GetMapping("/hello")
>	public String hello(String name) {
>		return "hello" + name;
>	}
>}
>```
>
>스프링 4부터 `@Controller` 대신 `@RestController` 이 붙는다.
>
>@RestController를 사용하면 REST방식의 응답을 처리하는 컨트롤러를 구현할 수 있다.
>
>@Controller를 사용했다면 hello() 메소드의 리턴타입이 문자열을 사용했을 때, 문자열에 해당하는 view를 만들어야 한다.
>
>반면, @RestController는 문자열이나 VO(자동으로 JSON 형태로 변환)를  브라우저에 그대로 출력되기 때문에 별도로 view 화면을 만들 필요 없다.

<br>

<br>