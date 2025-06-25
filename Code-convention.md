Spring Boot 프로젝트에서 널리 통용되는 코드 컨벤션은 명확성, 유지보수성, 가독성을 목표로 하며, Java 및 Spring 커뮤니티의 모범 사례를 따릅니다. 아래는 Spring Boot 프로젝트에서 일반적으로 사용되는 코드 컨벤션의 주요 요소들입니다.

1. **패키지 구조**
   - **계층적 구조**:
     - 패키지는 기능 또는 모듈별로 분리: `com.example.myapp.domain`, `com.example.myapp.service`, `com.example.myapp.controller` 등.
     - 예:
       ```
       com.example.myapp
       ├── config
       ├── controller
       ├── service
       ├── repository
       ├── domain
       │   ├── entity
       │   ├── dto
       │   └── vo
       └── exception
       ```
   - **명명 규칙**:
     - 패키지 이름은 소문자로, 도메인 기반으로 작성 (예: `com.company.project`).
     - 모듈명은 단수형 사용 (예: `controller`, `service`).

2. **클래스 및 파일 명명**
   - **클래스 이름**:
     - PascalCase 사용 (예: `UserService`, `OrderController`).
     - 역할에 따라 접미사 사용:
       - Controller: `UserController`
       - Service: `UserService`
       - Repository: `UserRepository`
       - Entity: `User`, `Order`
       - DTO: `UserRequest`, `UserResponse`
   - **파일명**:
     - 클래스명과 동일해야 함.
     - 예: `UserService.java`

3. **메서드 명명**
   - CamelCase 사용: 동사로 시작, 의도를 명확히 (예: `findById`, `saveUser`, `updateOrderStatus`).
   - **명명 패턴**:
     - 조회: `find`, `get` (예: `findByUsername`, `getOrderById`).
     - 저장: `save`, `create` (예: `saveUser`).
     - 수정: `update` (예: `updateUserProfile`).
     - 삭제: `delete`, `remove` (예: `deleteById`).
   - **명확성 우선**: `getUserById`보다 `findUserById` 선호.

4. **변수 및 상수**
   - **변수**:
     - CamelCase 사용 (예: `userId`, `orderStatus`).
     - 의미 있는 이름 사용, 축약은 최소화 (예: `user` 대신 `currentUser`).
   - **상수**:
     - 대문자와 언더스코어(_) 사용 (예: `MAX_RETRY_COUNT`, `DEFAULT_TIMEOUT`).
     - `static final`로 선언.

5. **코드 포맷팅**
   - **들여쓰기**: 4칸 공백 (탭 대신 공백 사용).
   - **줄 길이**: 최대 120자 권장.
   - **중괄호**:
     - 메서드와 클래스 선언에서 중괄호는 같은 줄에 (K&R 스타일):
       ```java
       public class UserService {
           public void saveUser() {
               // 코드
           }
       }
       ```
   - **공백**:
     - 연산자 주변에 공백 (예: `a + b`, `if (condition)`).
     - 메서드 파라미터 사이에 공백 없음 (예: `findUserById(Long id, String name)`).

6. **주석**
   - **Javadoc**:
     - Public 메서드와 클래스에 Javadoc 작성:
       ```java
       /**
        * 사용자 정보를 ID로 조회한다.
        * @param id 사용자 ID
        * @return User 사용자 객체
        * @throws UserNotFoundException 사용자가 없을 경우
        */
       public User findUserById(Long id) { ... }
       ```
   - **인라인 주석**:
     - 복잡한 로직에만 간결히 작성.
     - 예: `// 복잡한 계산을 위해 임시 변수 사용.`

7. **Spring Boot 특화 규칙**
   - **컨트롤러**:
     - `@RestController` 사용 시, `@ResponseBody` 생략.
     - 메서드명은 HTTP 동사와 일치 (예: `getUser`, `postOrder`).
   - **서비스**:
     - 비즈니스 로직은 서비스 계층에 집중.
     - `@Service` 어노테이션 사용.
   - **리포지토리**:
     - JPA 사용 시, 메서드명은 Spring Data JPA 규칙 준수 (예: `findByUsernameAndStatus`).
     - `@Repository`는 Spring Data JPA에서 생략 가능.
   - **DTO**:
     - 요청/응답 DTO 분리 (예: `UserRequest`, `UserResponse`).
     - 직렬화 가능한 클래스 사용 (implements Serializable 권장).
   - **예외 처리**:
     - `@ControllerAdvice`로 전역 예외 처리.
     - 커스텀 예외 클래스 사용 (예: `UserNotFoundException`).

