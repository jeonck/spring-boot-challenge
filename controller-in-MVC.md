컨트롤러의 기능은 주로 요청 입력, 비즈니스 로직 수행, 응답 생성 등 다양한 제어 처리를 포함합니다. 이러한 제어 처리의 대상은 다음과 같습니다.

## **제어 처리의 주요 대상**

- **요청 입력 처리**: 클라이언트로부터 들어오는 HTTP 요청을 수신하고, 해당 요청의 유효성을 검사합니다. 예를 들어, 사용자가 입력한 데이터가 올바른 형식인지 확인하고, 필요한 경우 오류 메시지를 반환합니다[1][2][3].

- **비즈니스 로직 수행**: 요청에 따라 적절한 비즈니스 로직을 호출하여 데이터를 처리합니다. 이 단계에서 컨트롤러는 서비스 계층의 메서드를 호출하여 실제 비즈니스 로직을 수행하고, 그 결과를 모델에 반영합니다[4][8][9].

- **응답 생성**: 비즈니스 로직의 결과를 바탕으로 클라이언트에게 반환할 응답을 생성합니다. 이 과정에서 응답의 형식(예: JSON, HTML 등)을 결정하고, 필요한 데이터를 포함하여 클라이언트에게 전달합니다[5][6][10].

## **추가적인 제어 처리의 대상**

컨트롤러는 위의 세 가지 외에도 다음과 같은 추가적인 제어 처리의 대상을 가질 수 있습니다:

- **예외 처리**: 요청 처리 중 발생할 수 있는 예외를 관리하고, 적절한 오류 메시지를 클라이언트에게 반환하는 기능을 포함할 수 있습니다. 이는 사용자 경험을 향상시키는 데 중요한 역할을 합니다[11][12].

- **데이터 검증**: 입력된 데이터의 유효성을 검증하는 과정도 포함될 수 있습니다. 이는 비즈니스 로직이 실행되기 전에 데이터의 정확성을 보장하는 데 필요합니다[7][18].

- **로그 기록**: 요청과 응답의 흐름을 기록하여 디버깅이나 모니터링에 활용할 수 있습니다. 이는 애플리케이션의 안정성과 유지보수성을 높이는 데 기여합니다[13][14].

## **결론**

