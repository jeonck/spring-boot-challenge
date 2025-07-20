의존성 주입(Dependency Injection, DI)은 객체 간의 결합도를 줄이고, 코드의 유연성과 재사용성을 높이는 중요한 프로그래밍 패턴입니다. 이 과정에서 `@Autowired` 어노테이션을 사용하면 필요한 모듈(빈)을 스프링 컨테이너에서 자동으로 주입받을 수 있습니다. 

## **의존성 주입의 의미**
- **의존성**: 특정 객체가 다른 객체에 의존하는 관계를 의미합니다. 예를 들어, 서비스 클래스가 데이터베이스 접근을 위해 리포지토리 클래스를 필요로 할 때, 서비스 클래스는 리포지토리에 의존한다고 할 수 있습니다.
  
- **의존성 주입**: 필요한 객체를 직접 생성하는 것이 아니라, 외부에서 주입받는 방식입니다. 이를 통해 객체 간의 결합도를 낮추고, 코드의 재사용성을 높일 수 있습니다[1][2].

## **@Autowired의 역할**
- `@Autowired`는 스프링에서 의존성을 자동으로 주입할 때 사용하는 어노테이션입니다. 이 어노테이션이 붙은 필드, 생성자, 또는 세터 메서드에 스프링 컨테이너가 관리하는 빈을 자동으로 주입합니다[1][2][5].

### **예시**
```java
@Service
public class UserService {
    
    @Autowired
    private UserRepository userRepository; // UserRepository 빈이 자동으로 주입됨

    public void createUser(User user) {
        userRepository.save(user);
    }
}
```

위의 예시에서 `UserService` 클래스는 `UserRepository`에 의존하고 있으며, `@Autowired`를 통해 스프링이 자동으로 `UserRepository` 빈을 주입합니다. 이로 인해 개발자는 `UserRepository`를 직접 생성할 필요가 없고, 코드의 가독성과 유지보수성이 향상됩니다.

## **결론**
따라서, 의존성 주입은 필요한 모듈을 외부에서 주입받아 사용하는 과정이며, `@Autowired`를 통해 스프링이 관리하는 빈을 자동으로 인식하고 주입할 수 있습니다. 이는 코드의 결합도를 낮추고, 유연한 구조를 만들어 주는 중요한 기능입니다.
[1] https://velog.io/@ka0ka0ka/Autowired
[2] https://dev-coco.tistory.com/70
[3] https://wolmido.tistory.com/17
[4] https://5bong2-develop.tistory.com/23
[5] https://workshop-6349.tistory.com/entry/Spring-Core-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8-%EC%8A%A4%EC%BA%94%EA%B3%BC-%EC%9D%98%EC%A1%B4%EC%84%B1-%EC%A3%BC%EC%9E%85
[6] https://oneul-losnue.tistory.com/364
[7] https://www.catsriding.com/posts/dependency-injection-through-ioc-container-in-spring
[8] https://cmelcmel.tistory.com/96
[9] https://softwareengineering.stackexchange.com/questions/231867/which-classes-should-be-autowired-by-spring-when-to-use-dependency-injection
[10] https://www.quora.com/Why-do-we-use-Autowire-Spring-Spring-Boot-Spring-MVC-and-development
[11] https://joo0jae.tistory.com/m/329?category=1156445
[12] https://www.geeksforgeeks.org/spring-autowiring/
[13] https://www.reddit.com/r/java/comments/12imnqx/why_dependency_injection/
[14] https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/beans/factory/annotation/Autowired.html
[15] https://codesignal.com/learn/courses/introduction-to-spring-boot-and-spring-core-with-kotlin/lessons/dependency-injection-in-spring-boot
[16] https://www.reddit.com/r/SpringBoot/comments/13o315s/why_do_injected_dependencies_are_declared_as/
[17] https://www.baeldung.com/spring-autowire
[18] https://stackoverflow.com/questions/63933520/can-spring-boots-autowired-inject-dependencies-from-a-jarincluded-in-classpat
[19] https://mohammed-atif.medium.com/spring-boot-does-every-dependency-need-to-be-injected-757fa2cc69d8
[20] https://www.reddit.com/r/java/comments/kubqic/dependency_injection_containers_are_we_still/?tl=ko
