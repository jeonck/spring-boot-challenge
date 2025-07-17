백엔드 개발에서 디자인 패턴은 코드의 구조와 유지보수성을 향상시키기 위해 사용되는 중요한 도구입니다. 아래는 다양한 디자인 패턴을 쉽게 이해할 수 있도록 재구성한 내용입니다.

## 디자인 패턴의 필요성

백엔드 코드를 작성하다 보면, 작동은 하지만 이해하기 어렵거나 수정하기 힘든 코드에 직면할 수 있습니다. 이러한 문제를 해결하기 위해 디자인 패턴이 필요합니다. 디자인 패턴은 실제 시스템에서 발생하는 복잡한 문제를 해결하기 위한 검증된 방법론입니다.

## 주요 디자인 패턴

### 1. 빌더 패턴 (Builder Pattern)
- **문제**: 복잡한 생성자 호출로 인해 가독성이 떨어짐.
- **해결**: 빌더 패턴을 사용하여 객체를 단계별로 구성합니다.
  
  ```java
  User user = User.builder()
      .username("john.doe")
      .role("admin")
      .active(true)
      .build();
  ```

### 2. 전략 패턴 (Strategy Pattern)
- **문제**: 조건문이 많아져서 코드가 복잡해짐.
- **해결**: 각 전략을 별도의 클래스로 분리하여 필요할 때마다 교체할 수 있습니다.

  ```java
  public interface DiscountStrategy {
      BigDecimal calculate(Order order);
  }
  ```

### 3. 팩토리 패턴 (Factory Pattern)
- **문제**: 객체 생성 로직이 복잡해짐.
- **해결**: 팩토리 클래스를 사용하여 객체 생성을 중앙 집중화합니다.

  ```java
  public class NotificationFactory {
      public NotificationService get(String channel) {
          return switch(channel) {
              case "email" -> new EmailNotification(...);
              case "sms" -> new SmsNotification(...);
              default -> throw new IllegalArgumentException();
          };
      }
  }
  ```

### 4. 레포지토리 패턴 (Repository Pattern)
- **문제**: 데이터 접근 로직이 비즈니스 로직과 혼합됨.
- **해결**: 데이터 접근을 위한 별도의 레포지토리 클래스를 생성합니다.

  ```java
  public interface UserRepository extends JpaRepository<User, Long> {
      Optional<User> findByEmail(String email);
  }
  ```

### 5. 옵저버 패턴 (Observer Pattern)
- **문제**: 이벤트 기반 시스템에서 느슨한 결합이 필요함.
- **해결**: 옵저버 패턴을 사용하여 이벤트 발생 시 여러 객체가 반응하도록 합니다.

  ```java
  public class AlertService {
      private List<AlertSender> senders = new ArrayList<>();
      // ...
  }
  ```

### 6. 책임 연쇄 패턴 (Chain of Responsibility)
- **문제**: 요청 처리 로직이 복잡해짐.
- **해결**: 요청을 여러 핸들러를 통해 전달하여 각 핸들러가 하나의 작업을 수행하도록 합니다.

### 7. 템플릿 메서드 패턴 (Template Method)
- **문제**: 비슷한 로직을 반복적으로 구현해야 함.
- **해결**: 공통 로직을 추상 클래스에 정의하고, 변하는 부분만 서브클래스에서 구현합니다.

### 8. CQRS (Command Query Responsibility Segregation)
- **문제**: 읽기와 쓰기 로직이 복잡하게 얽힘.
- **해결**: 읽기와 쓰기 모델을 분리하여 각각 최적화합니다.

### 9. 데코레이터 패턴 (Decorator Pattern)
- **문제**: 기존 객체를 수정하지 않고 기능을 추가하고 싶음.
- **해결**: 객체를 감싸는 데코레이터 클래스를 사용하여 기능을 추가합니다.

### 10. 프록시 패턴 (Proxy Pattern)
- **문제**: 클라이언트와 실제 객체 간의 접근을 제어하고 싶음.
- **해결**: 프록시 객체를 사용하여 요청을 대신 처리합니다.

## 결론

