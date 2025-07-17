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

백엔드 개발에서 디자인 패턴은 코드의 구조와 유지보수성을 향상시키기 위해 사용되는 중요한 도구입니다. 아래는 다양한 디자인 패턴을 쉽게 이해할 수 있도록 문제에 대한 예시 코드와 함께 재구성한 내용입니다.

## 디자인 패턴의 필요성

백엔드 코드를 작성하다 보면, 작동은 하지만 이해하기 어렵거나 수정하기 힘든 코드에 직면할 수 있습니다. 이러한 문제를 해결하기 위해 디자인 패턴이 필요합니다. 디자인 패턴은 실제 시스템에서 발생하는 복잡한 문제를 해결하기 위한 검증된 방법론입니다.

## 주요 디자인 패턴

### 1. 빌더 패턴 (Builder Pattern)
- **문제**: 복잡한 생성자 호출로 인해 가독성이 떨어짐.
- **해결**: 빌더 패턴을 사용하여 객체를 단계별로 구성합니다.

  **예시 코드**:
  ```java
  public class User {
      private String username;
      private String role;
      private boolean active;

      private User(UserBuilder builder) {
          this.username = builder.username;
          this.role = builder.role;
          this.active = builder.active;
      }

      public static class UserBuilder {
          private String username;
          private String role;
          private boolean active;

          public UserBuilder username(String username) {
              this.username = username;
              return this;
          }

          public UserBuilder role(String role) {
              this.role = role;
              return this;
          }

          public UserBuilder active(boolean active) {
              this.active = active;
              return this;
          }

          public User build() {
              return new User(this);
          }
      }
  }

  // 사용 예
  User user = new User.UserBuilder()
      .username("john.doe")
      .role("admin")
      .active(true)
      .build();
  ```

### 2. 전략 패턴 (Strategy Pattern)
- **문제**: 조건문이 많아져서 코드가 복잡해짐.
- **해결**: 각 전략을 별도의 클래스로 분리하여 필요할 때마다 교체할 수 있습니다.

  **예시 코드**:
  ```java
  public interface DiscountStrategy {
      BigDecimal calculate(Order order);
  }

  public class PremiumDiscount implements DiscountStrategy {
      public BigDecimal calculate(Order order) {
          return order.getTotal().multiply(new BigDecimal("0.9")); // 10% 할인
      }
  }

  public class GuestDiscount implements DiscountStrategy {
      public BigDecimal calculate(Order order) {
          return order.getTotal(); // 할인 없음
      }
  }

  // 사용 예
  DiscountStrategy strategy = user.isPremium() ? new PremiumDiscount() : new GuestDiscount();
  BigDecimal finalPrice = strategy.calculate(order);
  ```

### 3. 팩토리 패턴 (Factory Pattern)
- **문제**: 객체 생성 로직이 복잡해짐.
- **해결**: 팩토리 클래스를 사용하여 객체 생성을 중앙 집중화합니다.

  **예시 코드**:
  ```java
  public class NotificationFactory {
      public NotificationService get(String channel) {
          switch (channel) {
              case "email":
                  return new EmailNotification();
              case "sms":
                  return new SmsNotification();
              default:
                  throw new IllegalArgumentException("Unknown channel: " + channel);
          }
      }
  }

  // 사용 예
  NotificationFactory factory = new NotificationFactory();
  NotificationService notification = factory.get("email");
  ```

### 4. 레포지토리 패턴 (Repository Pattern)
- **문제**: 데이터 접근 로직이 비즈니스 로직과 혼합됨.
- **해결**: 데이터 접근을 위한 별도의 레포지토리 클래스를 생성합니다.

  **예시 코드**:
  ```java
  public interface UserRepository {
      Optional<User> findByEmail(String email);
  }

  public class UserRepositoryImpl implements UserRepository {
      // 데이터베이스 접근 로직 구현
      public Optional<User> findByEmail(String email) {
          // DB에서 사용자 검색 로직
      }
  }

  // 사용 예
  UserRepository userRepository = new UserRepositoryImpl();
  Optional<User> user = userRepository.findByEmail("john.doe@example.com");
  ```

### 5. 옵저버 패턴 (Observer Pattern)
- **문제**: 이벤트 기반 시스템에서 느슨한 결합이 필요함.
- **해결**: 옵저버 패턴을 사용하여 이벤트 발생 시 여러 객체가 반응하도록 합니다.

  **예시 코드**:
  ```java
  public interface Observer {
      void update(String event);
  }

  public class EmailAlert implements Observer {
      public void update(String event) {
          System.out.println("Email alert for event: " + event);
      }
  }

  public class EventManager {
      private List<Observer> observers = new ArrayList<>();

      public void subscribe(Observer observer) {
          observers.add(observer);
      }

      public void notifyObservers(String event) {
          for (Observer observer : observers) {
              observer.update(event);
          }
      }
  }

  // 사용 예
  EventManager eventManager = new EventManager();
  eventManager.subscribe(new EmailAlert());
  eventManager.notifyObservers("User signed up");
  ```

