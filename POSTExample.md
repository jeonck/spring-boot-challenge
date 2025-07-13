스프링부트로 REST API를 구현하는 프로젝트의 전체 구조를 업데이트하고, 필요한 코드와 함께 프로젝트 트리를 포함하겠습니다. 이 예시는 사용자 정보를 처리하는 API를 기반으로 하며, Entity, DTO, Repository, Service, Controller를 포함합니다.

## **프로젝트 구조**

```
rest-api
│
├── src
│   ├── main
│   │   ├── java
│   │   │   └── com
│   │   │       └── example
│   │   │           └── restapi
│   │   │               ├── controller
│   │   │               │   └── UserController.java
│   │   │               ├── dto
│   │   │               │   └── UserDto.java
│   │   │               ├── entity
│   │   │               │   └── User.java
│   │   │               ├── repository
│   │   │               │   └── UserRepository.java
│   │   │               ├── service
│   │   │               │   └── UserService.java
│   │   │               └── DemoApplication.java
│   │   └── resources
│   │       └── application.properties
│   └── test
│       └── java
│           └── com
│               └── example
│                   └── restapi
│                       └── UserControllerTest.java
└── pom.xml
```

## **1. Entity 클래스**

`User.java` - 데이터베이스에 저장할 사용자 정보를 정의합니다.

```java
package com.example.restapi.entity;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String userName;
    private String phoneNumber;
    private int acceptCount;

    // Getter와 Setter 메서드
    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getUserName() {
        return userName;
    }

    public void setUserName(String userName) {
        this.userName = userName;
    }

    public String getPhoneNumber() {
        return phoneNumber;
    }

    public void setPhoneNumber(String phoneNumber) {
        this.phoneNumber = phoneNumber;
    }

    public int getAcceptCount() {
        return acceptCount;
    }

    public void setAcceptCount(int acceptCount) {
        this.acceptCount = acceptCount;
    }
}
```

## **2. DTO 클래스**

`UserDto.java` - 클라이언트로부터 받을 JSON 데이터를 매핑합니다.

```java
package com.example.restapi.dto;

public class UserDto {
    private String userName;
    private String phoneNumber;
    private int acceptCount;

    // Getter와 Setter 메서드
    public String getUserName() {
        return userName;
    }

    public void setUserName(String userName) {
        this.userName = userName;
    }

    public String getPhoneNumber() {
        return phoneNumber;
    }

    public void setPhoneNumber(String phoneNumber) {
        this.phoneNumber = phoneNumber;
    }

    public int getAcceptCount() {
        return acceptCount;
    }

    public void setAcceptCount(int acceptCount) {
        this.acceptCount = acceptCount;
    }
}
```

## **3. Repository 인터페이스**

`UserRepository.java` - JPA를 사용하여 데이터베이스와 상호작용합니다.

```java
package com.example.restapi.repository;

import com.example.restapi.entity.User;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface UserRepository extends JpaRepository<User, Long> {
}
```

## **4. 서비스 클래스**

`UserService.java` - 비즈니스 로직을 처리합니다.

```java
package com.example.restapi.service;

import com.example.restapi.dto.UserDto;
import com.example.restapi.entity.User;
import com.example.restapi.repository.UserRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class UserService {
    @Autowired
    private UserRepository userRepository;

    public User createUser(UserDto userDto) {
        User user = new User();
        user.setUserName(userDto.getUserName());
        user.setPhoneNumber(userDto.getPhoneNumber());
        user.setAcceptCount(userDto.getAcceptCount());
        return userRepository.save(user);
    }
}
```

## **5. 컨트롤러 클래스**

`UserController.java` - HTTP 요청을 처리합니다.

```java
package com.example.restapi.controller;

import com.example.restapi.dto.UserDto;
import com.example.restapi.entity.User;
import com.example.restapi.service.UserService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api/users")
public class UserController {
    @Autowired
    private UserService userService;

    @PostMapping("/create")
    public String createUser(@RequestBody UserDto userDto) {
        User createdUser = userService.createUser(userDto);
        return "User created successfully with ID: " + createdUser.getId();
    }
}
```

## **6. 애플리케이션 시작 클래스**

`DemoApplication.java` - 스프링 부트 애플리케이션의 시작점입니다.

```java
package com.example.restapi;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class DemoApplication {
    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}
```

## **7. 설정 파일**

`application.properties` - 데이터베이스 연결 및 기타 설정을 정의합니다.

