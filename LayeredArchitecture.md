## 스프링부트 레이어드 아키텍처와 프로젝트 트리 구조

스프링부트의 레이어드 아키텍처는 애플리케이션을 여러 개의 계층으로 나누어 각 계층이 특정한 역할을 수행하도록 설계되어 있습니다. 이 구조는 유지보수성과 확장성을 높이며, 각 계층은 독립적으로 개발 및 테스트할 수 있습니다. 주요 계층은 다음과 같습니다:

### 주요 계층

1. **프레젠테이션 계층 (Presentation Layer)**:
   - 사용자와 상호작용하는 계층으로, HTTP 요청을 처리하고 응답을 반환합니다.
   - 주로 REST 컨트롤러가 포함되며, 클라이언트의 요청을 비즈니스 계층으로 전달합니다.
   - 인증 및 요청 유효성 검증을 수행하며, JSON 변환 작업도 포함됩니다.

2. **비즈니스 계층 (Business Layer)**:
   - 애플리케이션의 핵심 비즈니스 로직을 처리하는 계층입니다.
   - 서비스 클래스를 통해 데이터 처리, 유효성 검사, 트랜잭션 관리 등을 수행합니다.
   - 프레젠테이션 계층과 데이터 접근 계층 간의 중재 역할을 하며, 비즈니스 규칙을 적용합니다.

3. **퍼시스턴스 계층 (Persistence Layer)**:
   - 데이터베이스와의 상호작용을 담당하는 계층으로, CRUD 작업을 수행합니다.
   - 주로 ORM 프레임워크(예: JPA, MyBatis)를 사용하여 데이터베이스와 연결됩니다.
   - 데이터 접근 객체(DAO)를 통해 데이터의 저장 및 조회를 처리합니다.

4. **도메인 계층 (Domain Layer)**:
   - 비즈니스 도메인과 관련된 객체를 정의하는 계층입니다.
   - 도메인 모델은 비즈니스 로직을 포함하며, 데이터베이스의 엔티티와 유사한 구조를 가집니다.
   - 이 계층은 비즈니스 규칙과 도메인 개념을 표현하며, DTO(Data Transfer Object)와 VO(Value Object) 등의 객체를 포함합니다.

5. **인프라스트럭처 계층 (Infrastructure Layer)**:
   - 애플리케이션의 기술적 요구사항을 처리하는 계층으로, 외부 시스템과의 통신을 담당합니다.
   - 데이터베이스 연결, 메시징 시스템, 외부 API와의 통신 등을 포함합니다.

### 프로젝트 트리 구조 예시

스프링부트 프로젝트의 기본적인 트리 구조는 다음과 같습니다:

```
src
 └── main
     ├── java
     │   └── com
     │       └── example
     │           ├── controller
     │           │   ├── ProductController.java
     │           │   ├── MemberController.java
     │           │   └── CartController.java
     │           ├── service
     │           │   ├── ProductService.java
     │           │   ├── MemberService.java
     │           │   └── CartService.java
     │           ├── repository
     │           │   ├── ProductRepository.java
     │           │   ├── MemberRepository.java
     │           │   └── CartRepository.java
     │           ├── model
     │           │   ├── Product.java
     │           │   ├── Member.java
     │           │   └── Cart.java
     │           └── infrastructure
     │               ├── DatabaseConfig.java
     │               └── MessagingService.java
     └── resources
         ├── application.properties
         └── static
```

- **controller**: 프레젠테이션 계층의 컨트롤러 클래스가 위치합니다.
- **service**: 비즈니스 로직을 처리하는 서비스 클래스가 위치합니다.
- **repository**: 데이터베이스와의 상호작용을 위한 리포지토리 인터페이스가 위치합니다.
- **model**: 데이터 모델 클래스가 위치합니다.
- **infrastructure**: 인프라스트럭처 계층의 구성 요소가 위치하며, 데이터베이스 설정 및 외부 시스템과의 통신을 처리하는 클래스가 포함됩니다.
- **resources**: 애플리케이션 설정 파일 및 정적 리소스가 포함됩니다.

