RestClientCustomizer는 Spring Boot에서 RestClient.Builder를 커스터마이징하는 데 사용되는 인터페이스입니다. 이를 통해 RestClient의 설정을 전역적으로 조정할 수 있습니다. 아래는 RestClientCustomizer를 사용하는 간단한 예시입니다.

### **예시 코드**

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.Bean;
import org.springframework.http.client.HttpComponentsClientHttpRequestFactory;
import org.springframework.web.client.RestClient;
import org.springframework.web.client.RestClientCustomizer;

@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

    @Bean
    public RestClientCustomizer customRestClientCustomizer() {
        return new RestClientCustomizer() {
            @Override
            public void customize(RestClient.Builder restClientBuilder) {
                // 기본 URL 설정
                restClientBuilder.baseUrl("http://localhost:8080");
                
                // 타임아웃 설정
                restClientBuilder.setRequestFactory(new HttpComponentsClientHttpRequestFactory());
            }
        };
    }
}
```

### **설명**

1. **Spring Boot 애플리케이션 설정**: `@SpringBootApplication` 애너테이션을 사용하여 Spring Boot 애플리케이션을 설정합니다.

2. **RestClientCustomizer 빈 등록**: `customRestClientCustomizer` 메서드에서 `RestClientCustomizer`를 구현하여 RestClient.Builder의 설정을 커스터마이즈합니다. 여기서는 기본 URL을 `http://localhost:8080`으로 설정하고, `HttpComponentsClientHttpRequestFactory`를 사용하여 요청 팩토리를 설정합니다.

3. **RestClient 사용**: 이 커스터마이저를 통해 생성된 RestClient는 모든 HTTP 요청에 대해 기본 URL과 요청 팩토리를 자동으로 적용받습니다.

이와 같이 RestClientCustomizer를 사용하면 애플리케이션 전역에서 RestClient의 설정을 일관되게 관리할 수 있습니다.
[1] https://shyun00.tistory.com/225
[2] https://github.com/spring-projects/spring-boot/issues/38832
[3] https://docs.spring.io/spring-boot/reference/io/rest-client.html
[4] https://stackoverflow.com/questions/79345220/spring-boot-3-4-new-feature-how-to-config-sslbundle-works-with-restclient
[5] https://docs.spring.io/spring-boot/api/java/org/springframework/boot/test/web/client/MockServerRestClientCustomizer.html
[6] https://docs.spring.vmware.com/spring-boot/docs/3.2.13.2/api/org/springframework/boot/test/web/client/MockServerRestClientCustomizer.html
[7] https://javadzone.com/restclient-in-spring-6-with-examples/
[8] https://junjangsee.tistory.com/entry/springboot-restclient-customizing
[9] https://codewithsibin.com/spring-boot-restclient-tutorial-setup-authentication-error-handling-advanced-usage/
[10] https://codefarm0.medium.com/restclient-in-spring-boot-3-x-with-code-examples-fde52540796d
[11] https://www.baeldung.com/spring-boot-restclient
[12] https://docs.spring.io/spring-framework/reference/integration/rest-clients.html
[13] https://github.com/spring-projects/spring-boot/issues/38500
[14] https://dev.to/noelopez/new-restclient-in-spring-61-10ac
[15] https://kkambi.tistory.com/142