디자인 패턴은 단순히 이론적인 개념이 아니라, 실제 문제를 해결하기 위한 실용적인 도구입니다. 이러한 패턴을 이해하고 적절히 활용하면, 더 깔끔하고 유지보수하기 쉬운 코드를 작성할 수 있습니다. 각 패턴의 사용 사례와 장단점을 잘 이해하고, 필요할 때 적절히 적용하는 것이 중요합니다.
[1] https://jiyeonseo.github.io/digital-garden/notes/backend-communication-design-patterns/
[2] https://appleg1226.tistory.com/49
[3] https://gamza1013.tistory.com/105
[4] https://www.inflearn.com/course/%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5-%EB%94%94%EC%9E%90%EC%9D%B8-%ED%8C%A8%ED%84%B4-%EC%96%84%EC%BD%94?srsltid=AfmBOopanaqWhV-q-YyPxwfBpOWZpr4oYo0-SeO-kpSTWYBkqOz6H4q9
[5] https://velog.io/@sierra9707/%EB%B0%B1%EC%97%94%EB%93%9C-%EB%A1%9C%EB%93%9C%EB%A7%B5-%EA%B0%9C%EB%B0%9C%EB%B0%A9%EB%B2%95%EB%A1%A0-Design-Pattern-Part3
[6] https://coding-business.tistory.com/42
[7] https://appleg1226.tistory.com/51
[8] https://sprint.codeit.kr/blog/2025-spring-%EB%B0%B1%EC%97%94%EB%93%9C-%EC%B7%A8%EC%97%85-%EB%A1%9C%EB%93%9C%EB%A7%B5
[9] https://kimjingo.tistory.com/159
[10] https://github.com/self-taught-fe-dev/fe-roadmap
[11] https://appleg1226.tistory.com/52
[12] https://m.hanbit.co.kr/store/books/book_view.html?p_code=B9696096335
[13] https://refactoring.guru/ko/design-patterns/book
[14] https://wlsdn93.github.io/life/how-i-became-a-developer/
[15] https://bb-dochi.tistory.com/72
[16] https://shoark7.github.io/programming/knowledge/what-is-design-pattern
[17] https://velog.io/@gusdh2/%EB%94%94%EC%9E%90%EC%9D%B8-%ED%8C%A8%ED%84%B4%EC%9D%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80
[18] https://oobwrite.com/entry/%EB%94%94%EC%9E%90%EC%9D%B8-%ED%8C%A8%ED%84%B4Design-Pattern-%EC%B4%9D%EC%A0%95%EB%A6%AC-23%EA%B0%80%EC%A7%80-%EB%94%94%EC%9E%90%EC%9D%B8-%ED%8C%A8%ED%84%B4-%EC%A0%95%EC%9D%98-%EC%A2%85%EB%A5%98-%EC%9E%A5%EB%8B%A8%EC%A0%90
[19] https://innovation123.tistory.com/171
[20] https://velog.io/@path_creator/%EB%B0%B1%EC%97%94%EB%93%9C%EC%97%90%EC%84%9C-%EC%9E%90%EC%A3%BC-%EC%82%AC%EC%9A%A9%EB%90%98%EB%8A%94-%EB%94%94%EC%9E%90%EC%9D%B8%ED%8C%A8%ED%84%B4-%EA%B5%AC%EC%A1%B0-%ED%8C%A8%ED%84%B4%ED%98%95-nayvgs1w
[21] https://hyeonproject.medium.com/%EB%B0%B0%EC%9B%8C%EB%B3%B4%EC%9E%90-%EB%94%94%EC%9E%90%EC%9D%B8%ED%8C%A8%ED%84%B4-1-%EB%94%94%EC%9E%90%EC%9D%B8-%ED%8C%A8%ED%84%B4-41f248fad091
[22] https://velog.io/@sierra9707/%EB%B0%B1%EC%97%94%EB%93%9C-%EB%A1%9C%EB%93%9C%EB%A7%B5-Design-Pattern-Design-Pattern-Part1
[23] https://mingrammer.com/translation-10-common-software-architectural-patterns-in-a-nutshell/
[24] https://molonlabe.tistory.com/19
[25] https://github.com/ksundong/backend-interview-question
[26] https://www.inflearn.com/course/%EB%B9%84%EC%A0%84%EA%B3%B5%EC%9E%90%EB%A5%BC-%EC%9C%84%ED%95%9C-spring-mvc-%EA%B8%B0%EC%B4%88?srsltid=AfmBOopQ2lQvB5uHYP4o3N1U6FOiwRhu653ruFRmK4cExyg6plhhiL9Y
