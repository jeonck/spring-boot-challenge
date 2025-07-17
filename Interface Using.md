사용자 서비스(User Service)를 스프링부트에서 구현하는 방법을 설명하겠습니다. 이 과정은 인터페이스 정의, 구현체 작성, 그리고 컨트롤러에서의 사용 흐름을 포함합니다.

## **1. 인터페이스 정의**

먼저, 사용자 관련 기능을 정의하는 `UserService` 인터페이스를 생성합니다. 이 인터페이스는 사용자 정보를 관리하는 메서드를 포함합니다.

```java
public interface UserService {
    User findUserById(Long id);
    List<User> findAllUsers();
    void addUser(User user);
}
```

이 인터페이스는 사용자를 ID로 찾고, 모든 사용자를 조회하며, 새로운 사용자를 추가하는 메서드를 선언합니다.

## **2. 인터페이스 구현**

이제 `UserService` 인터페이스를 구현하는 클래스를 작성합니다. 예를 들어, 메모리에서 사용자 정보를 관리하는 `InMemoryUserServiceImpl` 클래스를 만들 수 있습니다.

```java
@Service
public class InMemoryUserServiceImpl implements UserService {
    private List<User> users = new ArrayList<>();

    @Override
    public User findUserById(Long id) {
        return users.stream().filter(user -> user.getId().equals(id)).findFirst().orElse(null);
    }

    @Override
    public List<User> findAllUsers() {
        return users;
    }

    @Override
    public void addUser(User user) {
        users.add(user);
    }
}
```

이 클래스는 `UserService` 인터페이스의 메서드를 구현하여 실제 사용자 데이터를 관리합니다.

## **3. 컨트롤러에서 사용**

이제 `UserController`라는 클래스를 만들어 클라이언트의 요청을 처리하고, 서비스 계층을 호출하여 사용자 정보를 반환합니다.

```java
@Controller
public class UserController {
    private final UserService userService;

    @Autowired
    public UserController(UserService userService) {
        this.userService = userService;
    }

    @GetMapping("/users")
    public String getAllUsers(Model model) {
        List<User> users = userService.findAllUsers();
        model.addAttribute("users", users);
        return "userList"; // userList.html 뷰를 반환
    }

    @PostMapping("/users")
    public String addUser(@ModelAttribute User user) {
        userService.addUser(user);
        return "redirect:/users"; // 추가 후 목록 페이지로 리다이렉트
    }
}
```

### **4. 전체 흐름**

1. **클라이언트 요청**: 사용자가 `/users` URL로 GET 요청을 보냅니다.
   
2. **컨트롤러 처리**: `UserController`의 `getAllUsers` 메서드가 호출되어 `UserService`를 통해 모든 사용자를 가져옵니다.

3. **모델에 데이터 추가**: 가져온 사용자 목록을 모델에 추가하여 뷰에서 사용할 수 있도록 합니다.

4. **뷰 반환**: `userList.html` 뷰를 반환하여 클라이언트에게 사용자 목록을 보여줍니다.

5. **사용자 추가**: 사용자가 사용자 정보를 추가하기 위해 POST 요청을 보내면, `addUser` 메서드가 호출되어 서비스 계층을 통해 사용자가 추가됩니다.

6. **리다이렉트**: 사용자가 추가된 후, 목록 페이지로 리다이렉트하여 업데이트된 목록을 보여줍니다.

## **결론**