### 6. 책임 연쇄 패턴 (Chain of Responsibility)
- **문제**: 요청 처리 로직이 복잡해짐.
- **해결**: 요청을 여러 핸들러를 통해 전달하여 각 핸들러가 하나의 작업을 수행하도록 합니다.

  **예시 코드**:
  ```java
  public abstract class Handler {
      protected Handler next;

      public void setNext(Handler next) {
          this.next = next;
      }

      public abstract void handleRequest(String request);
  }

  public class ConcreteHandlerA extends Handler {
      public void handleRequest(String request) {
          if (request.equals("A")) {
              System.out.println("Handled by A");
          } else if (next != null) {
              next.handleRequest(request);
          }
      }
  }

  public class ConcreteHandlerB extends Handler {
      public void handleRequest(String request) {
          if (request.equals("B")) {
              System.out.println("Handled by B");
          } else if (next != null) {
              next.handleRequest(request);
          }
      }
  }

  // 사용 예
  Handler handlerA = new ConcreteHandlerA();
  Handler handlerB = new ConcreteHandlerB();
  handlerA.setNext(handlerB);
  handlerA.handleRequest("B");
  ```

### 7. 템플릿 메서드 패턴 (Template Method)
- **문제**: 비슷한 로직을 반복적으로 구현해야 함.
- **해결**: 공통 로직을 추상 클래스에 정의하고, 변하는 부분만 서브클래스에서 구현합니다.

  **예시 코드**:
  ```java
  public abstract class PaymentProcessor {
      public void process() {
          validate();
          charge();
          sendReceipt();
      }

      protected abstract void charge();

      private void validate() {
          System.out.println("Validation logic");
      }

      private void sendReceipt() {
          System.out.println("Receipt sent");
      }
  }

  public class CreditCardPayment extends PaymentProcessor {
      protected void charge() {
          System.out.println("Charging credit card");
      }
  }

  // 사용 예
  PaymentProcessor payment = new CreditCardPayment();
  payment.process();
  ```

### 8. CQRS (Command Query Responsibility Segregation)
- **문제**: 읽기와 쓰기 로직이 복잡하게 얽힘.
- **해결**: 읽기와 쓰기 모델을 분리하여 각각 최적화합니다.

  **예시 코드**:
  ```java
  public class CommandService {
      public void createOrder(Order order) {
          // 주문 생성 로직
      }
  }

  public class QueryService {
      public Order getOrderById(String id) {
          // 주문 조회 로직
      }
  }

  // 사용 예
  CommandService commandService = new CommandService();
  QueryService queryService = new QueryService();
  commandService.createOrder(new Order());
  Order order = queryService.getOrderById("123");
  ```

### 9. 데코레이터 패턴 (Decorator Pattern)
- **문제**: 기존 객체를 수정하지 않고 기능을 추가하고 싶음.
- **해결**: 객체를 감싸는 데코레이터 클래스를 사용하여 기능을 추가합니다.

  **예시 코드**:
  ```java
  public interface UserService {
      User get(String id);
  }

  public class BasicUserService implements UserService {
      public User get(String id) {
          return new User(id); // 기본 사용자 반환
      }
  }

  public class CachingUserService implements UserService {
      private final UserService delegate;
      private final Map<String, User> cache = new HashMap<>();

      public CachingUserService(UserService delegate) {
          this.delegate = delegate;
      }

      public User get(String id) {
          return cache.computeIfAbsent(id, k -> delegate.get(k));
      }
  }

  // 사용 예
  UserService userService = new CachingUserService(new BasicUserService());
  User user = userService.get("john.doe");
  ```

### 10. 프록시 패턴 (Proxy Pattern)
- **문제**: 클라이언트와 실제 객체 간의 접근을 제어하고 싶음.
- **해결**: 프록시 객체를 사용하여 요청을 대신 처리합니다.

  **예시 코드**:
  ```java
  public interface Image {
      void display();
  }

  public class RealImage implements Image {
      private String filename;

      public RealImage(String filename) {
          this.filename = filename;
          loadImageFromDisk();
      }

      private void loadImageFromDisk() {
          System.out.println("Loading " + filename);
      }

      public void display() {
          System.out.println("Displaying " + filename);
      }
  }

  public class ProxyImage implements Image {
      private RealImage realImage;
      private String filename;

      public ProxyImage(String filename) {
          this.filename = filename;
      }

      public void display() {
          if (realImage == null) {
              realImage = new RealImage(filename);
          }
          realImage.display();
      }
  }

  // 사용 예
  Image image = new ProxyImage("test_image.jpg");
  image.display(); // 처음 호출 시 로드
  image.display(); // 이후 호출 시 로드하지 않음
  ```

## 결론

