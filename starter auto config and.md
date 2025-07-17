
스프링 부트로 REST API를 구축해본 경험이 있다면, 현대 자바 개발의 세계에 발을 들인 것입니다. 그러나 단순히 CRUD 애플리케이션을 만드는 것만으로는 충분하지 않습니다. 진정한 개발자는 스프링 부트를 깊이 이해하고, 확장 가능하며 안전하고 고성능의 시스템을 설계할 수 있어야 합니다. 이 가이드는 초보 개발자가 스프링 부트의 고급 기능을 쉽게 이해하고, 실무에서 바로 적용할 수 있도록 새로운 관점에서 정리했습니다. 마치 선배 개발자가 옆에서 친절히 설명해주는 듯한 느낌으로 따라와 보세요!

## 1. 스프링 부트 스타터: 설정을 간편하게 만드는 비밀 무기

`spring-boot-starter-web`과 같은 의존성을 추가해본 경험이 있겠지만, 그 의미를 정확히 아는 개발자는 많지 않습니다.

### 스타터란?

스타터는 관련 라이브러리들을 한 번에 묶어주는 패키지입니다. 예를 들어, `spring-boot-starter-data-jpa`는 Hibernate, Spring Data, JDBC 등 데이터베이스 작업에 필요한 모든 것을 포함합니다:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

### 왜 중요할까?

- 복잡한 의존성 설정을 줄여줍니다.
- 라이브러리 버전 충돌 걱정 없이 호환성을 보장합니다.
- `pom.xml`이나 `build.gradle` 파일을 깔끔하게 유지할 수 있습니다.

### 꿀팁

대규모 프로젝트에서는 팀에서 공통으로 사용할 커스텀 스타터를 만들어보세요. 반복 작업을 줄이는 데 큰 도움이 됩니다!

## 2. 자동 설정(Auto-Configuration): 마법 같은 편리함

스프링 부트는 애플리케이션을 실행할 때 필요한 설정을 자동으로 처리합니다. 이게 어떻게 가능할까요?

### 자동 설정이란?

스프링 부트는 클래스패스와 환경 변수를 분석하여 필요한 빈(Bean)을 자동으로 생성합니다. 예를 들어, `spring-boot-starter-data-jpa`와 H2 데이터베이스가 클래스패스에 있으면 인메모리 데이터베이스를 자동으로 설정해줍니다:

```java
@ConditionalOnClass(DataSource.class)
@ConditionalOnMissingBean(DataSource.class)
@Bean
public DataSource dataSource() {
    // 조건이 맞으면 데이터소스 자동 생성
}
```

### 왜 중요할까?

- 설정 코드를 줄여 개발 속도를 높입니다.
- 필요에 따라 `@Conditional`이나 `@EnableAutoConfiguration`으로 커스터마이징할 수 있습니다.
- 특정 자동 설정을 비활성화하려면 `@SpringBootApplication(exclude = {DataSourceAutoConfiguration.class})`를 사용하세요.

### 주의

자동 설정은 편리하지만, 원리를 이해하지 않으면 디버깅이 어려울 수 있습니다.

## 3. 프로파일(Profiles): 환경별 설정을 깔끔하게

개발 환경과 프로덕션 환경의 설정이 혼합되면 큰 문제가 발생할 수 있습니다. 스프링 프로파일이 이 문제를 해결해줍니다.

### 하는 일

환경별 설정 파일을 분리하여 관리합니다: `application-dev.properties`, `application-prod.properties`

프로파일 활성화 방법:

```bash
-Dspring.profiles.active=dev
```

또는 `application.properties`에 다음과 같이 설정할 수 있습니다:

```properties
spring.profiles.active=prod
```

특정 환경에서만 빈을 생성할 수 있습니다:

```java
@Profile("dev")
@Bean
public DataSource devDataSource() {
    // 개발 환경에서만 사용
}
```

### 왜 중요할까?

- 환경별 설정을 분리하여 실수를 줄입니다.
- 테스트와 배포가 용이해집니다.

## 4. 액추에이터(Actuator): 앱의 건강 상태를 한눈에

프로덕션 환경에서 애플리케이션이 잘 작동하는지 확인하는 방법은 무엇일까요? 스프링 부트 액추에이터가 그 해답입니다.

### 제공 기능

- 건강 체크: `/actuator/health`
- 메트릭: `/actuator/metrics`
- 앱 정보: `/actuator/info`
- 커스텀 엔드포인트 추가 가능

