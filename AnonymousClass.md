익명 클래스(Anonymous Class)는 자바에서 이름이 없는 클래스를 정의하고 즉시 인스턴스를 생성할 수 있는 기능입니다. 익명 클래스는 주로 일회용 객체를 생성할 때 사용되며, 다음과 같은 필요성과 예시가 있습니다.

## **익명 클래스의 필요성**

1. **간결한 코드**: 익명 클래스는 별도의 클래스 파일을 만들 필요 없이, 필요한 곳에서 즉시 클래스를 정의하고 사용할 수 있습니다. 이는 코드의 가독성을 높이고, 불필요한 클래스를 줄여줍니다.

2. **일회용 객체**: 특정 작업을 위해 단 한 번만 사용될 객체를 생성할 때 유용합니다. 예를 들어, 이벤트 리스너나 스레드와 같은 경우에 적합합니다.

3. **상속 및 인터페이스 구현**: 익명 클래스는 기존 클래스나 인터페이스를 상속받거나 구현할 수 있어, 특정 기능을 재정의하거나 추가할 수 있습니다. 이는 코드의 재사용성을 높이는 데 기여합니다.

## **익명 클래스 사용 예시**

### 1. 인터페이스 구현

```java
public interface Operate {
    int operate(int a, int b);
}

public class Calculator {
    private int a;
    private int b;

    public Calculator(int a, int b) {
        this.a = a;
        this.b = b;
    }

    public int result(Operate op) {
        return op.operate(this.a, this.b);
    }
}

public class Main {
    public static void main(String[] args) {
        Calculator calculator = new Calculator(20, 10);

        int result = calculator.result(new Operate() {
            @Override
            public int operate(int a, int b) {
                return a - b;
            }
        });

        System.out.println(result); // 10
    }
}
```

위의 예시에서 `Operate` 인터페이스를 익명 클래스로 구현하여 `Calculator` 클래스의 `result()` 메서드에 전달하고 있습니다. 이를 통해 별도의 클래스를 정의하지 않고도 인터페이스를 사용할 수 있습니다.

### 2. 이벤트 리스너

```java
Button button = new Button("Click Me");
button.addActionListener(new ActionListener() {
    @Override
    public void actionPerformed(ActionEvent e) {
        System.out.println("Button clicked!");
    }
});
```

이 예시에서는 버튼 클릭 이벤트를 처리하기 위해 익명 클래스를 사용하고 있습니다. 버튼이 클릭될 때마다 `actionPerformed` 메서드가 호출되어 메시지를 출력합니다.

## **결론**

익명 클래스는 자바에서 코드의 간결함과 재사용성을 높이는 데 중요한 역할을 합니다. 특히, 일회용 객체를 생성하거나 특정 인터페이스를 구현할 때 유용하며, 이벤트 처리와 같은 상황에서 자주 사용됩니다. 이러한 특성 덕분에 익명 클래스는 자바 프로그래밍에서 매우 유용한 도구입니다.
[1] https://shyun00.tistory.com/225
[2] https://inpa.tistory.com/entry/JAVA-%E2%98%95-%EC%9D%B5%EB%AA%85-%ED%81%B4%EB%9E%98%EC%8A%A4Anonymous-Class-%EC%82%AC%EC%9A%A9%EB%B2%95-%EB%A7%88%EC%8A%A4%ED%84%B0%ED%95%98%EA%B8%B0
[3] https://ittrue.tistory.com/568
[4] https://velog.io/@jhw970714/%EC%9D%B5%EB%AA%85-%ED%81%B4%EB%9E%98%EC%8A%A4%EC%99%80-%EB%9E%8C%EB%8B%A4Lambda
[5] https://xzio.tistory.com/443
[6] https://lktprogrammer.tistory.com/139
[7] https://jminie.tistory.com/83
[8] https://myvelop.tistory.com/217
[9] https://ride-dev.tistory.com/86
[10] https://gunjoon.tistory.com/154
[11] https://yummy0102.tistory.com/661
[12] https://eunveloper.tistory.com/entry/WAS-Spring-Boot-DB-%EC%84%B1%EB%8A%A5-%EA%B0%9C%EC%84%A0%EA%B3%BC-%EC%B5%9C%EC%A0%81%ED%99%94-3-RestClient
[13] https://www.geeksforgeeks.org/advance-java/a-guide-to-restclient-in-spring-boot/
[14] https://tadaktadak-it.tistory.com/19
[15] https://tech-se.tistory.com/73
[16] https://m.blog.naver.com/tkdldjs35/220879215387
[17] https://mangkyu.tistory.com/303
[18] https://velog.io/@sinryuji/Spring%EC%97%90%EC%84%9C-%EC%82%AC%EC%9A%A9%ED%95%A0-HTTP-Client%EB%A5%BC-%EA%B3%A8%EB%9D%BC%EB%B3%B4%EC%9E%90RestTemplate-vs-RestClient-vs-WebClient
[19] https://www.baeldung.com/spring-boot-restclient
[20] https://bin-repository.tistory.com/172
[21] https://docs.spring.io/spring-framework/reference/integration/rest-clients.html
[22] https://blog.leaphop.co.kr/blogs/70/RestClient__HttpInterface_%EA%B3%A0%EC%9C%A0%EB%AA%85%EC%82%AC%EA%B0%80_%EB%90%98%EB%8B%A4
[23] https://spring.io/blog/2023/07/13/new-in-spring-6-1-restclient
[24] https://www.baeldung.com/java-anonymous-classes
[25] https://github.com/spring-projects/spring-boot/issues/41568
[26] https://www.w3resource.com/java-exercises/nested-classes/java-nested-classes-exercise-8.php
[27] https://docs.oracle.com/javase/tutorial/java/javaOO/anonymousclasses.html
[28] https://stackoverflow.com/questions/18455870/java-how-to-create-anonymous-class-on-the-fly
[29] https://medium.com/@gauravverma.career/inner-and-anonymous-inner-class-in-java-704f06fd6b24
[30] https://medium.com/@lahirurajapakshe.stack/feign-client-vs-rest-client-a-comprehensive-guide-ad227272537a
[31] https://www.reddit.com/r/learnrust/comments/141sc91/rust_analogue_of_anonymous_inner_classes/
[32] https://wooaoe.tistory.com/47
[33] https://quarkus.io/guides/rest-client
[34] https://www.codingshuttle.com/spring-boot-handbook/rest-client
[35] https://digma.ai/restclient-vs-webclient-vs-resttemplate/
[36] https://stackoverflow.com/questions/79354398/spring-boot-starter-oauth2-client-ability-to-provide-custom-restclient-instead-o
[37] https://www.reddit.com/r/programminghorror/comments/wtg0ee/is_there_a_legitimate_reasons_to_not_do_this_in/
[38] https://stackoverflow.com/questions/3262759/how-to-test-an-anonymous-inner-class-that-calls-a-private-method/3262938
