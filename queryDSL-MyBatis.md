## QueryDSL과 MyBatis 비교표

| **특징**               | **QueryDSL**                                                                 | **MyBatis**                                                                 |
|----------------------|------------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| **쿼리 작성 방식**       | 자바 코드로 SQL 쿼리를 작성하여 타입 안전성을 제공하며, 컴파일 시 오류를 발견할 수 있음[5][13]. | XML 또는 애너테이션을 사용하여 SQL 쿼리를 작성하며, 문자열 기반으로 오류를 발견하기 어려움[1][10]. |
| **동적 쿼리 지원**      | 동적 쿼리 작성이 용이하며, 조건에 따라 쿼리를 쉽게 변경할 수 있음[5][13]. | 동적 SQL을 XML에서 작성할 수 있지만, 복잡한 쿼리 작성 시 불편할 수 있음[10][12]. |
| **유지보수성**          | 자바 코드로 작성되어 IDE의 도움을 받아 쉽게 유지보수 가능[5][13].          | SQL 쿼리를 직접 작성해야 하므로, 쿼리 수정 시 DTO 필드도 함께 변경해야 함[3][4]. |
| **성능**               | 필요한 데이터를 한 번의 쿼리로 가져올 수 있어 성능 최적화 가능[5][13].       | 매핑 과정에서 성능 저하가 발생할 수 있으며, 복잡한 쿼리에서 성능이 떨어질 수 있음[2][6]. |
| **타입 안전성**        | 정적 타입을 이용하여 SQL 쿼리를 생성하므로, 타입 안전성이 높음[5][13].       | 타입 안전성이 낮아 런타임 오류 발생 가능성이 있음[6][10]. |
| **개발 생산성**        | 복잡한 쿼리를 쉽게 작성할 수 있어 개발 생산성이 높음[5][13].                | CRUD 쿼리를 수동으로 작성해야 하므로 생산성이 낮을 수 있음[3][4]. |
| **커뮤니티 및 지원**    | 비교적 새로운 기술로, 활발한 커뮤니티와 문서가 존재함[5][13].                | 오랜 역사를 가진 기술로, 많은 자료와 커뮤니티 지원이 있음[1][10]. |

이 표는 QueryDSL과 MyBatis의 주요 특징을 비교하여 각 기술의 장단점을 명확히 보여줍니다. QueryDSL은 타입 안전성과 유지보수성에서 우수한 반면, MyBatis는 오랜 역사와 많은 자료를 바탕으로 한 안정성을 제공합니다. 각 기술의 선택은 프로젝트의 요구사항과 개발자의 선호도에 따라 달라질 수 있습니다.
[1] https://stackshare.io/stackups/mybatis-vs-querydsl
[2] https://stackoverflow.com/questions/26639057/is-it-possible-to-combine-mybatis-and-querydsl-jooq
[3] https://devuna.tistory.com/83
[4] https://akku-dev.tistory.com/116
[5] https://velog.io/@kyungmin/Spring-Query-DSL-%EA%B8%B0%EB%B3%B8%EB%AC%B8%EB%B2%95
[6] https://medium.com/@iam.rodrigofarias/navigating-the-seas-of-data-access-a-deep-dive-into-spring-data-jpa-and-mybatis-9ea0b8e777f3
[7] https://peterica.tistory.com/688
[8] https://velog.io/@cho876/JPQL-vs-query-DSL
[9] https://gwamssoju.tistory.com/102
[10] https://blog.jooq.org/sql-templating-with-jooq-or-mybatis/
[11] https://techblog.woowahan.com/2662/
[12] https://harderthanever.tistory.com/246
[13] https://dhelloper.tistory.com/75
[14] https://jeonyoungho.github.io/posts/MyBatis%EC%99%80-%EC%A0%84%ED%86%B5%EC%A0%81%EC%9D%B8-JDBC%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%A8%EC%9D%98-%EB%B9%84%EA%B5%90/
[15] https://www.enterprisedb.com/blog/using-java-orms-postgresql-mybatis
[16] https://techblog.uplus.co.kr/jpa-%EA%B2%BD%ED%97%98%EA%B8%B0-6e50497f56fd
[17] https://blog.naver.com/jowlee/220726778470?viewType=pc
[18] https://www.reddit.com/r/java/comments/iv0oxe/jooq_vs_jdbi_vs_querydsl_vs_mybatis/
[19] https://mybatis.org/mybatis-dynamic-sql/docs/kotlinOverview.html
[20] https://www.alibabacloud.com/blog/mybatis-with-a-more-fluent-experience_598062
[21] https://mybatis.org/mybatis-dynamic-sql/docs/kotlinMyBatis3.html
[22] https://medium.com/@tiendat.simplize/how-to-use-the-best-practices-for-mybatis-dynamic-sql-2c3e25f1d4d1
[23] https://codingnomads.com/mybatis-tutorial-mappers-crud
[24] https://www.marcobehler.com/guides/java-databases
[25] https://medium.com/@ShantKhayalian/comparing-hibernate-vs-jooq-vs-mybatis-for-high-performance-database-queries-e60d5ea47212
