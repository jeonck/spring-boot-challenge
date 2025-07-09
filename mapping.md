Spring Boot에서 "매핑"이라는 용어는 주로 두 가지 요소 간의 변환을 의미합니다. 구체적으로, 매핑은 다음과 같은 요소들 간의 관계를 나타냅니다:

1. **Entity to DTO (A to B)**: 
   - **Entity**: 데이터베이스의 테이블과 매핑되는 자바 객체입니다. 예를 들어, `User` 엔티티는 데이터베이스의 `users` 테이블과 연결됩니다.
   - **DTO (Data Transfer Object)**: 클라이언트와 서버 간의 데이터 전송을 위해 사용되는 객체입니다. 예를 들어, `UserDto`는 클라이언트에 전달될 사용자 정보를 담고 있습니다.

   이 경우, 매핑은 `User` 엔티티의 필드를 `UserDto`의 필드로 변환하는 과정을 의미합니다. 예를 들어, `User`의 `username` 필드를 `UserDto`의 `name` 필드로 매핑할 수 있습니다[1][2].

2. **DTO to Entity (B to A)**: 
   - 이 방향의 매핑은 클라이언트로부터 받은 DTO를 데이터베이스에 저장하기 위해 Entity로 변환하는 과정입니다. 예를 들어, `UserDto`의 `name` 필드를 `User` 엔티티의 `username` 필드로 매핑합니다.

3. **다대일 또는 일대다 매핑**: 
   - 여러 개의 소스 객체를 하나의 타겟 객체로 매핑하는 경우도 있습니다. 예를 들어, 여러 `Address` 객체를 하나의 `UserDto`에 매핑할 수 있습니다. 이 경우, 여러 `Address`의 필드를 하나의 `DeliveryAddressDto`로 변환하는 방식입니다[1][2].

4. **복잡한 객체 간의 매핑**: 
   - 객체 내부에 다른 객체가 포함된 경우, 예를 들어 `Car` 객체가 `Engine` 객체를 포함하고 있을 때, `Car`의 `engine` 필드를 `EngineDto`로 매핑하는 방식도 포함됩니다[2][5].

이러한 매핑 과정은 주로 MapStruct와 같은 라이브러리를 통해 자동화되며, 개발자는 매핑 규칙을 정의하는 것만으로 복잡한 변환 로직을 간소화할 수 있습니다.
[1] https://mein-figur.tistory.com/entry/mapstruct-2
[2] https://kimfk567.tistory.com/134
[3] https://velog.io/@choi-ju-yung/Spring-mapper-2%EA%B0%80%EC%A7%80-%EB%B0%A9%EB%B2%95
[4] https://chaelin1211.github.io/study/2021/07/24/model-mapper.html
[5] https://codingdog.tistory.com/entry/spring-boot-mapstruct%EB%A1%9C-mapping%EC%9D%84-%EC%86%90%EC%89%BD%EA%B2%8C-%ED%95%B4-%EB%B4%85%EC%8B%9C%EB%8B%A4
[6] https://2ye-eun.tistory.com/37
[7] https://record1996.tistory.com/135
[8] https://m.blog.naver.com/qjawnswkd/222421554202
[9] https://bepoz-study-diary.tistory.com/412
[10] https://moonhy7.tistory.com/entry/Spring-2%EC%9E%A5-Mapper-XML-%ED%8C%8C%EC%9D%BC-%EC%84%A4%EC%A0%95
[11] https://twofootdog.github.io/Spring-DAO%EC%99%80-Mapper%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90/
[12] https://devlog-wjdrbs96.tistory.com/200
[13] https://coder-in-war.tistory.com/entry/SpringBoot-11-ModelMapper-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC-%EC%9D%B4%EC%9A%A9%ED%95%98%EA%B8%B0
[14] https://mybatis.org/mybatis-3/ko/sqlmap-xml.html
[15] https://velog.io/@doridam1116/MyBatis-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0-Spring-Boot-%EC%97%B0%EB%8F%99-%EB%B0%8F-%ED%99%98%EA%B2%BD-%EC%84%A4%EC%A0%95
[16] https://velog.io/@jungnoeun/%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8%EC%97%90-DB%EC%97%B0%EA%B2%B0-0xho523e
[17] https://dalpaeng00.tistory.com/83
[18] https://gdngy.tistory.com/122
[19] https://velog.io/@seulki971227/Spring-Boot-Mapper-Interface-%EC%83%9D%EC%84%B1-Mapper-%EC%9E%91%EC%84%B1%ED%95%98%EA%B8%B0
[20] https://jaeano.tistory.com/entry/Spring-Boot-Repository-MyBatis-Mapper-Domain
[21] https://beaniejoy.tistory.com/55
[22] https://jung-story.tistory.com/128
[23] https://velog.io/@letsdev/MapStruct-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EB%B3%80%ED%99%98-1-%EA%B8%B0%EB%B3%B8-%EA%B0%9C%EB%85%90%EA%B3%BC-%EC%BD%94%EB%93%9C
[24] https://lob-dev.tistory.com/56
[25] https://jangjjolkit.tistory.com/42
[26] https://srk911028.tistory.com/209
[27] https://zzang9ha.tistory.com/420
[28] https://lims-dev.tistory.com/45
