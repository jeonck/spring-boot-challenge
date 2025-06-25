## Spring Boot JPA 활용 컨벤션과 코드

Spring Boot에서 JPA를 효과적으로 활용하기 위한 컨벤션과 코드 작성 방법은 프로젝트 구조, 엔티티 설계, Repository/Service/Controller 계층 분리, DTO 사용, 트랜잭션 처리, 네이밍 전략 등 여러 측면에서 정리할 수 있습니다.

### **1. 프로젝트 구조 및 의존성**

- 일반적으로 다음과 같은 패키지 구조를 권장합니다:
  - `domain` (엔티티), `repository`, `service`, `controller`, `dto`, `converter` 등.
- Maven/Gradle에 `spring-boot-starter-data-jpa`와 DB 드라이버 의존성을 추가합니다.

```groovy
implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
runtimeOnly 'com.h2database:h2'
```

### **2. 엔티티 설계 컨벤션**

- 엔티티 클래스에는 가급적 Setter를 사용하지 않습니다. 생성자, 빌더 패턴, 변경 메서드로 값 설정을 권장합니다.
- 모든 연관관계는 `LAZY` 로딩을 기본으로 설정합니다.
- 컬렉션(List 등)은 필드에서 바로 초기화합니다. `private List<Item> items = new ArrayList<>();`
- 테이블/컬럼 네이밍은 카멜케이스 → 언더스코어, 대문자 → 소문자로 자동 매핑됩니다. 필요시 명시적으로 `@Table`, `@Column` 사용합니다.
- 엔티티에는 `@Entity`, PK에는 `@Id`, 자동 생성 전략에는 `@GeneratedValue`를 사용합니다.

```java
@Entity
@NoArgsConstructor(access = AccessLevel.PROTECTED)
public class Product {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(nullable = false)
    private String name;
}
```

### **3. Repository 계층**

- `JpaRepository<T, ID>`를 상속받아 인터페이스만 생성하면 자동으로 빈 등록 및 CRUD 메서드 제공됩니다.
- Repository 인터페이스에 `@Repository`를 붙이지 않습니다. Spring이 자동 감지합니다.
- 커스텀 쿼리는 `@Query` 또는 Query Method로 작성합니다.

```java
public interface ProductRepository extends JpaRepository<Product, Long> {
    List<Product> findByName(String name);
}
```

### **4. DTO 활용 및 계층 분리**

- 엔티티를 직접 API 응답으로 반환하지 않고, DTO로 변환하여 반환합니다.
  - 엔티티 변경이 API에 영향을 주지 않게 하고, 보안/유연성을 확보합니다.
- DTO 변환은 Service 계층에서 처리합니다.

```java
public record ProductDTO(Long id, String name) {}

@Service
public class ProductService {
    private final ProductRepository productRepository;

    public ProductDTO getProductById(Long id) {
        Product product = productRepository.findById(id)
            .orElseThrow(() -> new RuntimeException("Not found"));
        return new ProductDTO(product.getId(), product.getName());
    }
}
```

### **5. 트랜잭션 처리**

- JPA를 통한 모든 데이터 변경은 반드시 트랜잭션 안에서 실행해야 합니다.
- Service 계층에 `@Transactional`을 선언합니다.

```java
@Service
@Transactional
public class ProductService { ... }
```

### **6. 성능 및 유지보수 Best Practices**

- `FetchType.LAZY`, `@EntityGraph`로 N+1 문제 예방합니다.
- Pagination 처리로 대용량 데이터 대응합니다.
- HikariCP 등 커넥션 풀 사용 (Spring Boot 기본값).
- SQL 로그 활성화로 쿼리 모니터링합니다.
- 대량 연관관계에 `CascadeType.REMOVE` 사용 자제합니다.
- `@Version`으로 낙관적 락킹 적용합니다.

### **7. 네이밍 전략 및 설정**

- 논리명/물리명 전략은 Spring Boot 기본값을 따르되, 필요시 `spring.jpa.hibernate.naming.*` 속성으로 커스터마이즈합니다.

```yaml
spring:
  jpa:
    hibernate:
      naming:
        implicit-strategy: org.springframework.boot.orm.jpa.hibernate.SpringImplicitNamingStrategy
```

## **실전 코드 예시**

```java
// Entity
@Entity
@NoArgsConstructor(access = AccessLevel.PROTECTED)
public class User {
    @Id @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    @Column(nullable = false)
    private String name;
}

// Repository
public interface UserRepository extends JpaRepository<User, Long> {}

// DTO
public record UserDTO(Long id, String name) {}

// Service
@Service
@Transactional
public class UserService {
    private final UserRepository userRepository;
    public UserDTO getUserById(Long id) {
        User user = userRepository.findById(id)
            .orElseThrow(() -> new RuntimeException("User not found"));
        return new UserDTO(user.getId(), user.getName());
    }
}

// Controller
@RestController
@RequestMapping("/api/users")
public class UserController {
    private final UserService userService;
    @GetMapping("/{id}")
    public ResponseEntity<UserDTO> getUser(@PathVariable Long id) {
        return ResponseEntity.ok(userService.getUserById(id));
    }
}
```

---

## **요약**

- **DTO 변환, 계층 분리, 트랜잭션 처리, 네이밍 규칙, LAZY 로딩, 커넥션 풀, SQL 로그, Repository 자동 감지** 등은 Spring Boot JPA 활용의 대표적인 컨벤션입니다.
- 실무에서는 엔티티 직접 노출을 피하고, DTO와 계층 분리를 통해 유지보수성과 확장성을 확보하는 것이 중요합니다.
[1] https://velog.io/@christer10/UMC-serverSpring-boot-7주차-spring-개발-환경-설정-JPA-설계
[2] https://velog.io/@hj_/JPA-활용-1편-1.-프로젝트-설정-및-도메인-설계
[3] https://kdohyeon.tistory.com/69
[4] https://aspring.tistory.com/entry/스프링부트-실전-스프링-부트와-JPA-활용1-2-5-엔티티-설계시-주의점
[5] https://wooj-coding-fordeveloper.tistory.com/76
[6] https://www.linkedin.com/pulse/mastering-spring-data-jpa-essential-best-practices-omar-ismail-mkgfe
[7] https://www.javaguides.net/2025/02/top-10-best-practices-for-spring-data.html
[8] https://blog.naver.com/adamdoha/222078847621
[9] https://sohee-dev.tistory.com/152
[10] https://twbf.tistory.com/33
