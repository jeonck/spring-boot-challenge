스프링 부트로 기본 앱을 만들어봤다면, 이제 한 단계 업그레이드할 시간입니다! 이번 가이드는 스프링 부트의 고급 기능을 초보자도 흥미롭게 이해할 수 있도록, 실무 사례를 곁들여 쉽게 풀어 설명합니다. 마치 동료 개발자가 옆에서 재미있는 이야기를 들려주듯이, 기업 수준의 앱을 만들기 위한 핵심 기술들을 배워보세요. 준비됐나요? 🚀

## 1. @Async로 비동기 처리: 사용자 기다리게 하지 마세요!

사용자가 회원가입을 했을 때 환영 이메일을 보내야 한다고 상상해보세요. 이메일 전송이 느리다면 사용자가 기다리는 동안 화면이 멈춰버릴 거예요. 스프링 부트의 @Async로 이 문제를 깔끔하게 해결할 수 있습니다.

### 어떻게 하나요?

- **비동기 기능 활성화**: `@EnableAsync`를 사용하여 비동기 기능을 활성화합니다.

```java
@EnableAsync
@Configuration
public class AsyncConfig {}
```

- **이메일 전송 메서드에 @Async 추가**:

```java
@Service
public class EmailService {
    @Async
    public void sendWelcomeEmail(String to) {
        System.out.println("Sending email to " + to);
    }
}
```

- **호출은 평소처럼**:

```java
emailService.sendWelcomeEmail("user@example.com");
```

### 왜 멋질까?

- 사용자는 기다릴 필요 없이 바로 다음 작업을 할 수 있어요.
- 서버 성능을 최적화해 빠른 응답을 제공합니다.

### 주의점:

- @Async 메서드는 void, Future<T>, 또는 CompletableFuture<T>를 반환해야 합니다.
- 같은 빈 안에서 호출하면 안 됩니다(스프링 프록시 한계).
- 스레드 풀이 필요하니 TaskExecutor로 설정하세요.

## 2. 조건부 빈(@Conditional): 환경에 따라 똑똑하게 동작

개발 환경에선 Swagger로 API 문서를 보고 싶지만, 프로덕션에선 보안 때문에 꺼야 한다면? 조건부 빈으로 깔끔하게 해결할 수 있습니다.

### 어떻게 하나요?

- **@ConditionalOnProperty로 조건 설정**:

```java
@Configuration
@ConditionalOnProperty(name = "swagger.enabled", havingValue = "true")
public class SwaggerConfig {
    // Swagger 설정
}
```

- **개발 환경 설정(application-dev.properties)**:

```properties
swagger.enabled=true
```

- **프로덕션 설정(application-prod.properties)**:

```properties
swagger.enabled=false
```

### 왜 멋질까?

- if 문 없이도 환경별로 빈을 동적으로 등록 가능.
- 코드가 간결하고 유지보수 쉬워집니다.

## 3. 내장 서버 바꾸기: Tomcat 말고 Jetty나 Undertow 어때요?

스프링 부트는 기본적으로 Tomcat을 사용하지만, 다른 서버로 바꾸면 앱 성능을 더 끌어올릴 수 있습니다.

### 왜 바꿀까?

- **Jetty**: 가볍고, 낮은 지연 시간이 필요한 앱에 딱!
- **Undertow**: 비동기 처리로 마이크로서비스에 최적.

### Jetty로 전환:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-jetty</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-tomcat</artifactId>
    <scope>provided</scope>
