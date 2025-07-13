REST API의 특징은 다음과 같이 중요순으로 나열할 수 있습니다.

## **1. Uniform Interface (유니폼 인터페이스)**

REST API는 URI로 지정된 리소스에 대한 조작을 통일되고 한정적인 인터페이스로 수행합니다. 이는 다양한 플랫폼에서 일관된 방식으로 API를 사용할 수 있게 하여, 개발자들이 쉽게 이해하고 사용할 수 있도록 합니다[1][2].

## **2. Stateless (무상태성)**

REST는 무상태성을 특징으로 하며, 클라이언트의 상태 정보를 서버에 저장하지 않습니다. 각 요청은 독립적이며, 서버는 요청을 처리하기 위해 필요한 모든 정보를 요청 내에 포함해야 합니다. 이로 인해 서버의 구현이 단순해지고, 확장성이 높아집니다[1][3].

## **3. Cacheable (캐시 가능)**

REST API는 HTTP 프로토콜을 기반으로 하므로, HTTP의 캐싱 기능을 활용할 수 있습니다. 이를 통해 성능을 향상시키고, 불필요한 서버 요청을 줄일 수 있습니다. HTTP의 Last-Modified 태그나 E-Tag를 사용하여 캐시를 구현할 수 있습니다[1][2].

## **4. Self-descriptiveness (자체 표현 구조)**

REST API는 메시지 자체가 충분한 정보를 포함하고 있어, 클라이언트가 API의 사용법을 쉽게 이해할 수 있도록 설계되어 있습니다. 이는 API의 가독성을 높이고, 사용자가 API를 보다 쉽게 활용할 수 있게 합니다[1][3].

## **5. Client-Server Architecture (클라이언트-서버 구조)**

REST는 클라이언트와 서버 간의 역할을 명확히 구분합니다. 클라이언트는 사용자 인터페이스와 관련된 작업을 수행하고, 서버는 데이터 저장 및 비즈니스 로직을 처리합니다. 이로 인해 각 구성 요소의 독립성이 증가하고, 개발 및 유지보수가 용이해집니다[1][2].

## **6. Layered System (계층형 구조)**

REST API는 여러 계층으로 구성될 수 있으며, 보안, 로드 밸런싱, 암호화 등의 기능을 추가하여 구조의 유연성을 높일 수 있습니다. 클라이언트는 API 서버와만 상호작용하며, 중간에 있는 다른 계층은 클라이언트에게 투명하게 작동합니다[1][3].

이러한 특징들은 REST API가 현대 웹 서비스에서 널리 사용되는 이유를 잘 설명해 줍니다. REST API는 간단하고 효율적인 통신을 가능하게 하여, 다양한 애플리케이션 간의 상호작용을 원활하게 합니다.
[1] https://kingofsiliconvalley.tistory.com/66
[2] https://nesoy.github.io/blog/REST-API
[3] https://rlawls1991.tistory.com/entry/REST-API-%EA%B3%B5%EB%B6%80%ED%95%98%EA%B8%B0
[4] https://inpa.tistory.com/entry/WEB-%F0%9F%8C%90-REST-API-%EC%A0%95%EB%A6%AC
[5] https://junvelee.tistory.com/107
[6] https://dev-coco.tistory.com/97
[7] https://blog.dreamfactory.com/rest-apis-an-overview-of-basic-principles
[8] https://trenbe.github.io/2022/01/16/rest-api.html
[9] https://coffeebytes.dev/en/basic-characteristics-of-an-api-rest-api/
[10] https://inblog.ai/muchankim/4522
[11] https://hahahoho5915.tistory.com/54
[12] https://skidrow6122.tistory.com/8
[13] https://easyhomputer.tistory.com/38
[14] https://www.redhat.com/ko/topics/api/what-is-a-rest-api
[15] https://www.ibm.com/think/topics/rest-apis
[16] https://velog.io/@nias0327/REST-API%EC%9D%98-%EC%A0%95%EC%9D%98%EC%99%80-%ED%8A%B9%EC%A7%95
[17] https://wildeveloperetrain.tistory.com/18
[18] https://www.ibm.com/kr-ko/think/topics/rest-apis
[19] https://arunangshudas.com/blog/5-key-features-of-restful-apis/
[20] https://junior-datalist.tistory.com/270
[21] https://esevan.tistory.com/15
[22] https://www.scrapingbee.com/blog/six-characteristics-of-rest-api/
[23] https://aws.amazon.com/what-is/restful-api/
[24] https://learn.microsoft.com/en-us/azure/architecture/best-practices/api-design
[25] https://www.techtarget.com/searchapparchitecture/definition/RESTful-API
[26] https://stackoverflow.blog/2020/03/02/best-practices-for-rest-api-design/
[27] https://konghq.com/blog/learning-center/what-is-restful-api
