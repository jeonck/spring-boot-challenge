스프링부트에서 의존성 주입(Dependency Injection, DI)은 필요한 모듈이나 객체를 선언만 하면, 개발자가 직접 클래스를 생성하는 코드 없이도 스프링 컨테이너가 자동으로 해당 객체를 생성하고 주입해주는 기능을 의미합니다.

## **의존성 주입의 작동 원리**

- **제어의 역전(IoC)**: 스프링은 객체의 생성과 생명 주기를 관리하는 제어권을 개발자에서 스프링 컨테이너로 넘깁니다. 이를 통해 개발자는 객체를 직접 생성할 필요 없이, 필요한 객체를 스프링이 자동으로 생성하고 주입하게 됩니다[1][2].

- **자동 주입**: 스프링에서는 `@Autowired` 어노테이션을 사용하여 의존성을 자동으로 주입할 수 있습니다. 이 어노테이션이 붙은 필드나 생성자는 스프링이 관리하는 빈(Bean)으로부터 필요한 의존성을 자동으로 주입받습니다[3][4].

## **예시**

예를 들어, 다음과 같은 코드에서 `SampleRepository` 객체를 `SampleController`에 주입할 수 있습니다:

```java
public class SampleController {
    @Autowired
    private SampleRepository sampleRepository; // SampleRepository가 자동으로 주입됨
}
```

이렇게 하면, `SampleController`가 생성될 때 스프링이 `SampleRepository`의 인스턴스를 자동으로 생성하고 주입해줍니다. 개발자는 `SampleRepository`를 직접 생성하는 코드를 작성할 필요가 없습니다.

## **결론**

따라서, 의존성 주입은 스프링부트의 핵심 기능 중 하나로, 개발자가 객체 생성에 대한 부담을 덜고, 코드의 가독성과 유지보수성을 높이는 데 기여합니다.
[1] https://do5do.tistory.com/17
[2] https://woogienote.tistory.com/118
[3] https://www.geeksforgeeks.org/advance-java/spring-dependency-injection-with-example/
[4] https://lincoding.tistory.com/76
[5] https://stackoverflow.com/questions/8579733/automatic-dependency-injection-with-spring
[6] https://sorryday.tistory.com/26
[7] https://nextculture.github.io/spring-boot-auto-configuration/
[8] https://ddd66.tistory.com/33
[9] https://technology-share.tistory.com/11
[10] https://www.baeldung.com/spring-dependency-injection
[11] https://medium.com/dev-spring/autowired-in-spring-boot-6e46e7c9c4a3
[12] https://docs.spring.io/spring-framework/reference/core/beans/dependencies/factory-collaborators.html
[13] https://chung-develop.tistory.com/148
[14] https://ittrue.tistory.com/227
[15] https://velog.io/@lychee/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%95%B5%EC%8B%AC-%EC%9B%90%EB%A6%AC-07.-%EC%9D%98%EC%A1%B4%EA%B4%80%EA%B3%84-%EC%9E%90%EB%8F%99-%EC%A3%BC%EC%9E%85
[16] https://stackoverflow.com/questions/76666072/how-to-do-dependency-injection-manually-in-spring-boot
[17] https://ship-jh.tistory.com/54
[18] https://medium.com/@reetesh043/spring-boot-dependency-injection-137f85f84590
[19] https://velog.io/@sookyung/Spring-%EB%A9%80%ED%8B%B0-%EB%AA%A8%EB%93%88%EB%A1%9C-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EB%A7%8C%EB%93%A4%EA%B8%B0
[20] https://wngml56.tistory.com/188
[21] https://velog.io/@zueon/%EC%8A%A4%ED%94%84%EB%A7%81-%EB%B6%80%ED%8A%B8%EC%9D%98-%EC%9D%98%EC%A1%B4%EC%84%B1-%EA%B4%80%EB%A6%AC%EC%99%80-%EC%9E%90%EB%8F%99%EC%84%A4%EC%A0%95
[22] https://iagreebut.tistory.com/224
[23] https://igventurelli.io/dependency-injection-in-spring-simplifying-your-code/
[24] https://devloo.tistory.com/entry/Spring-Boot-%EC%8A%A4%ED%94%84%EB%A7%81-%EB%B6%80%ED%8A%B8-%EA%B3%B5%ED%86%B5-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC-%EA%B5%AC%EC%B6%95%ED%95%98%EA%B8%B0-%EA%B3%B5%ED%86%B5-%EB%AA%A8%EB%93%88
[25] https://catchdream.tistory.com/category/SpringFrameWork
[26] https://www.reddit.com/r/SpringBoot/comments/suf304/spring_boot_and_dependency_injection/
[27] https://velog.io/@dbsrud11/SpringBoot-3-7.-%EC%9D%98%EC%A1%B4%EA%B4%80%EA%B3%84-%EC%9E%90%EB%8F%99-%EC%A3%BC%EC%9E%85
[28] https://idkim97.github.io/2023-07-14-%EC%9D%98%EC%A1%B4%EA%B4%80%EA%B3%84%20%EC%9E%90%EB%8F%99%20%EC%A3%BC%EC%9E%85/
[29] https://ssdragon.tistory.com/135
