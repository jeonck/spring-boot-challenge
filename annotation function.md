스프링부트에서 어노테이션은 다양한 기능을 수행하며, 이를 통해 애플리케이션의 설정, 컴포넌트 관리, 요청 처리, 의존성 주입, 트랜잭션 관리 등을 간소화합니다. 아래에서는 이러한 기능을 역할별로 카테고리화하고, 각 카테고리의 주요 어노테이션과 예시를 포함하여 설명하겠습니다.

## **1. 설정(Configuration) 관련 어노테이션**

### **@Configuration**
- **기능**: 스프링 애플리케이션의 설정 클래스를 정의합니다. 이 클래스 내에서 `@Bean` 어노테이션을 사용하여 빈을 등록할 수 있습니다.

```java
@Configuration
public class AppConfig {
    @Bean
    public MyService myService() {
        return new MyService();
    }
}
```

### **@SpringBootApplication**
- **기능**: 스프링부트 애플리케이션의 진입점을 정의하며, `@Configuration`, `@EnableAutoConfiguration`, `@ComponentScan`을 포함합니다.

```java
@SpringBootApplication
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```

## **2. 컴포넌트 관리(Component Management) 관련 어노테이션**

### **@Component**
- **기능**: 스프링이 관리하는 빈으로 등록할 클래스를 나타냅니다.

```java
@Component
public class MyComponent {
    // 비즈니스 로직
}
```

### **@Service**
- **기능**: 비즈니스 로직을 포함하는 서비스 클래스를 정의합니다.

```java
@Service
public class UserService {
    public String getUser() {
        return "Hello, User!";
    }
}
```

### **@Repository**
- **기능**: 데이터 접근 계층을 나타내며, 데이터베이스와의 상호작용을 처리합니다.

```java
@Repository
public class UserRepository {
    // 데이터베이스 접근 로직
}
```

### **@Controller**
- **기능**: 웹 요청을 처리하는 컨트롤러 클래스를 정의합니다.

```java
@Controller
public class UserController {
    @GetMapping("/users")
    public String getUsers(Model model) {
        // 사용자 목록을 모델에 추가
        return "userList";
    }
}
```

## **3. 요청 처리(Request Handling) 관련 어노테이션**

### **@RequestMapping**
- **기능**: HTTP 요청을 특정 메서드에 매핑합니다.

```java
@RequestMapping(value = "/users", method = RequestMethod.GET)
public List<User> getAllUsers() {
    // 모든 사용자 반환
}
```

### **@GetMapping, @PostMapping, @PutMapping, @DeleteMapping**
- **기능**: 각각 GET, POST, PUT, DELETE 요청을 처리하는 메서드를 정의합니다.

```java
@PostMapping("/users")
public void createUser(@RequestBody User user) {
    // 사용자 생성 로직
}
```

## **4. 의존성 주입(Dependency Injection) 관련 어노테이션**

### **@Autowired**
- **기능**: 스프링이 빈의 의존성을 자동으로 주입하도록 합니다.

```java
@Autowired
private UserService userService;
```

### **@Qualifier**
- **기능**: 여러 빈 중에서 특정 빈을 주입받고자 할 때 사용합니다.

```java
@Autowired
@Qualifier("myService")
private MyService myService;
```

## **5. 트랜잭션 관리(Transaction Management) 관련 어노테이션**

### **@Transactional**
- **기능**: 메서드나 클래스에 적용되어 트랜잭션을 관리합니다. 데이터베이스 작업의 원자성을 보장합니다.

```java
@Transactional
public void updateUser(User user) {
    // 사용자 업데이트 로직
}
```