이와 같이 스프링부트에서 사용자 서비스를 정의하고 구현체를 작성한 후, 컨트롤러에서 이를 활용하여 클라이언트의 요청을 처리하는 흐름을 구성할 수 있습니다. 이러한 구조는 코드의 유연성과 유지보수성을 높이며, 테스트를 용이하게 합니다.
[1] https://learn.microsoft.com/en-us/windows/application-management/per-user-services-in-windows
[2] https://www.unixsysadmin.com/systemd-user-services/
[3] https://portal.hosted-power.com/knowledgebase/article/139/systemd-user-services-examples/
[4] https://wiki.archlinux.org/title/Systemd/User
[5] https://blog.victormendonca.com/2018/05/14/creating-a-simple-systemd-user-service/
[6] https://nts.strzibny.name/systemd-user-services/
[7] https://learn.microsoft.com/ko-kr/windows/application-management/per-user-services-in-windows
[8] https://www.baeldung.com/linux/systemd-create-user-services
[9] https://docs.oracle.com/en/operating-systems/oracle-linux/9/systemd/CreatingasystemdUserBasedService.html
[10] https://recordsoflife.tistory.com/1076
[11] https://velog.io/@minjiki2/Spring-Spring-MVC%EC%9D%98-%EC%9E%91%EB%8F%99%ED%9D%90%EB%A6%84-DispatcherServlet%EA%B3%BC-FrontController
[12] https://oneheung.tistory.com/22
[13] https://man7.org/linux/man-pages/man5/user@.service.5.html
[14] https://askubuntu.com/questions/676007/how-do-i-make-my-systemd-service-run-via-specific-user-and-start-on-boot
[15] https://qh5944.tistory.com/179
[16] https://velog.io/@yee0033/%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EC%99%80-%EA%B5%AC%ED%98%84%EC%B2%B4
[17] https://inpa.tistory.com/entry/JAVA-%E2%98%95-%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4Interface%EC%9D%98-%EC%A0%95%EC%84%9D-%ED%83%84%ED%83%84%ED%95%98%EA%B2%8C-%EA%B0%9C%EB%85%90-%EC%A0%95%EB%A6%AC
[18] https://medium.com/j-m-park/%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EC%9D%98-%EA%B5%AC%ED%98%84-%EB%B0%8F-%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%9C-%EB%8B%A4%ED%98%95%EC%84%B1-d6789a15ff2f
[19] https://it-learner.tistory.com/31
[20] https://dalpaeng00.tistory.com/83
[21] https://adjh54.tistory.com/138
[22] https://nozeroslope.tistory.com/205
[23] https://blog.naver.com/mals93/220716635488
[24] https://clickup.com/ko/blog/127635/use-case
[25] https://priming.tistory.com/71
[26] https://meetyougo.tistory.com/309
[27] https://velog.io/@whdrb2643/SPRING-%EC%A0%84%EC%B2%B4%EC%A0%81%EC%9D%B8-%ED%9D%90%EB%A6%84-%EC%A0%95%EB%A6%AC
[28] https://wooj-coding-fordeveloper.tistory.com/42
[29] https://it-recording.tistory.com/31
[30] https://adjh54.tistory.com/347
[31] https://youseong.tistory.com/31
[32] https://blog.naver.com/PostView.nhn?blogId=droneaje&logNo=221989463375
[33] https://devraphy.tistory.com/502
[34] https://basicplan.tistory.com/entry/%EC%84%9C%EB%B9%84%EC%8A%A4-%EB%AA%A9%ED%91%9C-%EC%84%A4%EC%A0%95%EA%B3%BC-%ED%83%80%EA%B2%9F-%EC%82%AC%EC%9A%A9%EC%9E%90-%EB%B6%84%EC%84%9D
[35] https://www.i-boss.co.kr/ab-qletter-621124
[36] https://help.blackboard.com/ko-kr/Learn/Administrator/SaaS/Integrations/Student_Information_System/SIS_Integration_Types/Snapshot_Flat_File/Snapshot_Examples/User_Examples
[37] https://thinkingdata.kr/blog/analysis-user-behavior-strategies
[38] https://ideascale.com/ko/%EB%B8%94%EB%A1%9C%EA%B7%B8/%EA%B3%A0%EA%B0%9D-%EC%84%9C%EB%B9%84%EC%8A%A4-%ED%98%81%EC%8B%A0%EC%9D%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80%EC%9A%94/
[39] https://m.blog.naver.com/ssossing/222004016673
[40] https://datarian.io/blog/user-activity-analysis-netflix-amazon
