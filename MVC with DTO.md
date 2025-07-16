스프링 부트(Spring Boot)에서 가장 간단한 DTO(Data Transfer Object)를 포함하는 예제를 소개하겠습니다. DTO는 계층 간 데이터 전송을 위한 객체로, 주로 비즈니스 로직을 가지지 않고 데이터만을 포함합니다.

## **1. User 엔티티 클래스**

먼저, 데이터베이스와 매핑되는 `User` 엔티티 클래스를 정의합니다:

```java
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String username;
    private String email;

    // Getters and Setters
    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }
}
```

## **2. UserDTO 클래스**

다음으로, `User` 엔티티와 매핑되는 DTO 클래스를 정의합니다:

```java
public class UserDTO {
    private String username;
    private String email;

    // Getters and Setters
    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }
}
```

## **3. UserController 클래스**

이제 컨트롤러를 작성하여 클라이언트의 요청을 처리하고 DTO를 사용하여 데이터를 전송합니다:

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/users")
public class UserController {

    @Autowired
    private UserService userService;

    @PostMapping
    public ResponseEntity<UserDTO> createUser(@RequestBody UserDTO userDTO) {
        User user = userService.createUser(userDTO);
        return ResponseEntity.ok(convertToDTO(user));
    }

    private UserDTO convertToDTO(User user) {
        UserDTO userDTO = new UserDTO();
        userDTO.setUsername(user.getUsername());
        userDTO.setEmail(user.getEmail());
        return userDTO;
    }
}
```

## **4. UserService 클래스**

서비스 클래스에서 DTO를 사용하여 비즈니스 로직을 처리합니다:

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class UserService {

    @Autowired
    private UserRepository userRepository;

    public User createUser(UserDTO userDTO) {
        User user = new User();
        user.setUsername(userDTO.getUsername());
        user.setEmail(userDTO.getEmail());
        return userRepository.save(user);
    }
}
```

## **결론**

이 예제에서는 `User` 엔티티와 `UserDTO`를 정의하고, 컨트롤러와 서비스에서 DTO를 사용하여 데이터를 전송하는 방법을 보여주었습니다. DTO를 사용함으로써 데이터 전송의 효율성을 높이고, 비즈니스 로직과 데이터 구조를 분리하여 코드의 유지보수성을 향상시킬 수 있습니다[1][2][3].
[1] https://realabishan.medium.com/data-transfer-object-dto-spring-mvc-506cd5340764
[2] https://medium.com/@vishamberlal/understanding-data-transfer-objects-dto-in-spring-boot-ac06b575a1d5
[3] https://www.geeksforgeeks.org/java/data-transfer-object-dto-in-spring-mvc-with-example/
[4] https://www.reddit.com/r/SpringBoot/comments/14v304k/how_do_dtos_make_sense_a_cry_for_an_explained/
[5] https://idkim97.github.io/2023-08-15-DAO,%20DTO,%20VO,%20Entity%EB%9E%80/
[6] https://velog.io/@rhee519/DAO-DTO-Entity-class
[7] https://e-una.tistory.com/72
[8] https://velog.io/@phjppo0918/%E5%88%9D%E5%BF%83-Spring-Boot-%EC%98%88%EC%A0%9C%EB%A5%BC-%ED%86%B5%ED%95%B4-MVC-%ED%8C%A8%ED%84%B4-%EC%84%A4%EA%B3%84
[9] https://code-lab1.tistory.com/201
[10] https://www.javaguides.net/2021/02/spring-boot-dto-example-entity-to-dto.html
[11] https://zeuskwon-ds.tistory.com/55
[12] https://www.javaguides.net/2022/12/spring-boot-dto-example-tutorial.html
[13] https://www.baeldung.com/java-dto-pattern
[14] https://medium.com/@roshanfarakate/understanding-dtos-in-spring-boot-a-comprehensive-guide-20e2b8101ee6
[15] https://pupbani.tistory.com/256
[16] https://www.geeksforgeeks.org/java/spring-boot-map-entity-to-dto-using-modelmapper/
[17] https://www.baeldung.com/entity-to-and-from-dto-for-a-java-spring-application
[18] https://blog.naver.com/ncbomb/223297380275?viewType=pc
[19] https://stackoverflow.com/questions/58859348/where-to-put-entity-to-dto-transformation-in-a-spring-boot-project
