오라클 데이터베이스와 연결된 Spring Boot 애플리케이션을 Gradle 빌드 방식으로 설정하는 방법에 대해 설명하겠습니다. 이 예제에서는 Spring Data JPA를 사용하여 RESTful API를 구축합니다.

## **1. Gradle 프로젝트 설정**

### **1.1. build.gradle 파일 설정**

`build.gradle` 파일에 필요한 의존성을 추가합니다. 아래는 Oracle JDBC 드라이버와 Spring Boot 관련 의존성을 포함한 예시입니다.

```groovy
plugins {
    id 'org.springframework.boot' version '3.0.0'
    id 'io.spring.dependency-management' version '1.0.11.RELEASE'
    id 'java'
}

group = 'com.example'
version = '0.0.1-SNAPSHOT'
sourceCompatibility = '17'

repositories {
    mavenCentral()
}

dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
    implementation 'org.springframework.boot:spring-boot-starter-web'
    runtimeOnly 'com.oracle.database.jdbc:ojdbc8:19.8.0.0' // Oracle JDBC 드라이버
    testImplementation 'org.springframework.boot:spring-boot-starter-test'
}
```

### **1.2. 데이터베이스 설정**

`src/main/resources/application.properties` 파일에 데이터베이스 연결 정보를 추가합니다.

```properties
spring.datasource.url=jdbc:oracle:thin:@localhost:1521:xe
spring.datasource.username=your_username
spring.datasource.password=your_password
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
```

여기서 `your_username`과 `your_password`는 오라클 데이터베이스의 사용자 이름과 비밀번호로 변경해야 합니다.

## **2. 엔티티 클래스 생성**

예를 들어, `Customer`라는 엔티티 클래스를 생성합니다.

```java
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

@Entity
public class Customer {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private String email;

    // Getters and Setters
}
```

## **3. 레포지토리 인터페이스 생성**

Spring Data JPA를 사용하여 데이터베이스와 상호작용할 레포지토리 인터페이스를 생성합니다.

```java
import org.springframework.data.jpa.repository.JpaRepository;

public interface CustomerRepository extends JpaRepository<Customer, Long> {
}
```

## **4. REST 컨트롤러 생성**

이제 REST API를 제공할 컨트롤러를 생성합니다.

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/api/customers")
public class CustomerController {
    @Autowired
    private CustomerRepository customerRepository;

    @GetMapping
    public List<Customer> getAllCustomers() {
        return customerRepository.findAll();
    }

    @PostMapping
    public Customer createCustomer(@RequestBody Customer customer) {
        return customerRepository.save(customer);
    }
}
```

## **5. 애플리케이션 실행**

이제 Spring Boot 애플리케이션을 실행하면, `/api/customers` 엔드포인트를 통해 고객 정보를 조회하고 추가할 수 있습니다.

### **6. Postman으로 테스트하기**

- **GET 요청**: `http://localhost:8080/api/customers`에 GET 요청을 보내면 모든 고객 정보를 조회할 수 있습니다.
- **POST 요청**: `http://localhost:8080/api/customers`에 고객 정보를 JSON 형식으로 포함하여 POST 요청을 보내면 새로운 고객이 추가됩니다.

```json
{
    "name": "John Doe",
    "email": "john.doe@example.com"
}
```

이렇게 하면 Gradle 빌드 방식으로 오라클 데이터베이스에 연결된 간단한 Spring Boot REST API를 구축할 수 있습니다.
[1] https://github.com/shawn-mcginty/spring-boot-oracle-example/blob/master/build.gradle
[2] https://www.codejava.net/frameworks/spring-boot/connect-to-oracle-database-examples
[3] https://azurealstn.tistory.com/83
[4] https://velog.io/@seulki412/Spring-Boot-%EC%98%A4%EB%9D%BC%ED%81%B4-DB-%EC%97%B0%EA%B2%B0%ED%95%98%EA%B8%B0-JDBC-gradle-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC-%EC%B6%94%EA%B0%80-%EC%9D%B8%EC%BD%94%EB%94%A9-%EC%BB%A4%EB%84%A5%EC%85%98%EC%84%A4%EC%A0%95
[5] https://verycrazy.tistory.com/88
[6] https://www.baeldung.com/spring-oracle-connection-pooling
[7] https://velog.io/@vegayes/Spring-BootTIL-no.70-2023.11.09
[8] https://medium.com/@ishinihettiarachchiuv/how-to-connect-a-spring-boot-project-and-oracle-db-locally-and-create-tables-using-the-jpa-f0e1891ef470
[9] https://www.springboottutorial.com/spring-boot-with-mysql-and-oracle
[10] https://m.blog.naver.com/PostView.naver?blogId=626ksb&logNo=222319536114
[11] https://docs.spring.io/spring-boot/gradle-plugin/running.html
[12] https://chillin-dev.tistory.com/38
[13] https://developerson.tistory.com/112
[14] https://stackoverflow.com/questions/58160999/spring-boot-oracle-gradle-cannot-load-driver-class-oracle-jdbc-oracledriver
[15] https://stackoverflow.com/questions/54305348/how-to-connect-to-oracle-database-using-spring-boot
[16] https://www.oracle.com/database/spring-boot/
[17] https://www.cdata.com/kb/tech/oracledb-jdbc-spring-boot.rst
[18] https://apexapps.oracle.com/pls/apex/f?p=44785:112:1023757009042::::P112_CONTENT_ID,P112_PREV_PAGE:17698
[19] https://wugawuga.tistory.com/7
[20] https://gwamssoju.tistory.com/57
[21] https://blogs.oracle.com/developers/post/hikaricp-best-practices-for-oracle-database-and-spring-boot
[22] https://programmer93.tistory.com/24
[23] https://www.oracle.com/apac/database/spring-boot/
[24] https://simplifyingtechcode.wordpress.com/2023/12/26/spring-boot-hibernate-jpa-oracle-db-rest-crud-example/
[25] https://stackoverflow.com/questions/37783669/how-to-add-ojdbc7-to-java-web-app-by-gradle/41525769
[26] https://discuss.gradle.org/t/gradle-catalog-does-not-work-correctly-with-spring-boot-project/46666
[27] https://hye0-log.tistory.com/24
[28] https://devpad.tistory.com/106
[29] https://congsong.tistory.com/46
[30] https://jonghyeok-dev.tistory.com/21
[31] https://sycdev.tistory.com/entry/Spring-Boot-REST-API-%EB%A7%8C%EB%93%A4%EA%B8%B0-3-MySQL-JDBC-Template
[32] https://medium.com/@stevriss22/connecting-spring-boot-microservice-to-oracle-datasource-aae33008643a
[33] https://github.com/spring-projects/spring-boot/blob/main/spring-boot-project/spring-boot/build.gradle
[34] https://haaland09009.tistory.com/417
