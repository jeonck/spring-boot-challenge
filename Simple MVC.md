스프링 부트(Spring Boot)에서 가장 간단한 MVC 예제를 구현하는 방법을 설명하겠습니다. 이 예제는 기본적인 구조를 이해하는 데 도움이 됩니다.

## **1. 프로젝트 설정**

스프링 부트 프로젝트를 생성할 때, 다음 두 가지 의존성을 추가합니다:

- `spring-boot-starter-web`: 웹 애플리케이션을 위한 기본 스타터
- `spring-boot-starter-thymeleaf`: Thymeleaf 템플릿 엔진을 사용하기 위한 스타터

## **2. 프로젝트 구조**

프로젝트 구조는 다음과 같습니다:

```
src
└── main
    ├── java
    │   └── com
    │       └── example
    │           └── demo
    │               └── HelloController.java
    └── resources
        └── templates
            └── hello-page.html
```

## **3. HelloController.java**

컨트롤러 클래스를 작성하여 요청을 처리합니다:

```java
package com.example.demo;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class HelloController {

    @GetMapping("/hello")
    public String hello(Model model) {
        String name = "Spring";
        model.addAttribute("name", name);
        return "hello-page"; // 반환할 뷰의 이름
    }
}
```

## **4. hello-page.html**

Thymeleaf를 사용하여 HTML 페이지를 작성합니다:

```html
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Hello</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
</head>
<body>
    <p th:text="'Hello ' + ${name}">Hello</p>
</body>
</html>
```

## **5. 실행 결과**

1. 사용자가 `GET /hello` 요청을 보냅니다.
2. 스프링의 Dispatcher Servlet이 요청을 받아 `HelloController`로 전달합니다.
3. `HelloController`에서 "Spring"이라는 이름을 모델에 추가하고, "hello-page"라는 뷰 이름을 반환합니다.
4. View Resolver가 "hello-page"를 찾아 모델 데이터를 포함하여 최종 HTML을 생성합니다.
5. 생성된 HTML이 사용자에게 반환됩니다.

이 간단한 예제를 통해 스프링 부트의 MVC 구조를 이해할 수 있습니다. MVC 패턴은 모델, 뷰, 컨트롤러 간의 명확한 분리를 통해 코드의 유지보수성과 가독성을 높여줍니다[1][3].
[1] https://chb2005.tistory.com/60
[2] https://medium.com/@TechiesSpot/mastering-mvc-in-java-spring-boot-a-comprehensive-guide-f7353a06fd61
[3] https://velog.io/@sunset_1839/Spring-%EA%B0%84%EB%8B%A8%ED%95%9C-MVC-%ED%99%9C%EC%9A%A9%EA%B3%BC-%EC%9E%91%EB%8F%99%EB%B0%A9%EC%8B%9D
[4] https://www.baeldung.com/spring-mvc-tutorial
[5] https://joonfluence.tistory.com/699
[6] https://shallow-learning.tistory.com/entry/%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-4-Spring-MVC-Controller-%EB%A7%8C%EB%93%A4%EA%B8%B0
[7] http://topstonesoftware.com/publications/simple_spring_boot_mvc_example.html
[8] https://recordsoflife.tistory.com/1074
[9] https://stackoverflow.com/questions/71815901/does-a-simple-rest-project-in-spring-boot-use-the-mvc-principle
[10] https://velog.io/@dlehddud60/%EA%B2%8C%EC%8B%9C%ED%8C%90-%EB%A7%8C%EB%93%A4%EA%B8%B0-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EA%B0%80%EC%9E%A5-%EA%B0%84%EB%8B%A8%ED%95%9C-CRUD%EA%B2%8C%EC%8B%9C%ED%8C%90-%EC%98%88%EC%A0%9C
[11] https://www.digitalocean.com/community/tutorials/spring-mvc-example
[12] https://www.devkuma.com/docs/spring-boot/mvc/
[13] https://crunchify.com/simplest-spring-mvc-hello-world-example-tutorial-spring-model-view-controller-tips/
[14] https://bnzn2426.tistory.com/126
[15] https://javatechonline.com/spring-boot-mvc-crud-example/
[16] https://spring.io/guides/gs/spring-boot
[17] https://spring.io/guides/gs/serving-web-content
[18] https://devocean.sk.com/blog/techBoardDetail.do?ID=165272
[19] https://www.reddit.com/r/learnjava/comments/attzey/spring_bootmvc_real_world_example_projects/
[20] https://just-joat.tistory.com/4
