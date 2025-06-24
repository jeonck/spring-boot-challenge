Spring Boot에서 FastAPI처럼 Swagger를 설정하여 API 문서를 자동으로 생성하고 테스트할 수 있는 방법에 대해 설명하겠습니다. FastAPI는 Swagger UI를 기본적으로 제공하여 API 문서를 쉽게 생성할 수 있지만, Spring Boot에서도 비슷한 기능을 구현할 수 있습니다.

## **1. Gradle 의존성 추가**

Spring Boot 프로젝트의 `build.gradle` 파일에 Swagger 관련 의존성을 추가합니다. Spring Boot 3.x 버전에서는 `springdoc-openapi` 라이브러리를 사용하는 것이 일반적입니다.

```groovy
dependencies {
    implementation 'org.springdoc:springdoc-openapi-starter-webmvc-ui:2.0.2' // Swagger UI
}
```

## **2. Swagger 설정 클래스 작성**

Swagger를 사용하기 위한 설정 클래스를 작성합니다. 이 클래스는 API 문서의 기본 정보를 설정합니다.

```java
import io.swagger.v3.oas.models.OpenAPI;
import io.swagger.v3.oas.models.info.Info;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class SwaggerConfig {

    @Bean
    public OpenAPI customOpenAPI() {
        return new OpenAPI()
                .info(new Info()
                        .title("My API")
                        .version("1.0")
                        .description("API documentation for my application"));
    }
}
```

## **3. API 엔드포인트에 Swagger 어노테이션 추가**

각 API 엔드포인트에 Swagger 어노테이션을 추가하여 문서화합니다. 예를 들어, 다음과 같이 사용할 수 있습니다.

```java
import io.swagger.v3.oas.annotations.Operation;
import io.swagger.v3.oas.annotations.Parameter;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api")
public class MyController {

    @Operation(summary = "Get user by ID", description = "Retrieve user details by user ID")
    @GetMapping("/users/{id}")
    public User getUserById(@Parameter(description = "ID of the user to be retrieved") @PathVariable Long id) {
        // 사용자 조회 로직
        return new User(id, "John Doe");
    }
}
```

## **4. Swagger UI 접근**

애플리케이션을 실행한 후, Swagger UI에 접근하려면 브라우저에서 다음 URL을 입력합니다:

```
http://localhost:8080/swagger-ui/index.html
```

여기서 API 문서와 함께 각 엔드포인트를 테스트할 수 있는 UI가 제공됩니다.

## **5. 추가 설정 (선택 사항)**

Swagger UI의 동작 방식을 추가로 설정하고 싶다면, `application.properties` 파일에 다음과 같은 설정을 추가할 수 있습니다.

```properties
springdoc.swagger-ui.path=/swagger-ui.html
springdoc.api-docs.path=/v3/api-docs
```

이렇게 하면 Swagger UI와 API 문서의 경로를 사용자 정의할 수 있습니다.

## **결론**

이와 같이 Spring Boot에서 FastAPI처럼 Swagger를 설정하여 API 문서를 자동으로 생성하고 테스트할 수 있습니다. Swagger UI를 통해 API의 사용법을 쉽게 이해하고, 직접 테스트할 수 있는 환경을 제공받게 됩니다.
[1] https://infinitecode.tistory.com/65
[2] https://www.reddit.com/r/golang/comments/16e9o5u/why_doesnt_golang_have_easy_api_swagger_docs_like/
[3] https://m.blog.naver.com/seek316/222706591090
[4] https://medium.com/@berktorun.dev/swagger-like-a-pro-with-spring-boot-3-and-java-17-49eed0ce1d2f
[5] https://velog.io/@koeunyeon/FastAPI-%EC%8D%A8-%EB%B3%B8-%ED%9B%84%EA%B8%B0
[6] https://bell-sw.com/blog/documenting-rest-api-with-swagger-in-spring-boot-3/
[7] https://sjh9708.tistory.com/169
[8] https://www.theserverside.com/blog/Coffee-Talk-Java-News-Stories-and-Opinions/swagger-spring-boot-url-openapi-rest-api-document-java-tutorial-ui
[9] https://kim-jong-hyun.tistory.com/49
[10] https://kafcamus.tistory.com/43
[11] https://stackoverflow.com/questions/74614369/how-to-run-swagger-3-on-spring-boot-3
[12] https://fastapi.tiangolo.com/how-to/configure-swagger-ui/
[13] https://jeonyoungho.github.io/posts/Open-API-3.0-Swagger-v3-%EC%83%81%EC%84%B8%EC%84%A4%EC%A0%95/
[14] https://hogwart-scholars.tistory.com/entry/Spring-Boot-SpringDoc%EA%B3%BC-Swagger%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%B4-API-%EB%AC%B8%EC%84%9C%ED%99%94-%EC%9E%90%EB%8F%99%ED%99%94%ED%95%98%EA%B8%B0
[15] https://www.theserverside.com/video/OpenAPI-Swagger-and-Spring-Boot-REST-APIs
[16] https://lucas-owner.tistory.com/28
[17] https://www.geeksforgeeks.org/spring-boot-rest-api-documentation-using-swagger/
[18] https://forum.flowable.org/t/how-to-expose-swagger-docs-with-spring-boot/12108