</dependency>
```

### 왜 멋질까?

앱의 특성에 맞는 서버를 골라 성능과 효율성을 극대화할 수 있습니다.

## 4. 스프링 시큐리티로 보안 강화: JWT로 안전한 API

보안은 선택이 아니라 필수! 스프링 시큐리티와 JWT로 강력한 인증 시스템을 만들어보세요.

### JWT 인증 흐름:

1. 사용자가 로그인하면 JWT 토큰 발급.
2. 요청마다 Authorization 헤더에 토큰을 포함.
3. 필터가 토큰을 검증하고 사용자 인증 정보를 설정.

### JWT 필터 예시:

```java
public class JwtTokenFilter extends OncePerRequestFilter {
    protected void doFilterInternal(...) {
        String token = resolveToken(request);
        if (isValid(token)) {
            Authentication auth = getAuthentication(token);
            SecurityContextHolder.getContext().setAuthentication(auth);
        }
        filterChain.doFilter(request, response);
    }
}
```

### 왜 멋질까?

간단한 설정으로 안전하고 확장 가능한 인증 시스템을 구축할 수 있어요.

## 5. @Retryable로 앱의 회복력 높이기

외부 API 호출이 실패하면? 다시 시도해보세요! @Retryable로 쉽게 재시도 로직을 추가할 수 있습니다.

### 하는 법:

- **재시도 활성화**:

```java
@EnableRetry
@SpringBootApplication
public class App {}
```

- **재시도 로직 추가**:

```java
@Service
public class PaymentService {
    @Retryable(value = {RemoteServiceException.class}, maxAttempts = 3, backoff = @Backoff(delay = 2000))
    public String callExternalPaymentGateway() {
        // 외부 API 호출
    }
    
    @Recover
    public String recover(RemoteServiceException e) {
        return "결제 실패 시 기본 응답";
    }
}
```

### 왜 멋질까?

실패해도 자동으로 재시도해 앱의 안정성을 높입니다.

## 6. Testcontainers: 진짜 환경에서 테스트하기

모킹에 지쳤나요? Testcontainers로 실제 데이터베이스나 서비스를 테스트에 활용하세요.

### 예시: PostgreSQL 테스트

```java
@Container
static PostgreSQLContainer<?> postgres = new PostgreSQLContainer<>("postgres:14")
    .withDatabaseName("test")
    .withUsername("test")
    .withPassword("test");
```

### 스프링 부트 설정:

```properties
spring.datasource.url=jdbc:tc:postgresql:14:///test
```

### 왜 멋질까?

Kafka, Redis 같은 의존성을 실제로 띄워 테스트하니 더 믿을 수 있는 결과를 얻습니다.

## 7. @Scheduled로 자동화된 작업 만들기

매시간 보고서를 생성해야 한다면? @Scheduled로 간단히 스케줄링하세요.

### 하는 법:

- **스케줄링 활성화**:

```java
@EnableScheduling
@Configuration
public class SchedulerConfig {}
```

- **작업 정의**:

```java
@Component
public class ReportJob {
    @Scheduled(cron = "0 0 * * * *") // 매시간 실행
    public void generateHourlyReport() {
        System.out.println("보고서 생성 중...");
    }
}
```

### 왜 멋질까?

복잡한 크론 잡 설정 없이도 주기적 작업을 쉽게 추가할 수 있어요.

## 8. 우아한 종료(Graceful Shutdown): 데이터 손실 없이 앱 종료

앱이 종료될 때 데이터 손실 걱정 없도록, 스프링 부트 2.3+의 우아한 종료 기능을 사용하세요.

### 설정:

```properties
server.shutdown=graceful
spring.lifecycle.timeout-per-shutdown-phase=30s
```

### 정리 작업:

```java
@Component
public class CleanupService implements DisposableBean {
    @Override
    public void destroy() {
        // DB 연결 종료, 로그 전송 등
    }
}
```

### 왜 멋질까?

앱이 깔끔하게 종료되어 데이터 무결성을 지킬 수 있습니다.

## 9. @RestClientTest로 외부 API 테스트 쉽게

외부 API 호출을 테스트할 때 모킹이 필요하다면, @RestClientTest가 최고입니다.

### 예시:

```java
@RunWith(SpringRunner.class)
@RestClientTest(MyRestClient.class)
public class MyRestClientTest {
    @Autowired
    private MockRestServiceServer server;
    @Autowired
    private MyRestClient client;