이와 같이 스프링부트의 어노테이션은 각기 다른 역할을 수행하며, 이를 통해 개발자는 복잡한 설정 없이도 강력한 애플리케이션을 쉽게 구축할 수 있습니다. 각 카테고리의 어노테이션을 이해하고 활용하면, 스프링부트를 보다 효과적으로 사용할 수 있습니다.
[1] https://mihee0703.tistory.com/205
[2] https://lincoding.tistory.com/76
[3] https://beginnerdevelopment.tistory.com/95
[4] https://curiousjinan.tistory.com/entry/spring-boot-annotations-guide-1
[5] https://velog.io/@falling_star3/Spring-Boot-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8-%EC%8A%A4%EC%BA%94
[6] https://velog.io/@path_creator/spring-annotation%EC%8A%A4%ED%94%84%EB%A7%81-%EC%96%B4%EB%85%B8%ED%85%90%EC%9D%B4%EC%85%98-%EC%A0%95%EB%A6%AC
[7] https://dream-and-develop.tistory.com/382
[8] https://kkh1902.tistory.com/156
[9] https://08genie.tistory.com/entry/Spring-Boot-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8Spring-Boot-%EC%96%B4%EB%85%B8%ED%85%8C%EC%9D%B4%EC%85%98Annotation
[10] https://velog.io/@kwak0568/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%95%B5%EC%8B%AC-%EC%9B%90%EB%A6%AC-%EA%B8%B0%EB%B3%B8%ED%8E%B8-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8-%EC%B0%BE%EA%B8%B0
[11] https://hirlawldo.tistory.com/43
[12] https://sddev.tistory.com/225
[13] https://jdoryeon.tistory.com/34
[14] https://mangkyu.tistory.com/242
[15] https://rudaks.tistory.com/entry/%EC%8A%A4%ED%94%84%EB%A7%81-%EB%B6%80%ED%8A%B8-%EC%96%B4%EB%85%B8%ED%85%8C%EC%9D%B4%EC%85%98
[16] https://devpad.tistory.com/105
[17] https://adjh54.tistory.com/311
[18] https://iliveinseoul.tistory.com/entry/SpringBoot-Annotation-%EC%82%AC%EC%9A%A9-%EC%A0%95%EB%A6%AC
[19] https://blog.naver.com/pink_candy02/223397625306?viewType=pc
[20] https://f-lab.kr/insight/efficient-transaction-management-in-spring-boot-20240708
[21] https://ch4njun.tistory.com/219
[22] https://blog.naver.com/joymrk/222448797656?viewType=pc
[23] https://ffdev.tistory.com/5
[24] https://ksh03003.tistory.com/97
[25] https://rebornbb.tistory.com/entry/SpringBoot-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-Annotation-%EA%B0%9C%EB%85%90-%EB%B0%8F-%EC%A0%95%EB%A6%AC
[26] https://doridam-1116.tistory.com/14
[27] https://positive-impactor.tistory.com/153
[28] https://dbjh.tistory.com/26
[29] https://ittrue.tistory.com/229
[30] https://jjangadadcodingdiary.tistory.com/entry/Spring-%EC%8A%A4%ED%94%84%EB%A7%81%EC%9D%98-Transactional-%EC%96%B4%EB%85%B8%ED%85%8C%EC%9D%B4%EC%85%98%EC%9D%84-%ED%99%9C%EC%9A%A9%ED%95%9C-%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4-%ED%8A%B8%EB%9E%9C%EC%9E%AD%EC%85%98-%EA%B4%80%EB%A6%AC
[31] https://hongs-coding.tistory.com/115
[32] https://code-run.tistory.com/19
[33] https://coding-zzang.tistory.com/43
[34] https://bangu4.tistory.com/295
[35] https://velog.io/@live_in_truth/Spring-%EC%96%B4%EB%85%B8%ED%85%8C%EC%9D%B4%EC%85%98%EC%9D%98-%EC%9E%A5%EC%A0%90%EA%B3%BC-%EC%9D%98%EC%A1%B4%EC%84%B1-%EC%A3%BC%EC%9E%85-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0feat-Autowired-RequiredArgsConstructor
[36] https://colevelup.tistory.com/34
[37] https://velog.io/@kbin9919/%EC%8A%A4%ED%94%84%EB%A7%81-%EB%B6%80%ED%8A%B8Spring-Boot-%EC%9D%98%EC%A1%B4%EC%84%B1-%EC%A3%BC%EC%9E%85DI-FINAL%EB%B6%88%EB%B3%80%EC%84%B1
[38] https://haemanlee.tistory.com/33
[39] https://devjaewoo.tistory.com/79
[40] https://juntcom.tistory.com/232
[41] https://velog.io/@yeppi/SpringBoot2-Annotation-%EC%9E%90%EB%8F%99-%EC%84%A4%EC%A0%95-starter-%ED%99%9C%EC%9A%A9%ED%95%98%EA%B8%B0
[42] https://yeonyeon.tistory.com/230
[43] https://velog.io/@yeonssu/Spring-Boot-Annotation-%EC%A0%95%EB%A6%AC
[44] https://adjh54.tistory.com/312
[45] https://hstory0208.tistory.com/entry/Spring-HTTP-%EC%9A%94%EC%B2%AD-%EB%B0%A9%EB%B2%95%EA%B3%BC-%EA%B4%80%EB%A0%A8-%EC%96%B4%EB%85%B8%ED%85%8C%EC%9D%B4%EC%85%98Annotation
[46] https://velog.io/@devlyny/Spring-Boot%EB%8A%94-%EC%9A%94%EC%B2%AD%EC%9D%84-%EC%96%B4%EB%96%BB%EA%B2%8C
[47] https://velog.io/@dbyo1125/%EC%8A%A4%ED%94%84%EB%A7%81-%EB%B6%80%ED%8A%B8Spring-Boot-%EC%95%A0%EB%84%88%ED%85%8C%EC%9D%B4%EC%85%98
[48] https://sas-study.tistory.com/443
[49] https://medium.com/@hgbaek1128/transactional%EC%9D%80-%EC%96%B8%EC%A0%9C%EC%8D%A8%EC%95%BC%ED%95%A0%EA%B9%8C-bd7aac4ad17f
[50] https://kafcamus.tistory.com/30
[51] https://velog.io/@gale4739/Spring-Boot-InsertUpdate-%EB%B0%8F-%ED%8A%B8%EB%9E%9C%EC%9E%AD%EC%85%98-%EC%B2%98%EB%A6%AC
[52] https://blog.naver.com/seek316/222707671228
