**RestClientCustomizer**는 Spring Boot 3.2 이상에서 제공되는 기능으로, RestClient의 설정을 사용자 정의할 수 있는 인터페이스입니다. 이 인터페이스를 사용하면 RestClient.Builder 인스턴스를 커스터마이즈할 수 있으며, 이를 통해 다양한 HTTP 요청의 동작을 조정할 수 있습니다.

## **주요 기능**

- **커스터마이징 메서드**: `RestClientCustomizer` 인터페이스는 `customize(RestClient.Builder restClientBuilder)` 메서드를 포함하고 있습니다. 이 메서드는 RestClient.Builder 인스턴스를 매개변수로 받아, 사용자가 원하는 대로 설정을 변경할 수 있도록 합니다[1].

- **유연한 설정**: 이 기능을 통해 개발자는 HTTP 메시지 변환기, 요청 팩토리, 인터셉터 등 다양한 구성 요소를 쉽게 추가하거나 수정할 수 있습니다. 예를 들어, 특정 헤더를 추가하거나 기본 URL을 설정하는 등의 작업을 수행할 수 있습니다.

- **람다 표현식 지원**: `RestClientCustomizer`는 함수형 인터페이스로, 람다 표현식이나 메서드 참조를 사용하여 간편하게 구현할 수 있습니다. 이는 코드의 가독성을 높이고, 커스터마이징 작업을 더 직관적으로 만들어 줍니다[1].

## **사용 예시**

다음은 `RestClientCustomizer`를 사용하여 RestClient를 커스터마이즈하는 간단한 예시입니다:

```java
@Bean
public RestClientCustomizer customizer() {
    return restClientBuilder -> {
        restClientBuilder.defaultHeader("Authorization", "Bearer your_token");
        restClientBuilder.baseUrl("https://api.example.com");
    };
}
```

위의 예시에서 `RestClientCustomizer`를 사용하여 기본 URL과 인증 헤더를 설정하고 있습니다. 이러한 방식으로 RestClient의 동작을 유연하게 조정할 수 있습니다.

## **결론**

RestClientCustomizer는 Spring Boot에서 RestClient의 설정을 간편하게 조정할 수 있는 유용한 도구입니다. 이를 통해 개발자는 HTTP 요청의 동작을 세밀하게 제어할 수 있으며, 다양한 요구 사항에 맞춰 클라이언트를 최적화할 수 있습니다.
[1] https://docs.spring.io/spring-boot/api/java/org/springframework/boot/web/client/RestClientCustomizer.html
[2] https://ict-nroo.tistory.com/119
[3] https://junjangsee.tistory.com/entry/springboot-restclient-customizing
[4] https://heewon26.tistory.com/136
[5] https://www.baeldung.com/spring-boot-restclient
[6] https://stackoverflow.com/questions/78444230/how-to-change-the-restclient-implementation-for-springai
[7] https://www.geeksforgeeks.org/advance-java/a-guide-to-restclient-in-spring-boot/
[8] https://kkambi.tistory.com/142
[9] https://docs.spring.io/spring-framework/reference/integration/rest-clients.html
[10] https://codefarm0.medium.com/restclient-in-spring-boot-3-x-with-code-examples-fde52540796d
[11] https://foojay.io/today/spring-internals-of-restclient/
[12] https://hhlin.tistory.com/142
[13] https://m.blog.naver.com/seek316/223327989579
[14] https://junjangsee.tistory.com/entry/springboot-restclient
[15] https://eunveloper.tistory.com/entry/WAS-Spring-Boot-DB-%EC%84%B1%EB%8A%A5-%EA%B0%9C%EC%84%A0%EA%B3%BC-%EC%B5%9C%EC%A0%81%ED%99%94-3-RestClient
[16] https://velog.io/@rookedsysc/Spring%EC%97%90%EC%84%9C-%EC%99%B8%EB%B6%80-API-%EC%9A%94%EC%B2%ADRestClient-Object-Mapping
[17] https://codefarm0.medium.com/restclient-internal-architecture-in-spring-boot-3-2-fb43f7c5fec7
[18] https://tychejin.tistory.com/467
[19] https://stackoverflow.com/questions/79345220/spring-boot-3-4-new-feature-how-to-config-sslbundle-works-with-restclient
[20] https://www.codingshuttle.com/spring-boot-handbook/rest-client