따라서, 컨트롤러의 기능은 요청 입력, 비즈니스 로직, 응답 외에도 예외 처리, 데이터 검증, 로그 기록 등 다양한 제어 처리의 대상을 포함할 수 있습니다. 이러한 기능들은 웹 애플리케이션의 전반적인 동작을 관리하고, 사용자에게 원활한 경험을 제공하는 데 필수적입니다.
[1] https://saurabhnativeblog.medium.com/understanding-controllers-in-spring-boot-with-examples-312cb1879ec1
[2] https://klyhyeon.tistory.com/56
[3] https://lngnat.tistory.com/entry/%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B83-Controller-%EC%BB%A8%ED%8A%B8%EB%A1%A4%EB%9F%AC%EC%9D%98-%EC%97%AD%ED%95%A0-%EC%82%AC%EC%9A%A9-%EB%B0%A9%EB%B2%95-%EC%9A%94%EC%B2%AD%EC%97%90-%EB%8C%80%ED%95%9C-%EC%9D%91%EB%8B%B5%EC%9D%84-%ED%95%9C%EB%8B%A4
[4] https://do5do.tistory.com/18
[5] https://symflower.com/en/company/blog/2024/controller-restcontroller-spring-boot/
[6] https://velog.io/@alsgudtkwjs/Spring-Boot-Controller%EC%99%80-4%EA%B0%80%EC%A7%80%EC%9D%98-Http-%EC%9A%94%EC%B2%AD%EB%B0%A9%EB%B2%95
[7] https://it-techtree.tistory.com/entry/validating-form-input-in-springBoot
[8] https://velog.io/@dbsrud9126/Spring-MVC
[9] https://velog.io/@drms0522/%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-%EC%BB%A8%ED%8A%B8%EB%A1%A4%EB%9F%AC%EB%9E%80
[10] https://headf1rst.github.io/spring/response-entity/
[11] https://fordevelop.tistory.com/114
[12] https://ohju.tistory.com/428
[13] https://chinkl.tistory.com/entry/%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-%EC%BB%A8%ED%8A%B8%EB%A1%A4%EB%9F%AC
[14] https://medium.com/@roshanfarakate/understanding-controller-and-restcontroller-in-spring-boot-9e46687e6a23
[15] https://sol-devlog.tistory.com/6
[16] https://w97ww.tistory.com/99
[17] https://www.reddit.com/r/learnjava/comments/qzowlf/spring_boot_what_do_you_put_in_a_controller_and/
[18] https://velog.io/@win-luck/Springboot-%EC%8A%A4%ED%94%84%EB%A7%81-%EC%9A%94%EC%B2%AD-%EB%8D%B0%EC%9D%B4%ED%84%B0RequestDto%EC%97%90-%EB%8C%80%ED%95%B4-Valid%EB%A1%9C-%EC%9C%A0%ED%9A%A8%EC%84%B1-%EA%B2%80%EC%82%AC%ED%95%98%EA%B3%A0-%EC%98%88%EC%99%B8%EC%B2%98%EB%A6%AC%ED%95%98%EA%B8%B0
[19] https://sundaland.tistory.com/692
[20] https://hardlearner.tistory.com/315
[21] https://mangkyu.tistory.com/204
[22] https://dev.to/minjoong/spring-boot-gibon-ereo-eungdab-3980
[23] https://velog.io/@tkdwns414/Spring-Boot-%EA%B3%B5%ED%86%B5-%EC%9D%91%EB%8B%B5%EC%9A%A9-ApiResponse-%EB%A7%8C%EB%93%A4%EA%B8%B0
[24] https://blog.naver.com/ghdalswl77/222454059927
[25] https://stackoverflow.com/questions/32441919/how-return-error-message-in-spring-mvc-controller
[26] https://sudo-minz.tistory.com/25
[27] https://whalesbob.tistory.com/18
[28] https://inspector.dev/spring-boot-error-handling-a-step-by-step-guide/
[29] https://velog.io/@win-luck/Springboot-%EC%8A%A4%ED%94%84%EB%A7%81-API-%EA%B5%AC%ED%98%84-%EC%BB%A4%EC%8A%A4%ED%85%80-%EC%9D%91%EB%8B%B5%EA%B0%9D%EC%B2%B4-REST-API-HttpsCode-GlobalExceptionHandler
[30] https://medium.com/@vino7tech/generic-apiresponse-and-global-exception-handling-in-spring-boot-221ce807bca6
[31] https://www.linkedin.com/pulse/spring-boot-http-request-handling-abdullah-khames-qrn7f
[32] https://www.geeksforgeeks.org/springboot/exception-handling-in-spring-boot/
[33] https://gotoendiamwin.tistory.com/11
[34] https://www.toptal.com/java/spring-boot-rest-api-error-handling
[35] https://medium.com/@bolot.89/mastering-spring-boot-filters-and-interceptors-a-guide-to-request-processing-control-7ad28fdfe374
[36] https://abuuu.tistory.com/6
[37] https://devel-repository.tistory.com/57
[38] https://hstory0208.tistory.com/entry/Spring-HTTP-%EC%9D%91%EB%8B%B5-%EB%B0%A9%EB%B2%95%EA%B3%BC-%EA%B4%80%EB%A0%A8-%EC%96%B4%EB%85%B8%ED%85%8C%EC%9D%B4%EC%85%98Annotation
[39] https://stackoverflow.com/questions/66762006/spring-boot-exception-handling-best-practice
[40] https://young-s-note.tistory.com/147
[41] https://luanaeun.tistory.com/200
[42] https://arinlee.tistory.com/60
[43] https://youwjune.tistory.com/41
[44] https://blog.naver.com/PostView.nhn?blogId=good_ray&logNo=222267722516
[45] https://velog.io/@ppinkypeach/SpringBoot-Exception-%EC%B2%98%EB%A6%AC
[46] https://nocount.tistory.com/170
[47] https://da-y-0522.tistory.com/74
[48] https://naa0.tistory.com/195
[49] https://velog.io/@springer/%EB%B9%84%EC%A6%88%EB%8B%88%EC%8A%A4-%EB%A1%9C%EC%A7%81-%EC%9E%91%EC%84%B1
[50] https://com-squadleader.tistory.com/213
[51] https://tytydev.tistory.com/59
[52] https://www.geeksforgeeks.org/advance-java/spring-boot-controller-annotation-with-example/
[53] https://www.baeldung.com/spring-controllers
[54] https://spring.io/guides/tutorials/rest
[55] https://stackoverflow.com/questions/29958231/can-a-spring-boot-restcontroller-be-enabled-disabled-using-properties
[56] https://www.baeldung.com/spring-mvc-functional-controllers
[57] https://docs.spring.io/spring-framework/reference/web/webmvc/mvc-controller.html
[58] https://medium.com/@aleksandr.shashnin/understanding-http-request-processing-in-spring-boot-2227ca339a9f
[59] https://stackoverflow.com/questions/52253775/how-spring-boot-internally-handles-the-http-request-here
[60] https://www.reddit.com/r/learnjava/comments/tqaak5/im_confused_about_how_does_a_spring_boot_web/
[61] https://spring.io/guides/gs/handling-form-submission
[62] https://www.baeldung.com/spring-http-logging
[63] https://www.thecodingforums.com/threads/spring-boot-request-mapping-how-to-handle-multiple-request-paths-in-a-controller.975357/
[64] https://support.ptc.com/help/windchill/r13.0.1.0/de/Windchill_Help_Center/customization/WCCG_UICust_MVC_Overview_RequestHandlingBySpring.html
[65] https://www.baeldung.com/exception-handling-for-rest-with-spring
[66] https://www.reddit.com/r/SpringBoot/comments/172urpj/what_is_the_standardized_way_to_handle_response/
[67] https://medium.com/@sharmapraveen91/handle-exceptions-in-spring-boot-a-guide-to-clean-code-principles-e8a9d56cafe8
[68] https://spring.io/blog/2013/11/01/exception-handling-in-spring-mvc
[69] https://stackoverflow.com/questions/76881687/spring-boot-rest-handling-business-logic-in-the-service-or-controller-layer
[70] https://medium.com/@bectorhimanshu/write-a-business-logic-in-spring-boot-where-we-want-to-1219d7843fbf
[71] https://www.codefro.com/2023/10/03/implementing-business-logic/
[72] https://medium.com/@himanshu675/why-putting-business-logic-in-spring-boot-controllers-will-haunt-you-later-and-how-clean-d48a894cea33
[73] https://www.reddit.com/r/SpringBoot/comments/1l5ba0k/whats_the_point_creating_services_in_spring_boot/
[74] https://dev.to/the_autistic_programmer/managing-persistence-and-business-logic-in-spring-a-clean-and-scalable-approach-2bhn
[75] https://www.geeksforgeeks.org/springboot/spring-boot-architecture/
[76] https://www.reddit.com/r/PinoyProgrammer/comments/15yw6yd/is_it_bad_practice_to_throw_customexceptions_in/
[77] https://www.linkedin.com/pulse/how-design-implement-business-logic-using-spring-boot-mohan-vclqc
