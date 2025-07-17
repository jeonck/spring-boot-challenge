# 스프링 부트 앱을 쿠버네티스에서 쉽게 실행하기: 초보자를 위한 가이드

스프링 부트로 멋진 앱을 만들었고, 이제 이를 프로덕션 환경에서 안정적으로 실행하고 싶다고 상상해보세요. 쿠버네티스(Kubernetes, 줄여서 K8s)는 확장성, 안정성, 자동화를 제공하는 최고의 플랫폼입니다. 도커(Docker), 헬름(Helm), GitOps 같은 도구를 활용하면 복잡한 설정도 쉽게 관리할 수 있습니다. 이 가이드는 초보 개발자를 위해 간단하고 실용적으로 설명합니다. 마치 친구와 커피를 마시며 배우는 기분으로 따라와 보세요!

## 1. 도커로 앱을 클라우드 준비 완료하기

쿠버네티스가 앱을 실행하려면 먼저 앱을 이동 가능한 패키지로 만들어야 합니다. 도커는 앱과 필요한 모든 환경(의존성, 설정 등)을 컨테이너라는 상자에 깔끔하게 포장해줍니다.

### 하는 일:

Dockerfile을 만들어 앱을 포장하는 방법을 정의합니다. 이건 앱을 위한 요리 레시피 같은 거예요:

```dockerfile
FROM openjdk:17-jdk-alpine
COPY target/your-app.jar app.jar
ENTRYPOINT ["java", "-jar", "/app.jar"]
```

### 왜 중요할까?

이 파일로 앱을 어디서든 똑같이 실행할 수 있는 컨테이너 이미지를 만듭니다. 로컬 PC든, 클라우드든, 어디서든 동일하게 동작해요. 다음 단계: 도커 이미지를 빌드하고, 이를 쿠버네티스가 사용할 수 있는 이미지 저장소(예: Docker Hub)에 업로드하세요.

## 2. 쿠버네티스로 앱 배포하기

이제 도커로 포장한 앱을 쿠버네티스에서 실행할 차례입니다. 쿠버네티스는 여러 서버에서 앱을 실행하고 관리해주는 오케스트레이션 도구입니다. 여기서는 앱을 3개 복제본으로 실행하는 설정을 만들어 봅시다.

### 하는 일:

Deployment YAML 파일을 작성해 쿠버네티스에 앱 실행 방법을 알려줍니다:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - name: app
          image: your-repo/my-app:latest
          ports:
            - containerPort: 8080
          readinessProbe:
            httpGet:
              path: /actuator/health
              port: 8080
            initialDelaySeconds: 10
            periodSeconds: 5
```

### 왜 중요할까?

이 설정은 앱을 3개 복제본으로 실행해 부하를 분산하고, 하나가 죽어도 다른 복제본이 서비스를 유지해줍니다. `/actuator/health` 엔드포인트는 앱이 정상인지 확인하는 건강 체크 역할을 해요.

### 꿀팁:

- 설정은 ConfigMap으로 관리하세요. 예: `SPRING_PROFILES_ACTIVE=prod`
- 비밀번호 같은 민감한 정보는 Secret에 저장하세요.
- 메모리 초과를 막으려면 컨테이너에 리소스 제한(limits)을 설정하세요.
- 앱이 종료될 때 깔끔하게 끝나도록 `server.shutdown=graceful`을 `application.properties`에 추가하세요.

## 3. 헬름으로 배포 쉽게 재사용하기

매번 YAML 파일을 수정하는 건 귀찮죠. 헬름(Helm)은 쿠버네티스 배포를 템플릿화해 반복 작업을 줄여줍니다. 자바 개발자라면 메이븐(Maven)처럼 생각하면 됩니다.

### 하는 일:

`helm create my-app-chart`로 헬름 차트를 만듭니다. `values.yaml` 파일에서 환경별 설정(예: 복제본 수, 이미지 태그)을 정의:

```yaml
replicaCount: 3
image:
  repository: your-repo/my-app
  tag: latest
```

배포는 한 줄로:

```bash
helm install my-app-release ./my-app-chart
```

### 왜 중요할까?

헬름은 개발, 테스트, 프로덕션 환경에서 같은 템플릿을 재사용해 배포를 간단하게 만듭니다. 업데이트나 롤백도 `helm upgrade`나 `helm rollback` 명령어로 쉽게 처리할 수 있어요.

## 4. 다운타임 없이 앱 업데이트하기

사용자들은 서버가 멈추면 화를 내죠. 쿠버네티스는 앱을 업데이트할 때 서비스 중단 없이 부드럽게 처리할 수 있습니다.

### 방법 3가지:

- **롤링 업데이트**: 기본 방식이에요. 새 버전의 도커 이미지를 지정하면 쿠버네티스가 하나씩 오래된 컨테이너를 새 컨테이너로 교체합니다.

```bash
kubectl set image deployment/my-app app=your-repo/my-app:new-tag
```

- **블루-그린 배포**: 기존 버전(블루)과 새 버전(그린)을 동시에 실행한 뒤, 트래픽을 한 번에 새 버전으로 전환합니다. 문제가 생기면 바로 롤백 가능!

```yaml
spec:
  selector:
    version: green
