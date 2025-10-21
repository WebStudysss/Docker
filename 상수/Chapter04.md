# 애플리케이션 소스 코드에서 도커 이미지까지
### **Q1.**

다음 중 *멀티스테이지 빌드(Multi-stage build)*의 가장 큰 목적은 무엇인가?

A. 여러 컨테이너를 동시에 실행할 수 있도록 한다

B. 이미지 빌드 속도를 느리게 만들어 안정성을 확보한다

C. 빌드 환경과 실행 환경을 분리하여 최종 이미지를 작게 만든다

D. Dockerfile을 여러 개로 분리해 관리하기 쉽게 한다

---

### **Q2.**

다음 Dockerfile에서 `COPY --from=build-stage /build.txt /build.txt` 명령의 의미로 **가장 올바른 설명**은?

```docker
FROM diamol/base AS build-stage
RUN echo 'Building...' > /build.txt

FROM diamol/base AS test-stage
COPY --from=build-stage /build.txt /build.txt

```

A. build-stage 이미지를 삭제한다

B. build-stage에서 생성한 파일을 test-stage로 복사한다

C. build-stage와 test-stage를 동시에 실행한다

D. build-stage를 기반으로 test-stage를 다시 빌드한다

---

### **Q3.**

아래 명령의 의미로 올바른 것은?

```bash
docker image build -t multi-stage .

```

A. 컨테이너를 실행한다

B. 현재 디렉터리의 Dockerfile로 이미지를 빌드하고 이름을 multi-stage로 설정한다

C. Dockerfile을 삭제하고 캐시를 초기화한다

D. Dockerfile을 실행 중인 컨테이너에 복사한다

---

### **Q4.**

다음 중 *멀티스테이지 빌드*를 적용했을 때의 장점이 아닌 것은?

A. 이미지 크기를 줄일 수 있다

B. 빌드 환경이 표준화된다

C. 실행 시점의 보안 리스크를 줄인다

D. 실행 성능이 낮아진다

---

### **Q5.**

아래 Dockerfile에서 첫 번째 스테이지(`builder`)는 어떤 역할을 하는가?

```docker
FROM diamol/maven AS builder

WORKDIR /usr/src/iotd
COPY pom.xml .
RUN mvn -B dependency:go-offline
COPY . .
RUN mvn package

```

A. 애플리케이션 실행 환경을 제공한다

B. 빌드 도구인 Maven을 이용해 JAR 파일을 패키징한다

C. Docker 이미지의 크기를 줄이는 역할만 한다

D. JDK 이미지를 기반으로 JVM을 실행한다

---

### **Q6.**

빌드 서버 없이도 멀티스테이지 Dockerfile로 충분히 통합 빌드가 가능한 이유는?

A. Dockerfile이 Git을 자동으로 관리하기 때문이다

B. 모든 빌드 단계가 Docker 컨테이너 내부에서 실행되기 때문이다

C. Dockerfile은 CI/CD 도구를 대체한다

D. Docker CLI가 Maven을 자동으로 설치한다

---

### **Q7.**

다음 중 빌드 서버를 사용하는 이유로 가장 적절한 것은?

A. 개발자마다 다른 환경에서 빌드가 수행되면 결과가 달라질 수 있기 때문

B. Dockerfile은 개인 PC에서만 실행되기 때문

C. Maven과 JDK가 항상 같은 버전으로 동작하기 때문

D. 빌드 서버는 테스트 실행을 차단하기 위해서만 사용된다

---

### **Q8.**

아래와 같이 구성된 Dockerfile을 빌드하면 최종 이미지에는 어떤 파일이 포함되는가?

```docker
FROM diamol/base AS build-stage
RUN echo 'Building...' > /build.txt

FROM diamol/base AS test-stage
COPY --from=build-stage /build.txt /build.txt
RUN echo 'Testing...' >> /build.txt

FROM diamol/base
COPY --from=test-stage /build.txt /build.txt
CMD cat /build.txt

```

A. "Building..." 만 포함된 build.txt

B. "Testing..." 만 포함된 build.txt

C. "Building...\nTesting..." 내용이 포함된 build.txt

D. 빈 파일만 포함된다

---

### **Q9.**

`FROM diamol/openjdk` 스테이지의 역할로 올바른 것은?

A. Maven 프로젝트의 종속성 다운로드

B. 최종 JAR 파일을 실행하는 런타임 환경 제공

C. 테스트 코드 실행 및 검증

D. 이미지 빌드 캐시 정리

---

### **Q10.**

멀티스테이지 빌드의 *“성능 향상”* 효과를 설명할 때 적절한 이유는?

A. 각 단계가 병렬로 실행되어 CPU 사용량이 줄어든다

B. 캐시 재사용 덕분에 변경되지 않은 스테이지는 재빌드하지 않는다

C. Dockerfile의 줄 수가 줄어들어 컴파일 속도가 빠르다

D. 빌드 스테이지 간 로그를 자동 분석한다

---

| **Q1** | ✅ C | 빌드 환경과 실행 환경 분리 → 이미지 최소화 |
| --- | --- | --- |
| **Q2** | ✅ B | build-stage의 결과물(파일)을 test-stage로 복사 |
| **Q3** | ✅ B | 현재 디렉토리 Dockerfile로 `multi-stage` 이미지 빌드 |
| **Q4** | ✅ D | 멀티스테이지 빌드는 성능 저하가 아니라 향상 효과 |
| **Q5** | ✅ B | Maven 빌드 스테이지에서 JAR 패키징 수행 |
| **Q6** | ✅ B | 모든 빌드 과정이 Docker 컨테이너 내부에서 수행 |
| **Q7** | ✅ A | 환경 차이로 인한 빌드 결과 불일치 방지 |
| **Q8** | ✅ C | “Building…” + “Testing…” 둘 다 포함된 결과 파일 |
| **Q9** | ✅ B | 최종 JAR 실행을 위한 런타임 환경 제공 (OpenJDK) |
| **Q10** | ✅ B | 캐시 재사용으로 변경 없는 스테이지는 스킵되어 빠름 |