### 보안 설정

기본적으로 엔드포인트가 공개되므로 보안을 위해 설정해야 합니다:

```properties
management.endpoints.web.exposure.include=health,info
management.endpoint.health.show-details=always
```

스프링 시큐리티를 통해 추가적인 보호도 가능합니다.

### 왜 중요할까?

앱의 상태를 실시간으로 모니터링하여 문제를 신속하게 파악할 수 있습니다.

## 5. 배너 커스터마이징: 재미있는 첫인상

스프링 부트 애플리케이션이 시작될 때 콘솔에 출력되는 로고가 마음에 들지 않는다면, 변경할 수 있습니다.

### 하는 일

`src/main/resources`에 `banner.txt` 파일을 만들고 ASCII 아트를 추가합니다:

```text
____                  _     
/ ___| ___   ___   __| | ___ 
| |  _ / _ \ / _ \ / _` |/ _ \
| |_| | (_) | (_) | (_| |  __/
 \____|\___/ \___/ \__,_|\___|
```

`${application.version}` 같은 변수를 사용하여 동적 배너를 만들 수도 있습니다.

### 왜 중요할까?

사소한 부분이지만 팀의 개성을 드러내고, 개발자 경험을 더욱 즐겁게 만들어줍니다.

## 6. 지연 초기화(Lazy Initialization): 시작 속도 UP

기본적으로 스프링 부트는 모든 빈을 초기화하며 시작합니다. 그러나 무거운 빈이 많으면 시작 속도가 느려질 수 있습니다.

### 하는 일

```properties
spring.main.lazy-initialization=true
```

### 왜 중요할까?

- 개발 환경에서 애플리케이션 시작 속도를 빠르게 합니다.
- 메모리 사용량을 줄일 수 있습니다.

### 주의

프로덕션 환경에서는 런타임 에러 가능성이 있으므로 신중하게 사용해야 합니다.

## 7. 외부 설정(Externalized Configuration): 안전한 설정 관리

비밀번호나 DB URL을 코드에 하드코딩하면 보안 사고로 이어질 수 있습니다.

### 방법

환경 변수, YAML/프로퍼티 파일, 명령줄 인자, 클라우드 설정 서버에서 설정을 가져옵니다.

`@Value`로 간단히 주입할 수 있습니다:

```java
@Value("${database.url}")
private String dbUrl;
```

더 깔끔하게 `@ConfigurationProperties`를 사용할 수 있습니다:

```java
@ConfigurationProperties(prefix = "database")
public class DatabaseConfig {
    private String url;
    private String username;
    private String password;
}
```

`.env` 파일도 `spring.config.import=optional:file:.env`로 가져올 수 있습니다.

### 왜 중요할까?

설정을 코드와 분리하여 보안성과 유연성을 높입니다.

## 8. 에러 처리와 커스텀 에러 페이지: API를 깔끔하게

기본 에러 페이지는 HTML로 표시되는데, API에는 적합하지 않습니다.

### 하는 일

`@ControllerAdvice`로 전역 예외 처리를 구현합니다:

```java
@RestControllerAdvice
public class GlobalExceptionHandler {
    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<?> handleNotFound(ResourceNotFoundException ex) {
        return new ResponseEntity<>(new ApiError("Not Found", 404), HttpStatus.NOT_FOUND);
    }
}
```

### 왜 중요할까?

사용자와 개발자 모두에게 친절한 에러 메시지를 제공하여 디버깅과 사용자 경험을 개선합니다.

## 9. 커스텀 자동 설정: 나만의 마법 만들기

스프링 부트처럼 나만의 자동 설정을 만들 수 있습니다.

### 하는 일

```java
@Configuration
@ConditionalOnClass(MyService.class)
public class MyAutoConfig {
    @Bean
    public MyService myService() {
        return new MyService();
    }
}
```

`spring.factories`에 등록합니다:

```text
org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
com.example.autoconfig.MyAutoConfig
```

### 왜 중요할까?

재사용 가능한 모듈이나 프레임워크를 만들 때 강력한 도구가 됩니다.

## 10. 모듈화된 설정(@Import): 깔끔한 코드 구조

설정을 한 파일에 몰아넣으면 복잡해질 수 있습니다. `@Import`로 나누어 관리하세요:

```java
@Configuration
@Import({DbConfig.class, SecurityConfig.class})
public class MainConfig {
}
```

### 왜 중요할까?

코드를 모듈화하여 유지보수와 테스트를 쉽게 할 수 있습니다.

## 보너스: 테스트 잘하기

- `@SpringBootTest`로 통합 테스트를 수행합니다.
- `@DataJpaTest`, `@WebMvcTest`로 특정 기능만 테스트합니다.
- `@MockBean`으로 외부 API를 모킹합니다.
- `TestRestTemplate`으로 실제 HTTP 엔드포인트를 테스트합니다.

### 왜 중요할까?

테스트는 애플리케이션이 커질수록 안정성을 보장합니다.

## 마무리: 스프링 부트를 진정으로 마스터하자!

스프링 부트는 단순한 도구가 아니라 강력한 생태계입니다. 이 고급 개념들을 익히면:

- 더 견고하고 유연한 애플리케이션을 만들 수 있습니다.
- 디버깅과 성능 최적화가 쉬워집니다.
[1] https://velog.io/@lsm4556/%EC%8A%A4%ED%94%84%EB%A7%81-%EB%B6%80%ED%8A%B8-%ED%95%B5%EC%8B%AC%EA%B0%80%EC%9D%B4%EB%93%9C-1-3%EC%9E%A5-%EC%A0%95%EB%A6%AC
[2] https://www.geeksforgeeks.org/springboot/best-way-to-master-spring-boot-a-complete-roadmap/
[3] https://www.sivalabs.in/mastering-spring-boot-in-5-stages/
[4] https://dev.to/weder96/spring-boot-everything-you-need-to-know-and-what-nobody-told-you-o4j
[5] https://velog.io/@ameri-kano/%EC%8A%A4%ED%94%84%EB%A7%81-%EB%B6%80%ED%8A%B8-%ED%95%B5%EC%8B%AC-%EA%B0%80%EC%9D%B4%EB%93%9C-%EC%A0%95%EB%A6%AC-4%EC%A3%BC%EC%B0%A8
[6] https://webreference.com/java/spring/spring-boot/
[7] https://www.geeksforgeeks.org/advance-java/spring-boot/
[8] https://do5do.tistory.com/17
[9] https://reminisce057.tistory.com/41
[10] https://spring.io/guides/gs/spring-boot
[11] https://docs.spring.io/spring-boot/docs/0.0.9.BUILD-SNAPSHOT/reference/htmlsingle/
[12] https://docs.spring.io/spring-boot/documentation.html
[13] https://ezaouibiyassin.medium.com/spring-boot-essentials-your-comprehensive-guide-to-core-concepts-a1594c4d721d
[14] https://reminisce057.tistory.com/36
[15] https://master-spring-ter.medium.com/spring-boot-ai-a-comprehensive-guide-to-intelligent-java-development-c5bdf7116a50
[16] https://devkwonsehoon.github.io/posts/spring-guide-4/
[17] https://do5do.tistory.com/18
[18] https://spring.io/projects/spring-boot
[19] https://www.marcobehler.com/guides/spring-boot-autoconfiguration
[20] https://hyungjun-950912.tistory.com/113
[21] https://medium.com/@zaghdoudi.mohamed/spring-boot-design-patterns-a-comprehensive-guide-116ccba38054
[22] https://blog.naver.com/rock1192/223149758925
[23] https://freedeveloper.tistory.com/111
[24] https://www.upgrad.com/blog/spring-boot-annotations/
[25] https://velog.io/@ameri-kano/%EC%8A%A4%ED%94%84%EB%A7%81-%EB%B6%80%ED%8A%B8-%ED%95%B5%EC%8B%AC-%EA%B0%80%EC%9D%B4%EB%93%9C-%EC%A0%95%EB%A6%AC-3%EC%A3%BC%EC%B0%A8
[26] https://blog.yevgnenll.me/posts/spring-configuration-properties-fetch-application-properties
[27] https://shanepark.tistory.com/341
[28] https://innovation123.tistory.com/169
[29] https://kok202.tistory.com/129
[30] https://hoding-cloud.tistory.com/3
[31] http://honeymon.io/tech/2019/06/17/spring-boot-2-start.html
[32] https://www.reddit.com/r/WGU_CompSci/comments/1ce4qdt/d287_recommendations_to_learn_spring_boot/
[33] https://bump.sh/blog/generating-openapi-docs-for-java-with-spring-boot/
