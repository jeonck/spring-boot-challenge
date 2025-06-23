스프링부트에서 하이버네이트를 사용할 때 "동면"이라는 개념은 데이터베이스에 대한 생각을 잠시 멈추고, 코드 작성에 집중할 수 있는 상태를 의미한다고 볼 수 있습니다. 하이버네이트는 ORM(Object-Relational Mapping) 기술로, 자바 객체와 데이터베이스 간의 매핑을 자동으로 처리하여 개발자가 SQL 쿼리를 직접 작성하지 않고도 데이터베이스와 상호작용할 수 있게 해줍니다[1][4][11].

## **동면의 의미와 코드 집중**

- **에너지 절약**: 동면이 동물이 에너지를 절약하는 상태라면, 하이버네이트를 사용하는 개발자는 데이터베이스의 복잡한 세부 사항을 잊고 비즈니스 로직에만 집중할 수 있습니다. 이는 개발 과정에서 불필요한 에너지를 소모하지 않도록 도와줍니다[5][6][12].

- **자동화된 관리**: 하이버네이트는 엔티티 매니저를 통해 데이터베이스의 CRUD 작업을 자동으로 처리합니다. 개발자는 엔티티 클래스를 정의하기만 하면 하이버네이트가 이를 기반으로 데이터베이스 테이블을 생성하고 관리합니다. 이로 인해 개발자는 데이터베이스의 세부 사항에 대한 걱정 없이 코드 작성에만 집중할 수 있습니다[1][3][10].

- **추상화된 데이터 접근**: 하이버네이트는 데이터베이스 시스템에 대한 종속성을 줄여줍니다. 즉, 데이터베이스를 변경하더라도 코드의 수정이 최소화되므로, 개발자는 데이터베이스의 종류에 관계없이 동일한 코드를 사용할 수 있습니다[2][4][11].

결론적으로, 스프링부트에서 하이버네이트를 사용하는 것은 개발자가 데이터베이스에 대한 생각을 잠시 "동면"시키고, 코드 작성에 집중할 수 있는 환경을 제공하는 것입니다. 이는 개발의 생산성을 높이고, 유지보수를 용이하게 하며, 비즈니스 로직에 더 많은 시간을 투자할 수 있도록 돕습니다.
[1] https://web-inf.tistory.com/entry/%EC%8A%A4%ED%94%84%EB%A7%81-%EB%B6%80%ED%8A%B8%EC%99%80-%ED%95%98%EC%9D%B4%EB%B2%84%EB%84%A4%EC%9D%B4%ED%8A%B8-JPA-%EA%B8%B0%EB%B3%B8-%EC%82%AC%EC%9A%A9%EB%B2%95
[2] https://maze910.tistory.com/200
[3] https://medium.com/@SlackBeck/%EC%8A%A4%ED%94%84%EB%A7%81-%EB%B6%80%ED%8A%B8-auto-configuration%EA%B3%BC-jpa-%ED%95%98%EC%9D%B4%EB%B2%84%EB%84%A4%EC%9D%B4%ED%8A%B8-sql%EB%AC%B8-%EB%A1%9C%EA%B9%85-424de95ed171
[4] https://www.quora.com/What-is-Hibernate-in-Spring-Boot
[5] https://developer.okta.com/blog/2019/02/01/spring-hibernate-guide
[6] https://colabear754.tistory.com/136
[7] https://dzone.com/articles/what-is-the-difference-between-hibernate-and-sprin-1
[8] https://chaeyami.tistory.com/256
[9] https://stackoverflow.com/questions/42135114/how-does-spring-jpa-hibernate-ddl-auto-property-exactly-work-in-spring
[10] https://blog.naver.com/ddalki333/222327606287?viewType=pc
[11] https://yeoon.tistory.com/58
[12] https://medium.com/@busrabzgz/what-is-the-relationship-between-hibernate-and-spring-ee060f2eeb27
[13] https://www.theserverside.com/video/Spring-Boot-Hibernate-JPA-and-MySQL
[14] https://dev.to/poovamraj/make-spring-boot-lean-and-mean-throwing-away-hibernate-and-java-from-spring-boot-e77
[15] https://www.reddit.com/r/java/comments/jb5m0a/when_not_to_use_hibernate/
[16] https://superuser.com/questions/561252/hibernate-doesnt-use-power-or-does-it