8. **의존성 주입**
   - 생성자 주입 선호:
     ```java
     @Service
     public class UserService {
         private final UserRepository userRepository;

         public UserService(UserRepository userRepository) {
             this.userRepository = userRepository;
         }
     }
     ```
   - `@Autowired`는 최소화, 생성자 주입으로 불변성 보장.

9. **로깅**
   - SLF4J 사용:
     - `org.slf4j.Logger`와 `LoggerFactory` 사용.
     - 예:
       ```java
       private static final Logger log = LoggerFactory.getLogger(UserService.class);
       log.info("User saved: {}", userId);
       ```
   - 로그 레벨 적절히 사용: `debug`, `info`, `warn`, `error`.

10. **테스트 코드**
    - 테스트 클래스:
      - `@SpringBootTest` 또는 `@WebMvcTest`, `@DataJpaTest` 사용.
      - 클래스명은 클래스명 + Test (예: `UserServiceTest`).
    - 메서드명:
      - `should_동작_상황` 패턴 (예: `shouldSaveUserWhenValidInput`).
    - Mockito와 JUnit 적극 활용.

11. **기타 권장 사항**
    - 코드 정적 분석: Checkstyle, SonarQube 등으로 코드 품질 관리.
    - Lombok 사용:
      - `@Getter`, `@Setter`, `@Builder` 등으로 보일러플레이트 코드 감소.
      - 과도한 사용 자제 (예: `@Data` 대신 명시적 어노테이션).
    - 버전 관리: `.gitignore`에 빌드 파일, IDE 설정 파일 추가.

이 컨벤션은 팀마다 약간 다를 수 있으므로, 팀 내부에서 합의된 스타일 가이드를 따르는 것이 중요합니다.
[1] https://medium.com/@sharmapraveen91/clean-code-coding-guidelines-java-spring-boot-api-36a88e588008
[2] https://chaewsscode.tistory.com/224
[3] https://docs.spring.io/spring-boot/reference/using/structuring-your-code.html
[4] https://itchipmunk.tistory.com/576
[5] https://docs.spring.io/spring-boot/docs/2.1.3.RELEASE/reference/html/using-boot-structuring-your-code.html
[6] https://www.inflearn.com/blogs/7143?srsltid=AfmBOooxbheyfsiOn_0OnOmOvF_lYSYzIZkKK8eZBOoWQQpo6KDEAws7
[7] https://yeongchan1228.tistory.com/129
[8] https://github.com/arsy786/springboot-best-practices
[9] https://medium.com/javarevisited/how-to-follow-good-coding-standards-in-spring-boot-abada3e7ce64
[10] https://stackoverflow.com/questions/25105409/most-used-java-code-convention-style-guide
[11] https://jobc.tistory.com/212
[12] https://stackoverflow.com/questions/59425651/spring-boot-configuration-conventions
[13] https://jacobhboy66.tistory.com/41
[14] https://www.geeksforgeeks.org/java/spring-boot-code-structure/
[15] https://github.com/spring-projects/spring-framework/wiki/Code-Style
[16] https://velog.io/@jifrozen/Checkmate-intellij-spring-boot-%ED%98%91%EC%97%85%EC%8B%9C-%EA%B0%9C%EB%B0%9C-%ED%99%98%EA%B2%BD-%ED%86%B5%EC%9D%BC-%ED%95%98%EA%B8%B0-%EC%BD%94%EB%93%9C-%EC%BB%A8%EB%B2%A4%EC%85%98-swagger-API-%EB%AC%B8%EC%84%9C%ED%99%94-1
[17] https://techdocs.broadcom.com/us/en/vmware-tanzu/standalone-components/tanzu-application-platform/1-12/tap/spring-boot-conventions-reference-CONVENTIONS.html
[18] https://docs.spring.io/spring-boot/reference/using/index.html
[19] https://www.reddit.com/r/java/comments/sos5x1/spring_boot_microservices_coding_style_guidelines/
[20] https://www.codewalnut.com/insights/spring-boot-best-practices-for-scalable-applications
[21] https://velog.io/@kgy30002/Intellij-springboot%EC%BD%94%EB%93%9C-%EC%BB%A8%EB%B2%A4%EC%85%98-%EC%84%A4%EC%A0%95%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95
[22] https://mangkyu.tistory.com/215
[23] https://wordbe.tistory.com/227
[24] https://www.reddit.com/r/SpringBoot/comments/1buv6hn/what_are_the_best_practices_in_spring_boot/
[25] https://digma.ai/10-spring-boot-performance-best-practices/
[26] https://bhawana-gaur.medium.com/best-practices-for-developing-and-maintaining-spring-boot-applications-d96bb1816da6
[27] https://stackoverflow.com/questions/62107681/spring-boot-enforce-best-practices
[28] https://last9.io/blog/a-guide-to-spring-boot-logging/
