## MyBatis Mapper Interface의 필요성 in Spring Boot

MyBatis는 Java 애플리케이션에서 SQL 쿼리를 실행하고 결과를 매핑하는 데 사용되는 프레임워크입니다. Spring Boot와 함께 사용할 때, MyBatis의 Mapper 인터페이스는 여러 가지 중요한 역할을 수행합니다.

**1. 자동 구현 및 간편한 데이터 접근**

MyBatis의 Mapper 인터페이스는 SQL 쿼리를 호출하기 위한 메서드를 정의하는 인터페이스입니다. 이 인터페이스는 MyBatis에 의해 자동으로 구현되므로, 개발자는 별도의 DAO 클래스를 작성할 필요가 없습니다. 이는 코드의 간결성을 높이고, 유지보수를 용이하게 합니다[2][3][10].

**2. SQL과의 매핑**

Mapper 인터페이스는 SQL 쿼리와 매핑되는 메서드를 정의합니다. 예를 들어, `@Select` 어노테이션을 사용하여 SQL 쿼리를 메서드에 직접 연결할 수 있습니다. 이 방식은 SQL 쿼리를 XML 파일에 작성하는 것보다 직관적이며, 코드의 가독성을 높입니다[6][11][21].

**3. XML 파일과의 연동**

MyBatis는 Mapper XML 파일을 통해 SQL 쿼리를 정의할 수 있습니다. 이 경우, Mapper 인터페이스의 메서드와 XML 파일의 `<select>` 태그의 `id` 속성이 일치해야 합니다. 이를 통해 SQL 쿼리의 복잡성을 관리하고, 동적 SQL을 쉽게 처리할 수 있습니다[8][19].

**4. Spring과의 통합**

Spring Boot에서는 `@Mapper` 어노테이션을 사용하여 Mapper 인터페이스를 스프링의 빈으로 등록할 수 있습니다. 이로 인해, 스프링의 의존성 주입 기능을 활용하여 Mapper를 서비스 클래스에 쉽게 주입할 수 있습니다. 또한, `@MapperScan` 어노테이션을 사용하면 특정 패키지 내의 모든 Mapper 인터페이스를 자동으로 스캔하여 등록할 수 있습니다[5][18][22].

**5. 코드의 안전성 및 유지보수성 향상**

Mapper 인터페이스를 사용하면 SQL 쿼리와 메서드 간의 매핑이 명확해져, 코드의 안전성을 높이고, IDE의 코드 보조 기능을 활용할 수 있습니다. 이는 개발자가 SQL 쿼리를 작성할 때 발생할 수 있는 오류를 줄이는 데 도움을 줍니다[7][16].

결론적으로, MyBatis의 Mapper 인터페이스는 Spring Boot 애플리케이션에서 SQL 쿼리를 효율적으로 관리하고, 코드의 가독성과 유지보수성을 높이는 데 필수적인 요소입니다. 이를 통해 개발자는 더 빠르고 안전하게 데이터베이스 작업을 수행할 수 있습니다.
[1] https://innovation123.tistory.com/82
[2] https://curiousjinan.tistory.com/entry/spring-database-access-dao-mapper-annotation
[3] https://www.cockroachlabs.com/docs/stable/build-a-spring-app-with-cockroachdb-mybatis
[4] https://velog.io/@hxxnsxxg/SpringBoot-Mybatis-Mapper.xml-%EC%9E%91%EC%84%B1-%ED%95%B4%EB%B3%B4%EA%B8%B0
[5] https://mybatis.org/spring-boot-starter/mybatis-spring-boot-autoconfigure/
[6] https://kimvampa.tistory.com/59
[7] https://twofootdog.github.io/Spring-DAO%EC%99%80-Mapper%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90/
[8] https://jinmlee210.tistory.com/93
[9] https://blog.naver.com/tony950620/221679572008
[10] https://tony950620.tistory.com/81
[11] https://hyejin.tistory.com/261
[12] https://stackoverflow.com/questions/30253696/why-must-the-interface-and-xml-mapper-file-be-in-same-package-and-have-the-same
[13] https://taegyunwoo.github.io/mybatis/MyBatis_MyBatisFunction
[14] https://github.com/mybatis/spring-boot-starter/issues/510
[15] https://codingnojam.tistory.com/27
[16] https://velog.io/@kjenotn/Spring-MyBatis-%EA%B0%9C%EB%85%90-%ED%8A%B9%EC%A7%95
[17] https://velog.io/@kimcno3/Mapper-%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4%EB%A5%BC-service-%EB%A0%88%EC%9D%B4%EC%96%B4%EC%97%90-DI%ED%95%98%EC%A7%80-%EC%95%8A%EC%9D%80-%EC%9D%B4%EC%9C%A0
[18] https://dev-gorany.tistory.com/300
[19] https://www.baeldung.com/spring-mybatis
[20] https://mybatis.org/spring/mappers.html
[21] https://velog.io/@eksql3835/Spring-%EC%9D%98%EC%A1%B4%EC%84%B1-%EC%A3%BC%EC%9E%85-%ED%85%8C%EC%8A%A4%ED%8A%B8-%ED%99%98%EA%B2%BD-%EA%B5%AC%EC%B6%95-Spring-MyBatis-Mapper-Repository-Service
[22] https://medium.com/@prabin.neupane.work/mybatis-in-spring-boot-a-comprehensive-guide-to-efficient-database-access-8beea1491ece
[23] https://www.geeksforgeeks.org/advance-java/mybatis-with-spring/
[24] https://www.reddit.com/r/learnjava/comments/ydgojl/mybatis_with_spring_boot/
[25] https://sainimanish700.medium.com/mybatis-with-spring-boot-example-d521f393a742
[26] https://jung-story.tistory.com/128
