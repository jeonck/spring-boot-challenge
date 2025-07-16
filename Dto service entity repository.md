DTO(Data Transfer Object)는 데이터 전송을 위한 객체로, 서비스 계층에서 요청을 받아 엔티티로 변환한 후, 이를 리포지토리를 통해 데이터베이스에 저장하는 과정에서 중요한 역할을 합니다. 이 과정은 다음과 같은 단계로 이루어집니다.

## **1. 요청 처리**

사용자가 API를 통해 데이터를 요청하면, 해당 요청은 컨트롤러로 전달됩니다. 컨트롤러는 요청을 처리하고, 필요한 데이터를 DTO 형태로 변환하여 서비스 계층으로 전달합니다[1][2].

## **2. DTO에서 엔티티로 변환**

서비스 계층에서는 전달받은 DTO를 엔티티로 변환합니다. 이 변환 과정은 일반적으로 서비스 메서드 내에서 이루어지며, DTO의 데이터를 기반으로 엔티티 객체를 생성합니다. 이때, DTO는 비즈니스 로직을 포함하지 않기 때문에, 단순히 데이터 전송의 역할만 수행합니다[3][4][5].

```java
public void saveUser(UserDTO userDTO) {
    User user = new User();
    user.setName(userDTO.getName());
    user.setEmail(userDTO.getEmail());
    userRepository.save(user);
}
```

## **3. 트랜잭션 관리**

엔티티가 리포지토리를 통해 데이터베이스에 저장될 때, 트랜잭션 관리가 필요합니다. Spring에서는 `@Transactional` 어노테이션을 사용하여 트랜잭션을 관리합니다. 이 어노테이션이 적용된 메서드는 트랜잭션의 시작과 종료를 자동으로 처리하며, 만약 메서드 실행 중 오류가 발생하면 모든 변경 사항이 롤백됩니다[4][5][10].

```java
@Transactional
public void saveUser(UserDTO userDTO) {
    User user = new User();
    user.setName(userDTO.getName());
    user.setEmail(userDTO.getEmail());
    userRepository.save(user);
}
```

## **4. 데이터베이스에 저장**

변환된 엔티티는 리포지토리를 통해 데이터베이스에 저장됩니다. 이 과정에서 엔티티의 상태가 변경되며, 트랜잭션이 성공적으로 완료되면 데이터베이스에 반영됩니다. 만약 트랜잭션이 실패하면, 이전 상태로 롤백되어 데이터의 일관성을 유지합니다[6][10][11].

결론적으로, DTO는 서비스 계층에서 요청을 받아 엔티티로 변환하고, 이를 리포지토리를 통해 데이터베이스에 저장하는 과정에서 중요한 역할을 합니다. 이 과정은 데이터의 무결성과 일관성을 보장하기 위해 트랜잭션 관리와 함께 수행됩니다.
[1] https://www.reddit.com/r/SpringBoot/comments/1j2vy0m/using_dto_in_spring_boot/
[2] https://lsh2016.tistory.com/93
[3] https://curiousjinan.tistory.com/entry/spring-data-transfer-vo-dto
[4] https://www.geeksforgeeks.org/spring-boot-transaction-management-using-transactional-annotation/
[5] https://medium.com/@bubu.tripathy/implementing-transactions-in-a-spring-boot-application-bc6b33e88557
[6] https://velog.io/@arin/Spring-Dto%EC%9D%98-%EC%9E%AC%EC%82%AC%EC%9A%A9%EC%84%B1%EA%B3%BC-%EB%B2%94%EC%9C%84%EC%97%90-%EB%8C%80%ED%95%9C-%EA%B3%A0%EB%AF%BC
[7] https://medium.com/cdri/spring-boot-dto%EB%A5%BC-%ED%99%80%EB%8C%80%ED%95%98%EC%A7%80-%EC%95%8A%EB%8A%94-%EB%B0%A9%EB%B2%95-4d7946050d2a
[8] https://stackoverflow.com/questions/35078383/what-are-the-dao-dto-and-service-layers-in-spring-framework
[9] https://velog.io/@rudwhd515/Springboot-Controller-Service-Repository-%EA%B3%84%EC%B8%B5-%EA%B0%84%EC%9D%98-DTO
[10] https://www.marcobehler.com/guides/spring-transaction-management-transactional-in-depth
[11] https://blog.naver.com/dsz08082/223438064338?fromRss=true&trackingCode=rss
[12] https://softwareengineering.stackexchange.com/questions/400953/service-layer-returns-dto-to-controller-but-need-it-to-return-model-for-other-se
[13] https://docs.spring.io/spring-framework/docs/4.2.x/spring-framework-reference/html/transaction.html
[14] https://www.geeksforgeeks.org/how-to-transfer-data-in-spring-using-dto/
[15] https://dsc-sookmyung.tistory.com/198
[16] https://auth0.com/blog/automatically-mapping-dto-to-entity-on-spring-boot-apis/
[17] https://medium.com/@vishamberlal/understanding-data-transfer-objects-dto-in-spring-boot-ac06b575a1d5
[18] https://dev-jk93.tistory.com/82
[19] https://studyandwrite.tistory.com/433
[20] https://yong0810.tistory.com/57