디자인 패턴은 단순히 이론적인 개념이 아니라, 실제 문제를 해결하기 위한 실용적인 도구입니다. 이러한 패턴을 이해하고 적절히 활용하면, 더 깔끔하고 유지보수하기 쉬운 코드를 작성할 수 있습니다. 각 패턴의 사용 사례와 장단점을 잘 이해하고, 필요할 때 적절히 적용하는 것이 중요합니다.
[1] https://yelkim0210.tistory.com/130
[2] https://blog.naver.com/hanbitstory/223774065324
[3] https://ittrue.tistory.com/550
[4] https://velog.io/@nasaoreo/%EC%86%8C%ED%94%84%ED%8A%B8%EC%9B%A8%EC%96%B4-%EB%94%94%EC%9E%90%EC%9D%B8-%ED%8C%A8%ED%84%B4-%EB%AC%B8%EC%A0%9C%EC%97%90-%EB%8C%80%ED%95%9C-%ED%95%B4%EA%B2%B0%EC%B1%85
[5] https://velog.io/@nwn/1.3.27-1.3.28-%EC%BD%94%EB%93%9C-%EB%94%94%EC%9E%90%EC%9D%B8-%ED%8C%A8%ED%84%B4
[6] https://dev.to/divine_nnanna2/design-patterns-for-backend-development-1h57
[7] https://newsletter.masteringbackend.com/p/design-patterns
[8] https://www.geeksforgeeks.org/system-design/design-patterns-for-modern-backend-development/
[9] https://www.freecodecamp.org/news/design-pattern-for-modern-backend-development-and-use-cases/
[10] https://appleg1226.tistory.com/49
[11] https://dev.to/documatic/from-problems-to-solutions-understanding-design-patterns-3b7i
[12] https://oobwrite.com/entry/%EB%94%94%EC%9E%90%EC%9D%B8-%ED%8C%A8%ED%84%B4Design-Pattern-%EC%B4%9D%EC%A0%95%EB%A6%AC-23%EA%B0%80%EC%A7%80-%EB%94%94%EC%9E%90%EC%9D%B8-%ED%8C%A8%ED%84%B4-%EC%A0%95%EC%9D%98-%EC%A2%85%EB%A5%98-%EC%9E%A5%EB%8B%A8%EC%A0%90
[13] https://appleg1226.tistory.com/51
[14] https://www.reddit.com/r/Backend/comments/s1v01w/backend_design_patterns/
[15] https://mojing.tistory.com/entry/CSDesign-Pattern-GoF-%EB%94%94%EC%9E%90%EC%9D%B8-%ED%8C%A8%ED%84%B4-%EC%A0%95%EB%A6%AC
[16] https://medium.com/@mchtyener/design-patterns-solutions-for-cleaner-and-reusable-code-in-software-development-02ceb55b3109
[17] https://www.reddit.com/r/java/comments/2b4yyc/java_learning_design_patterns_using_a_problem/
[18] https://velog.io/@sierra9707/%EB%B0%B1%EC%97%94%EB%93%9C-%EB%A1%9C%EB%93%9C%EB%A7%B5-%EA%B0%9C%EB%B0%9C%EB%B0%A9%EB%B2%95%EB%A1%A0-Design-Pattern-Part3
[19] https://todamfather.tistory.com/86
[20] https://gamza1013.tistory.com/105
[21] https://jade314.tistory.com/entry/%EB%94%94%EC%9E%90%EC%9D%B8%EC%84%A4%EA%B3%84-%ED%8C%A8%ED%84%B4-%EB%B6%84%EB%A5%98
[22] https://dzone.com/articles/key-back-end-design-patterns-for-scalability-and-maintenance
[23] https://medium.com/@bartzalewski/exploring-design-and-development-principles-in-backend-development-09ec61aa4e01
[24] https://github.com/kamranahmedse/design-patterns-for-humans
[25] https://refactoring.guru/ko/design-patterns
[26] https://blog.naver.com/jihoanry/223202814696?fromRss=true&trackingCode=rss
[27] https://sourcemaking.com/design_patterns
[28] https://www.freecodecamp.org/news/communication-design-patterns-for-backend-development/
[29] https://www.digitalocean.com/community/tutorials/java-design-patterns-example-tutorial
[30] https://manoj-shu100.medium.com/design-patterns-in-software-development-common-solutions-to-common-problems-ca001772f17c
[31] https://velog.io/@sierra9707/%EB%B0%B1%EC%97%94%EB%93%9C-%EB%A1%9C%EB%93%9C%EB%A7%B5-Design-Pattern-Design-Pattern-Part1
[32] https://medium.com/@hanxuyang0826/roadmap-to-backend-programming-master-architectural-patterns-c763c9194414
[33] https://refactoring.guru/design-patterns
[34] https://www.geeksforgeeks.org/system-design/software-design-patterns/
[35] https://stackoverflow.com/questions/466365/when-are-design-patterns-the-problem-instead-of-the-solution


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
