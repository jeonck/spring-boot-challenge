스프링에서 **빈(Bean)**이 종료된다는 의미는 빈의 생명주기에서 마지막 단계인 소멸 과정을 나타냅니다. 빈은 스프링 IoC(제어의 역전) 컨테이너에 의해 생성되고 관리되는 객체로, 이 빈이 더 이상 필요하지 않거나 애플리케이션이 종료될 때, 스프링 컨테이너는 해당 빈을 소멸시킵니다.

### **빈의 종료 과정**

1. **소멸 메서드 호출**:
   - 빈이 소멸될 때, 스프링은 해당 빈에 정의된 소멸 메서드를 호출합니다. 이 메서드는 자원을 해제하거나 필요한 정리 작업을 수행하는 데 사용됩니다. 예를 들어, 데이터베이스 연결을 닫거나 파일 핸들을 정리하는 작업이 포함될 수 있습니다[2][3][5].

2. **@PreDestroy 어노테이션**:
   - 빈 클래스에 `@PreDestroy` 어노테이션을 사용하여 소멸 메서드를 지정할 수 있습니다. 이 메서드는 빈이 컨테이너에서 제거되기 직전에 자동으로 호출됩니다[6][7][8].

3. **소멸 시점**:
   - 빈의 소멸은 스프링 컨테이너가 종료될 때 발생합니다. 이 과정에서 빈은 생성의 역순으로 소멸되며, 모든 의존성이 해제되고 자원이 정리됩니다[2][4][5].

### **결론**

따라서, 스프링에서 빈이 종료된다는 것은 빈이 더 이상 필요하지 않거나 애플리케이션이 종료될 때, 해당 빈의 자원을 정리하고 소멸 메서드를 호출하여 메모리에서 제거되는 과정을 의미합니다. 이는 애플리케이션의 자원 관리를 효율적으로 수행하기 위해 필수적인 단계입니다.
[1] https://chung-develop.tistory.com/55
[2] https://www.geeksforgeeks.org/bean-life-cycle-in-java-spring/
[3] https://medium.com/@rajesh9616/spring-bean-lifecycle-full-guide-8ffcb9cff0e7
[4] https://jh-labs.tistory.com/108
[5] https://medium.com/@sendvjs/spring-bean-life-cycle-9363332c335e
[6] https://aroma-bok.tistory.com/entry/Spring-Spring-Framework-%ED%95%B5%EC%8B%AC-%EC%9B%90%EB%A6%AC-42-%EB%B9%88-%EB%93%B1%EB%A1%9D-%EC%B4%88%EA%B8%B0%ED%99%94-%EC%86%8C%EB%A9%B8-%EB%A9%94%EC%84%9C%EB%93%9C-%EC%A7%80%EC%A0%95-InitializingBean-DisposableBean-%EB%B9%88Bean-%EA%B8%B0%EB%8A%A5-PostConstruct-PreDestroy-%EC%96%B4%EB%85%B8%ED%85%8C%EC%9D%B4%EC%85%98-%EC%82%AC%EC%9A%A9%EB%B2%95
[7] https://www.geeksforgeeks.org/spring-init-and-destroy-methods-with-example/
[8] https://www.codingshuttle.com/spring-boot-handbook/spring-beans
[9] https://stackoverflow.com/questions/4460384/when-is-a-spring-beans-destroy-method-called
[10] https://docs.spring.io/spring-framework/reference/core/beans/factory-nature.html
[11] https://www.baeldung.com/spring-manually-destroy-prototype-bean
[12] https://annajin.tistory.com/72
[13] https://velog.io/@minji/%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-%EC%8A%A4%ED%94%84%EB%A7%81-%EB%B9%88Bean-%EC%97%90-%EB%8C%80%ED%95%9C-%EC%9D%B4%ED%95%B4
[14] https://www.javacodegeeks.com/manually-destroy-prototype-spring-bean.html
[15] https://belklog.tistory.com/entry/Spring-FrameworkSpring-Bean%EC%9D%98-%EC%B4%88%EA%B8%B0%ED%99%94%EC%99%80-%EC%A2%85%EB%A3%8C
[16] https://dev-coco.tistory.com/170
[17] https://devlog-wjdrbs96.tistory.com/321
[18] https://livenow14.tistory.com/66
[19] https://steady-coding.tistory.com/594
