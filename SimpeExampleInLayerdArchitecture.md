레이어드 아키텍처에서 데이터 흐름은 프레젠테이션 레이어부터 시작하여 비즈니스 레이어, 퍼시스턴스 레이어, 그리고 데이터베이스 레이어로 이어집니다. 각 레이어는 특정한 역할을 수행하며, 요청이 상위 레이어에서 하위 레이어로 흐르는 구조를 가지고 있습니다. 아래는 각 레이어의 역할과 데이터 흐름을 설명합니다.

## 1. 프레젠테이션 레이어 (Presentation Layer)

- **역할**: 사용자 인터페이스와 상호작용하며, 클라이언트의 요청을 수신합니다. 요청을 처리하기 위해 비즈니스 레이어에 전달합니다.
- **예시**: REST API의 컨트롤러 클래스가 이 레이어에 해당합니다.

```java
@RestController
@RequestMapping("/todos")
public class TodoController {
    @Autowired
    private TodoService service;

    @GetMapping
    public ResponseEntity<List<TodoEntity>> getAllTodos() {
        return ResponseEntity.ok(service.getAllTodos());
    }

    @PostMapping
    public ResponseEntity<TodoEntity> createTodo(@RequestBody TodoEntity todo) {
        return ResponseEntity.ok(service.createTodo(todo));
    }
}
```

## 2. 비즈니스 레이어 (Business Layer)

- **역할**: 애플리케이션의 비즈니스 로직을 처리합니다. 프레젠테이션 레이어로부터 요청을 받아 필요한 데이터 처리를 수행하고, 퍼시스턴스 레이어에 데이터 요청을 전달합니다.
- **예시**: 서비스 클래스가 이 레이어에 해당합니다.

```java
@Service
public class TodoService {
    @Autowired
    private TodoRepository repository;

    public List<TodoEntity> getAllTodos() {
        return repository.findAll();
    }

    public TodoEntity createTodo(TodoEntity todo) {
        return repository.save(todo);
    }
}
```

## 3. 퍼시스턴스 레이어 (Persistence Layer)

- **역할**: 데이터베이스와의 상호작용을 담당합니다. 비즈니스 레이어로부터 요청을 받아 데이터베이스에 CRUD 작업을 수행합니다.
- **예시**: JPA를 사용하는 레포지토리 인터페이스가 이 레이어에 해당합니다.

```java
@Repository
public interface TodoRepository extends JpaRepository<TodoEntity, Long> {
}
```

## 4. 데이터베이스 레이어 (Database Layer)

- **역할**: 실제 데이터가 저장되는 곳으로, 퍼시스턴스 레이어에서 요청한 데이터를 저장하거나 조회합니다. 이 레이어는 데이터베이스 관리 시스템(DBMS)에 해당합니다.

### 데이터 흐름 요약

1. **클라이언트 요청**: 클라이언트가 프레젠테이션 레이어에 요청을 보냅니다.
2. **프레젠테이션 레이어**: 요청을 수신하고 비즈니스 레이어에 전달합니다.
3. **비즈니스 레이어**: 요청을 처리하고 필요한 경우 퍼시스턴스 레이어에 데이터 요청을 보냅니다.
4. **퍼시스턴스 레이어**: 데이터베이스와 상호작용하여 데이터를 저장하거나 조회합니다.
5. **데이터베이스 레이어**: 실제 데이터가 저장되는 곳으로, 요청에 따라 데이터를 반환합니다.
6. **응답 반환**: 데이터가 다시 비즈니스 레이어를 거쳐 프레젠테이션 레이어로 전달되고, 최종적으로 클라이언트에게 응답됩니다.

이러한 구조는 각 레이어가 독립적으로 개발 및 유지보수될 수 있도록 하여, 코드의 재사용성과 유지보수성을 높이는 데 기여합니다.
[1] https://softwareengineering.stackexchange.com/questions/356632/understanding-the-data-flow-in-spring-rest-layered-architecture
[2] https://levelup.gitconnected.com/how-to-differentiate-business-and-service-layers-in-layered-architecture-912123b2ccf1
[3] https://www.oreilly.com/library/view/software-architecture-patterns/9781491971437/ch01.html
[4] https://github.com/alexplesoiu/LayeredArchitecture-Example
[5] https://medium.com/@sagar.hudge/layers-in-software-architecture-c8cc16329ff6
[6] https://dev.to/yasmine_ddec94f4d4/understanding-the-layered-architecture-pattern-a-comprehensive-guide-1e2j
[7] https://openmaker.tistory.com/133
[8] https://velog.io/@yisuho/%EB%A0%88%EC%9D%B4%EC%96%B4%EB%93%9C-%EC%95%84%ED%82%A4%ED%85%8D%EC%B2%98Layered-Architecture
[9] https://www.reddit.com/r/learnprogramming/comments/xirz2w/what_are_some_examples_of_the_layered/
[10] https://learn.microsoft.com/en-us/dotnet/architecture/modern-web-apps-azure/common-web-application-architectures
[11] https://www.numberanalytics.com/blog/ultimate-guide-layered-architecture
[12] https://www.tracesecurity.com/blog/articles/securing-the-osi-model-the-presentation-layer
[13] https://www.geeksforgeeks.org/computer-networks/presentation-layer-in-osi-model/
[14] https://hoyeong-rithm.tistory.com/98
[15] https://medium.com/@deanrubin/the-three-layered-architecture-fe30cb0e4a6
[16] https://proandroiddev.com/clean-architecture-data-flow-dependency-rule-615ffdd79e29
[17] https://medium.com/@meshara/three-layered-architecture-with-example-b597a2161538
[18] https://airbyte.com/data-engineering-resources/data-flow-architecture
[19] https://github.com/zachgoll/layered-architecture-example-app
[20] https://engineerinsight.tistory.com/63
[21] https://www.integriti.io/post/layered-architecture-what-it-is-and-how-it-can-help-you-create-applications
[22] https://joonfluence.tistory.com/801
[23] https://www.zendata.dev/post/mapping-the-data-journey-across-a-layered-architecture
[24] https://www.imperva.com/learn/application-security/osi-model/
[25] https://developer.android.com/topic/architecture/data-layer
[26] https://xxeol.tistory.com/26
[27] https://velog.io/@mrcocoball2/MSA-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0-2.-%EB%A0%88%EC%9D%B4%EC%96%B4%EB%93%9C-%EC%95%84%ED%82%A4%ED%85%8D%EC%B2%98-%ED%97%A5%EC%82%AC%EA%B3%A0%EB%82%A0-%EC%95%84%ED%82%A4%ED%85%8D%EC%B2%98
[28] https://en.wikipedia.org/wiki/Presentation_layer
[29] https://medium.com/@nay1228/the-presentation-layer-of-the-osi-model-an-in-depth-guide-for-professionals-c87bd1c7b9c5
[30] https://www.techtarget.com/searchnetworking/definition/presentation-layer
[31] https://www.coderscampus.com/what-is-the-presentation-layer-in-programming/
[32] https://codewithandrea.com/articles/flutter-presentation-layer/
[33] https://www.geeksforgeeks.org/computer-networks/presentation-layer-services/