    @Test
    public void shouldReturnResponse() {
        this.server.expect(requestTo("/external/api"))
            .andRespond(withSuccess("mock response", MediaType.TEXT_PLAIN));
        String result = client.callApi();
        assertEquals("mock response", result);
    }
}
```

### 왜 멋질까?

실제 외부 API 없이도 안전하고 빠르게 테스트 가능.

## 10. DevTools로 개발 속도 높이기

개발 중 코드 수정 후 매번 앱을 재시작하는 건 귀찮죠. DevTools가 해결사입니다.

### 설정:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <scope>runtime</scope>
</dependency>
```

### 기능:

- 코드 변경 시 자동 재시작.
- LiveReload로 브라우저 새로고침 자동화.
- 템플릿 캐싱 비활성화로 즉각적인 피드백.

### 왜 멋질까?

개발 생산성을 엄청나게 높여줍니다!

## 마무리: 스프링 부트로 진짜 프로 되기

이제 당신은 스프링 부트를 단순히 사용하는 수준을 넘어, 프로급 앱을 설계할 수 있는 개발자가 됐습니다. 비동기 처리, 조건부 빈, 테스트 컨테이너, 스케줄링, 보안 등 이 모든 기능은 단순한 "옵션"이 아니라, 안정적이고 확장 가능한 시스템을 만드는 핵심입니다.

### 당신이 얻은 것:

- 사용자 경험을 개선하는 비동기 처리.
- 환경별 유연한 설정 관리.
- 실제 의존성을 사용한 믿음직한 테스트.
- 안전한 보안과 자동화된 작업.

이제 이 기술들로 멋진 앱을 만들어 보세요! 🚀
[1] https://gdngy.tistory.com/116
[2] https://medium.com/@ismoil.793/mastering-enterprise-applications-with-java-spring-boot-9fbdf040790f
[3] https://product.kyobobook.co.kr/detail/S000213996094
[4] https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-%ED%95%B5%EC%8B%AC%EC%9B%90%EB%A6%AC-%ED%99%9C%EC%9A%A9?srsltid=AfmBOooWzUlGBEzZFHby2KeM3a9UpuSzeVtYwFX80RU3dsRGqtOihaRF
[5] https://thecodest.co/ko/blog/%EC%8A%A4%ED%94%84%EB%A7%81-%EB%B6%80%ED%8A%B8-%EA%B0%9C%EB%B0%9C%EC%9E%90-%EA%B3%A0%EC%9A%A9/
[6] https://www.geeksforgeeks.org/springboot/best-way-to-master-spring-boot-a-complete-roadmap/
[7] https://gdngy.tistory.com/105
[8] https://levelup.gitconnected.com/mastering-advanced-spring-boot-2025-a-deep-dive-into-modern-development-practices-29368b30324a
[9] https://jyami.tistory.com/12
[10] https://www.reddit.com/r/SpringBoot/comments/1aq3dp5/where_can_i_find_tutorials_for_complex_and/
[11] https://notavoid.tistory.com/101
[12] https://dev.to/tpointtechblog/spring-framework-tutorial-2025-build-enterprise-grade-java-applications-190b
[13] https://codefarm0.medium.com/advanced-spring-boot-concepts-every-java-developer-should-master-45cd90ef3e98
[14] https://www.hungrycoders.com/blog/spring-boot-roadmap-from-basics-to-advanced
[15] https://www.learningtree.com/courses/enterprise-java-applications-with-spring-training/
[16] https://apidog.com/kr/blog/api-development-frameworks-2/
[17] https://blog.naver.com/oraclejava31/221338751541?viewType=pc
[18] https://www.reddit.com/r/learnjava/comments/1jxhq1h/get_handson_coding_experience_on_an_enterprise/
