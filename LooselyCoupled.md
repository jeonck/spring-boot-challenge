스프링부트 메인 애플리케이션이 **컨트롤러 모듈을 호출하는 맥락**은 다음과 같이 설명할 수 있습니다:

- **메인 애플리케이션 클래스**(보통 `@SpringBootApplication`로 선언)는 스프링 부트 프로젝트의 진입점이며, 내부적으로 `SpringApplication.run()`을 실행합니다. 이 과정에서 **스프링 IoC 컨테이너**가 초기화되어 모든 `@Component`, `@Service`, `@Repository`, `@Controller` 등 어노테이션이 붙은 클래스를 **스캔**하고 빈(bean)으로 등록합니다[1][5].
  
- 이때, 별도로 작성된 컨트롤러(`@RestController` 또는 `@Controller`로 선언된 클래스)는 자동으로 **스프링 컨테이너의 빈으로 등록**되어, HTTP 요청에 응답할 준비가 됩니다[1][5][8].

- **컨트롤러를 직접 호출하는 코드가 메인 애플리케이션에 명시적으로 존재하는 것이 아니라**, 스프링 프레임워크가 내장 톰캣 서버와 함께 URL 요청이 들어오면 해당 URL에 매핑된 컨트롤러 메서드를 실행해 응답을 반환합니다. 이 모든 과정은 스프링의 **디스패처 서블릿(DispatcherServlet)**과 **IoC 컨테이너의 의존성 주입**이 자동으로 처리합니다[4][7].

- 예를 들어, `/hello`라는 URL로 HTTP GET 요청이 오면, 스프링은 내부적으로 요청을 분석하고, 등록된 `HelloController`의 해당 메서드를 찾아 실행합니다. 메인 애플리케이션 클래스는 단지 모든 컴포넌트를 스캔하고 관리하며, 실제 호출 흐름은 프레임워크가 처리하게 되는 구조입니다[5][7].

즉, 메인 애플리케이션이 **직접 컨트롤러 모듈을 호출하는 것이 아니라,**
- **컨트롤러를 빈으로 등록**하고,
- **HTTP 요청이 올 때** 프레임워크가 자동으로 해당 메서드를 호출해서 처리가 이어집니다[1][5].

이 구조가 **스프링부트의 모듈화와 느슨한 결합**의 핵심입니다.
[1] https://secretartbook.tistory.com/29
[2] https://velog.io/@sloools/Spring-boot-스프링-부트-애플리케이션-실행
[3] https://devalice.tistory.com/41
[4] https://joyful-class-maker.tistory.com/88
[5] https://soohyun6879.tistory.com/34
[6] http://sgc109.github.io/2020/07/09/spring-running-startup-logic/
[7] https://shallow-learning.tistory.com/entry/스프링부트-4-Spring-MVC-Controller-만들기
[8] https://goddaehee.tistory.com/203
[9] https://lifere.tistory.com/entry/Spring-Boot-프로젝트-및-Controller-생성
