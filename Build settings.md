스프링 부트(Spring Boot)에서 Gradle을 사용한 빌드의 구성 요소는 다음과 같습니다.

## **1. build.gradle 파일**

- **플러그인 설정**: `plugins {}` 블록에서 스프링 부트와 관련된 플러그인을 설정합니다. 예를 들어, 스프링 부트 플러그인을 추가하여 JAR 또는 WAR 파일을 패키징할 수 있습니다.

  ```groovy
  plugins {
      id 'org.springframework.boot' version '3.2.5'
      id 'io.spring.dependency-management' version '1.0.11.RELEASE'
      id 'java'
  }
  ```

- **그룹 및 버전**: `group`과 `version`을 설정하여 프로젝트의 메타데이터를 정의합니다.

  ```groovy
  group = 'com.example'
  version = '0.0.1-SNAPSHOT'
  ```

- **소스 호환성**: `sourceCompatibility`를 사용하여 사용할 Java 버전을 지정합니다.

  ```groovy
  sourceCompatibility = '11'
  ```

- **저장소 설정**: `repositories {}` 블록에서 의존성을 다운로드할 저장소를 정의합니다. 일반적으로 Maven Central을 사용합니다.

  ```groovy
  repositories {
      mavenCentral()
  }
  ```

- **의존성 설정**: `dependencies {}` 블록에서 프로젝트에 필요한 라이브러리를 정의합니다. 예를 들어, 웹 애플리케이션을 위한 스프링 부트 스타터와 테스트 라이브러리를 추가할 수 있습니다.

  ```groovy
  dependencies {
      implementation 'org.springframework.boot:spring-boot-starter-web'
      testImplementation 'org.springframework.boot:spring-boot-starter-test'
  }
  ```

## **2. settings.gradle 파일**

- **프로젝트 설정**: 멀티 프로젝트 환경에서 서브 프로젝트를 정의하고, 프로젝트의 이름을 설정합니다. 단일 프로젝트의 경우 생략할 수 있습니다.

  ```groovy
  rootProject.name = 'my-spring-boot-project'
  include 'subproject1', 'subproject2'
  ```

## **3. Gradle Wrapper**

- **Gradle Wrapper**: `gradlew`와 `gradlew.bat` 파일을 통해 Gradle을 설치하지 않고도 프로젝트를 빌드할 수 있게 해줍니다. 이는 모든 개발자가 동일한 Gradle 버전을 사용하도록 보장합니다.

## **4. 빌드 명령어**

- **빌드 실행**: 프로젝트 루트 디렉토리에서 다음 명령어를 사용하여 빌드를 실행합니다.

  ```bash
  ./gradlew build
  ```

  이 명령어는 소스 코드를 컴파일하고, 테스트를 실행하며, 최종적으로 JAR 파일을 생성합니다.

## **결론**

스프링 부트에서 Gradle을 사용한 빌드는 `build.gradle` 파일을 중심으로 구성되며, 플러그인, 의존성, 저장소 설정 등이 포함됩니다. `settings.gradle` 파일은 멀티 프로젝트 설정에 사용되며, Gradle Wrapper는 일관된 빌드를 보장합니다. 이러한 구성 요소들은 스프링 부트 애플리케이션을 효율적으로 개발하고 배포하는 데 필수적입니다.
[1] https://code-overflow.tistory.com/entry/%EC%8A%A4%ED%94%84%EB%A7%81-%EB%B6%80%ED%8A%B8Spring-Boot-%EB%B9%8C%EB%93%9CBuild%ED%95%98%EA%B8%B0
[2] https://sr-itdiary.tistory.com/12
[3] https://docs.spring.io/spring-boot/docs/3.2.5/gradle-plugin/reference/htmlsingle/
[4] https://kimdeveloper.tistory.com/42
[5] https://www.digitalocean.com/community/tutorials/key-components-and-internals-of-spring-boot-framework
[6] https://shoney.tistory.com/entry/Spring-gradle-%EB%B9%8C%EB%93%9C-jar-%EC%8B%A4%ED%96%89%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95
[7] https://docs.spring.io/spring-boot/docs/current/gradle-plugin/reference/htmlsingle/
[8] https://velog.io/@brandonnam/Spring-Boot-Gradle-components
[9] https://velog.io/@appti/Spring-boot%EC%97%90%EC%84%9C%EC%9D%98-Gradle-%EC%84%A4%EC%A0%95
[10] https://limdevbasic.tistory.com/12
[11] https://kkambi.tistory.com/92
[12] https://stackoverflow.com/questions/47283048/how-to-capture-build-info-using-gradle-and-spring-boot
[13] https://discuss.gradle.org/t/help-understanding-publishing-artifact-plain-vs-bootable-and-testimplementation/47296
[14] https://www.baeldung.com/spring-boot-gradle-plugin
[15] https://jserim420.github.io/spring-boot/gradle/
[16] https://mosei.tistory.com/entry/Spring-Boot-Gradle-%EB%A1%9C-%EB%B9%8C%EB%93%9C-%ED%95%98%EB%8A%94-%EB%B2%95
[17] https://medium.com/@prabhathsumindapathirana/how-to-create-a-java-spring-boot-library-with-gradle-and-publish-it-to-jfrog-artifactory-e13e4b2e5867
[18] https://spring.io/guides/gs/spring-boot
[19] https://ship-jh.tistory.com/54
[20] https://discuss.gradle.org/t/how-to-publish-spring-boot-war-file-using-gradle-6-2/37522