이러한 계층 구조는 각 계층이 독립적으로 개발될 수 있도록 하여, 코드의 재사용성과 유지보수성을 높이는 데 기여합니다. 각 계층은 명확한 책임을 가지고 있으며, 상위 계층은 하위 계층에 의존하지만, 하위 계층은 상위 계층의 구현 세부사항을 알 필요가 없습니다.
[1] https://innovation123.tistory.com/169
[2] https://jh7722.tistory.com/13
[3] https://engineerinsight.tistory.com/63
[4] https://xeounxzxu.medium.com/spring-4%EA%B3%84%EC%B8%B5%EB%A0%88%EC%9D%B4%EC%96%B4-%EC%86%8C%ED%94%84%ED%8A%B8%EC%9B%A8%EC%96%B4-%EC%95%84%ED%82%A4%ED%85%8D%EC%B2%98-8dc40298ba90
[5] https://velog.io/@julie0005/Layered-Architecture%EC%97%90-%EB%8C%80%ED%95%9C-%EA%B3%A0%EC%B0%B0-%EB%B0%8F-%EB%B3%80%ED%98%95
[6] https://poetic-code.tistory.com/112
[7] https://giron.tistory.com/92
[8] https://skyriv312079.tistory.com/42
[9] https://djcho.github.io/springboot/spring-boot-chapter2-3/
[10] https://jepa.tistory.com/10
[11] https://velog.io/@gayeong39/SPRING-%EB%A0%88%EC%9D%B4%EC%96%B4%EB%93%9C-%EC%95%84%ED%82%A4%ED%85%8D%EC%B2%98
[12] https://loosie.tistory.com/296
[13] https://velog.io/@dnrwhddk1/Spring-%EB%A0%88%EC%9D%B4%EC%96%B4%EB%93%9C-%EC%95%84%ED%82%A4%ED%85%8D%EC%B2%98
[14] https://senna.tistory.com/2
[15] https://www.reddit.com/r/SpringBoot/comments/13ftcsw/can_you_apply_hexagonal_architecture_to_springboot/
[16] https://dev-coco.tistory.com/166
[17] https://medium.com/@nagireddygajjela19/spring-boot-project-setup-and-layered-architecture-introduction-936f560fd219
[18] https://lifelife7777.tistory.com/100
[19] https://medium.com/mo-zza/spring-boot-%EA%B8%B0%EB%B0%98-%ED%97%A5%EC%82%AC%EA%B3%A0%EB%82%A0-%EC%95%84%ED%82%A4%ED%85%8D%EC%B2%98-hexagonal-architecture-with-spring-boot-4daf81752756
[20] https://m.blog.naver.com/sosow0212/223086185606
[21] https://velog.io/@9aeun/Spring-Boot-%EA%B0%9C%EB%B0%9C%EC%97%90-%EC%95%9E%EC%84%9C-%EC%95%8C%EB%A9%B4-%EC%A2%8B%EC%9D%80-%EA%B8%B0%EC%B4%88-%EC%A7%80%EC%8B%9D2
[22] https://deepeshkumarkurapati.medium.com/exploring-key-architectures-in-spring-boot-layered-mvc-and-microservices-d0f0c370e206
[23] https://velog.io/@sunil1369/Spring-boot-%ED%8C%A8%ED%82%A4%EC%A7%80-%EA%B5%AC%EC%A1%B0
[24] https://rameshfadatare.medium.com/spring-boot-architecture-controller-service-repository-database-architecture-flow-9144084818b0
[25] https://godekdls.github.io/Spring%20Integration/overview/
[26] https://medium.com/@RogelioOrts/layered-architecture-spring-boot-af7dc071d2b5
[27] https://www.geeksforgeeks.org/springboot/spring-boot-architecture/
[28] https://pwskills.com/blog/architecture-of-spring-boot-examples-pattern-layered-controller-layer/
[29] https://stackoverflow.com/questions/76139579/hexagonal-architecture-spring-boot
[30] https://dev.to/writech/designing-a-multi-layered-architecture-for-building-restful-web-services-with-spring-boot-and-kotlin-51l5
[31] https://www.baeldung.com/spring-boot-clean-architecture
[32] https://stackoverflow.com/questions/51953758/layered-architecture-application-and-infra-layer
[33] https://www.reddit.com/r/SpringBoot/comments/13co4al/hexagonal_architecture_or_rest_layers/
[34] https://medium.com/@udaypatil318/spring-boot-architecture-39935654ce5c
[35] https://www.reddit.com/r/SpringBoot/comments/1029xf6/good_indepth_resources_for_layered_architecture/
[36] https://1kevinson.com/understand-how-spring-boot-architecture-is-designed/
[37] https://levelup.gitconnected.com/understanding-spring-boot-architecture-6083e2631bc6
[38] https://stackoverflow.com/questions/34429832/how-to-use-layered-architecture-of-spring-and-still-follow-object-oriented-struc
[39] https://malshani-wijekoon.medium.com/spring-boot-folder-structure-best-practices-18ef78a81819
[40] https://www.reddit.com/r/SpringBoot/comments/1h2efiw/ddd_domain_driven_design_how_do_you_structure/
[41] https://symflower.com/en/company/blog/2024/spring-boot-folder-structure/
[42] https://github.com/longporo/my-springboot-app
[43] https://www.reddit.com/r/SpringBoot/comments/1fsecgk/package_structure/
