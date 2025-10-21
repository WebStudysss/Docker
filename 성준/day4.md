### 1) 4장에서 권장하는 **멀티스테이지 빌드**의 핵심 목적은?

A. 이미지 레이어를 1개로 합쳐서 I/O를 없애기

B. 빌드 도구·의존성은 빌더(stage)에만 두고, 런타임(stage)은 산출물만 담아 **용량↓/공격면↓**

C. 빌드 시간을 늘리는 대신 재현성을 높이기

D. 동일 베이스 이미지를 반복해 캐시 사용 줄이기

**정답: B**

해설: 빌더에 컴파일러·패키지 관리자를 두고 최종 이미지는 실행 산출물만 복사해 **슬림&안전**.

---

### 2) **Java(Maven/Gradle)** 이미지 빌드에서 캐시 최적 순서로 옳은 것은?

A. `COPY . .` → `mvn package`

B. `COPY src ./src` → `mvn package` → `COPY pom.xml .`

C. `COPY pom.xml .` → **의존성 다운로드** → `COPY src ./src` → 빌드

D. `mvn package` 후에 `COPY . .`

**정답: C**

해설: **의존성 정의(pom/gradle 파일)만 먼저 복사 → 다운로드 캐시 고정 → 소스 복사 → 빌드**.

---

### 3) **Node.js** 빌드에서 4장이 강조하는 CI 친화적 설치 방식은?

A. `npm install` (항상 최신에 맞춤)

B. `npm ci` (lockfile 기반, 재현성↑, 속도↑)

C. `npm update` (보안패치 자동 반영)

D. `yarn add --dev` (개발용 의존성만 추가)

**정답: B**

해설: `npm ci`는 **package-lock.json을 엄격히 따른 재현성 빌드**에 적합.

---

### 4) **Go 애플리케이션** 멀티스테이지 빌드의 일반적인 이점은?

A. 최종 이미지에 `go` 컴파일러가 포함되어 디버깅이 쉽다

B. `CGO_ENABLED=1` 기본으로 네이티브 라이브러리 의존성이 커진다

C. **정적 바이너리**를 빌드해서 `scratch`/경량 런타임에만 담아 **크기↓ 이식성↑**

D. 항상 glibc가 필요해 `alpine`을 쓰면 안 된다

**정답: C**

해설: Go는 정적 빌드가 쉬워 **최종 이미지는 실행 파일만** 넣는 패턴이 흔하다.

---

### 5) 다음 중 **멀티스테이지** 패턴으로 옳은 것은?

A. `FROM runtime AS builder` → `FROM builder AS prod`

B. `FROM builder` 단일 단계에서 빌드와 런을 모두 처리

C. `FROM builder AS build` → `FROM runtime AS final` → `COPY --from=build …`

D. `FROM scratch AS runtime`에서 직접 컴파일

**정답: C**

해설: **빌드 단계(build)와 런타임 단계(final)를 분리**하고 산출물만 복사.

---

### 6) **빌드 컨텍스트 최소화**를 위해 4장에서 권장되는 방법은?

A. 컨텍스트는 항상 루트(`.`)여야 하므로 조절 불가

B. `.dockerignore`로 **`node_modules/`, `target/`, `.git/`** 등을 제외

C. 컨텍스트를 비우고 원격 URL로만 받기

D. 큰 파일은 `ADD` URL로 두 번 받기

**정답: B**

해설: 컨텍스트 슬리밍은 빌드 속도·캐시 적중률·보안에 모두 유리.

---

### 7) 4장 예제 흐름에서 **런타임 이미지**에 포함되면 안 되는 것은?

A. 빌드 산출물(JAR, 바이너리, 번들)

B. 앱이 필요로 하는 설정/템플릿

C. 빌드 툴(컴파일러, 패키지 매니저, 헤더 파일)

D. 앱 실행에 필요한 런타임 라이브러리

**정답: C**

해설: 빌드 툴은 **빌더 스테이지**에만. 런타임은 **실행에 꼭 필요한 것만**.

---

### 8) **Java JAR** 실행용 Dockerfile에서 진입점 설정으로 가장 적절한 것은?

A. `RUN java -jar app.jar`

B. `CMD ["java -jar app.jar"]`

C. `ENTRYPOINT ["java","-jar","app.jar"]` (+ 필요 시 `CMD`로 기본 인자)

D. `EXPOSE 8080`이면 자동 실행됨

**정답: C**

해설: `ENTRYPOINT`는 실행 파일, `CMD`는 기본 인자. `RUN`은 빌드 시 실행이라 오답.

---

### 9) **의존성 캐시**를 잘 활용하는 파일 조합은?

A. Node: `package.json`만, Java: `src/**`만, Go: `*.go`만

B. Node: `package.json`+`package-lock.json`, Java: `pom.xml`/`build.gradle`, Go: `go.mod`+`go.sum`

C. 모든 언어 공통으로 `README.md`

D. Node: `node_modules/`를 컨텍스트에 포함

**정답: B**

해설: **의존성 정의/lock 파일**을 먼저 복사해 캐시 계층을 고정하는 게 핵심.

---

### 10) 다음 중 4장 관점에서 **나쁜 빌드 패턴**은?

A. Node에서 `npm ci` 사용

B. Java에서 `COPY pom.xml` 후 의존성 받기 → `COPY src`

C. Go에서 빌더에서만 컴파일 후 `scratch`로 복사

D. **런타임 스테이지에서 다시 `apt-get install build-essential`**

**정답: D**

해설: 런타임 이미지에 빌드 툴을 다시 설치하면 **용량↑, 보안면↑, 원칙 위반**.