```

- **카나리 배포**: 새 버전을 소수의 사용자(예: 10~20%)에게 먼저 테스트한 뒤 점차 전체로 확산합니다. Istio나 NGINX Ingress를 사용하면 트래픽 비율을 조정할 수 있어요:

```yaml
weight:
  stable: 80
  canary: 20
```

### 왜 중요할까?

이 방법들은 사용자가 아무것도 눈치채지 못하게 업데이트를 배포할 수 있어요. 카나리 배포는 특히 프로덕션에서 새 기능을 안전하게 테스트할 때 유용합니다.

## 5. GraphQL로 API를 유연하게 만들기

스프링 부트 앱에 GraphQL을 추가하면 클라이언트(예: 모바일 앱, 웹 UI)가 원하는 데이터만 정확히 요청할 수 있습니다.

### 하는 일:

의존성 추가:

```xml
<dependency>
  <groupId>com.graphql-java-kickstart</groupId>
  <artifactId>graphql-spring-boot-starter</artifactId>
</dependency>
```

GraphQL 스키마 정의 (`schema.graphqls`):

```graphql
type Query {
  product(id: ID!): Product
}
type Product {
  id: ID!
  name: String
  price: Float
}
```

리졸버 구현:

```java
@Component
public class ProductResolver implements GraphQLQueryResolver {
    public Product product(Long id) {
        return productRepo.findById(id).orElse(null);
    }
}
```

쿼리 예시:

```graphql
{ product(id: 1) { name price } }
```

### 왜 중요할까?

GraphQL은 클라이언트가 필요한 데이터만 요청할 수 있어 네트워크 부하를 줄이고, 복잡한 UI나 모바일 앱에서 특히 유용합니다.

## 6. GitOps와 ArgoCD로 배포 자동화

GitOps는 배포를 코드처럼 관리하는 방식입니다. ArgoCD를 사용하면 Git 저장소에 푸시된 설정을 자동으로 쿠버네티스에 적용할 수 있어요.

### 하는 일:

- Git에 쿠버네티스 YAML 파일이나 헬름 차트를 저장합니다.
- ArgoCD가 Git을 감시하며 변경 사항을 클러스터에 동기화합니다.
- ArgoCD의 웹 UI에서 배포 상태, 차이점, 롤백 옵션을 확인할 수 있습니다.

### 왜 중요할까?

- Git에 모든 변경 내역이 기록되니 누가, 언제, 무엇을 바꿨는지 추적 가능.
- 문제가 생기면 `git revert`로 쉽게 롤백.
- 팀 전체가 코드처럼 배포를 관리할 수 있어 협업이 쉬워집니다.

## 7. 보안 설정과 시크릿 관리

앱 설정과 비밀번호 같은 민감한 정보는 안전하게 관리해야 합니다.

### 하는 일:

- ConfigMap으로 일반 설정 관리:

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  SPRING_PROFILES_ACTIVE: prod
```

- Secret으로 비밀번호 저장:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: db-secret
type: Opaque
data:
  username: c3ByaW5n
  password: c2VjcmV0
```

- 스프링 부트에서 환경 변수로 사용:

```properties
spring.datasource.username=${DB_USERNAME}
spring.datasource.password=${DB_PASSWORD}
```

- Vault 같은 도구로 비밀번호를 동적으로 관리하고 주기적으로 갱신하세요.

### 왜 중요할까?

민감한 데이터를 코드에 하드코딩하면 보안 사고로 이어질 수 있어요. ConfigMap과 Secret은 설정을 분리해 안전하게 관리합니다.

## 마무리: 당신은 이제 클라우드 네이티브 개발자!

이제 스프링 부트 앱을 쿠버네티스에서 실행하고, 다운타임 없이 업데이트하고, 보안까지 강화할 수 있는 방법을 배웠습니다. 이건 단순한 이론이 아니라 넷플릭스, 구글, 아마존 같은 기업들이 실제로 사용하는 워크플로우예요.

### 주요 내용 요약:

- 도커로 앱을 포장하고 쿠버네티스로 배포
- 헬름으로 배포를 재사용 가능하게
- 롤링 업데이트, 블루-그린, 카나리 배포로 다운타임 제로
- GraphQL로 유연한 API 제공
- GitOps와 ArgoCD로 배포 자동화
- ConfigMap과 Secret으로 안전한 설정 관리

이제 당신의 앱은 확장 가능하고, 안정적이며, 클라우드 네이티브하게 실행될 준비가 됐습니다. 시작해 볼까요? 🚀