```properties
spring.h2.console.enabled=true
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=password
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
```

## **8. 테스트 클래스**

`UserControllerTest.java` - 컨트롤러의 테스트를 위한 클래스입니다.

```java
package com.example.restapi;

import com.example.restapi.controller.UserController;
import com.example.restapi.dto.UserDto;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.AutoConfigureMockMvc;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.http.MediaType;
import org.springframework.test.web.servlet.MockMvc;

import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.post;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;

@SpringBootTest
@AutoConfigureMockMvc
public class UserControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @Test
    public void testCreateUser() throws Exception {
        UserDto userDto = new UserDto();
        userDto.setUserName("JohnDoe");
        userDto.setPhoneNumber("123-456-7890");
        userDto.setAcceptCount(5);

        mockMvc.perform(post("/api/users/create")
                .contentType(MediaType.APPLICATION_JSON)
                .content("{\"userName\":\"JohnDoe\",\"phoneNumber\":\"123-456-7890\",\"acceptCount\":5}"))
                .andExpect(status().isOk());
    }
}
```

이 구조를 통해 스프링부트에서 REST API를 구현하는 데 필요한 모든 요소를 포함한 프로젝트를 구성할 수 있습니다. 각 클래스는 명확한 역할을 가지고 있으며, 프로젝트의 유지보수성과 확장성을 높이는 데 기여합니다.
[1] https://ws-pace.tistory.com/70
[2] https://codefinity.com/courses/v2/87dc501e-89a6-4a4b-afd4-8b38c46a80c7/9a2cd386-7414-4da6-a5ba-c79732024d97/c5672c70-6af2-4164-ad97-b6205befa155
[3] https://velog.io/@msung99/SpringBoot-RestAPI-Structure-%EA%B5%AC%EC%84%B1
[4] https://codingnomads.com/java-spring-project-structure-best-practices
[5] https://bkjo94.tistory.com/entry/%EC%8A%A4%ED%94%84%EB%A7%81-%EB%B6%80%ED%8A%B8Spring-Boot%EB%A5%BC-%ED%99%9C%EC%9A%A9%ED%95%9C-POST-REST-API-%EA%B5%AC%ED%98%84
[6] https://medium.com/@pratik.941/building-rest-api-using-spring-boot-a-comprehensive-guide-3e9b6d7a8951
[7] https://malshani-wijekoon.medium.com/spring-boot-folder-structure-best-practices-18ef78a81819
[8] https://johnconomics.tistory.com/entry/SpringBoot-Springboot-POST-API-%EA%B5%AC%ED%98%84%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95
[9] https://symflower.com/en/company/blog/2024/spring-boot-folder-structure/
[10] https://m.blog.naver.com/sosow0212/222521103062
[11] https://www.geeksforgeeks.org/advance-java/easiest-way-to-create-rest-api-using-spring-boot/
[12] https://creamilk88.tistory.com/184
[13] https://camunda.com/blog/2025/05/how-to-build-a-rest-api-with-spring-boot-a-step-by-step-guide/
[14] https://bcuts.tistory.com/153
[15] https://velog.io/@win-luck/Springboot-%EC%8A%A4%ED%94%84%EB%A7%81-API-%EA%B5%AC%ED%98%84-%EC%BB%A4%EC%8A%A4%ED%85%80-%EC%9D%91%EB%8B%B5%EA%B0%9D%EC%B2%B4-REST-API-HttpsCode-GlobalExceptionHandler
[16] https://velog.io/@seongwon97/Spring-Boot-POST-API
[17] https://ayoteralab.tistory.com/entry/Spring-Boot-28-REST-API-4-POST-method-%EC%99%80-Content-Type
[18] https://stackoverflow.com/questions/40902280/what-is-the-recommended-project-structure-for-spring-boot-rest-projects
[19] https://spring.io/guides/tutorials/rest
[20] https://pepega.tistory.com/4
[21] https://assu10.github.io/dev/2023/09/23/springboot-rest-api-request/
[22] https://kdyspring.tistory.com/44
[23] https://hereishyun.tistory.com/67
[24] https://blog.naver.com/writer0713/221853596497
[25] https://diary-developer.tistory.com/10
[26] https://joo0jae.tistory.com/374
[27] https://velog.io/@hyeok_1212/GDSC-Spring-Boot%EB%A1%9C-REST-API-%EB%A7%8C%EB%93%A4%EC%96%B4%EB%B3%B4%EA%B8%B0
[28] https://ococ99.tistory.com/177
