### 1. 도커 컨테이너의 기본 상태 확인 방식은 무엇을 기준으로 판단하는가?

A. 컨테이너 이미지 용량

B. 실행 중인 주요 프로세스의 상태

C. CPU 사용량

D. 네트워크 접속 가능 여부

---

### 2. 헬스체크(Healthcheck)를 사용하는 주요 목적은?

A. 컨테이너의 로그 정리

B. 애플리케이션의 동작 상태를 주기적으로 확인하기 위해

C. Dockerfile을 자동 생성하기 위해

D. 컨테이너의 포트를 자동 설정하기 위해

---

### 3. Dockerfile에서 헬스체크를 정의할 때 사용하는 구문은?

A. VERIFY

B. HEALTHCHECK

C. MONITOR

D. CHECKSTATUS

---

### 4. 다음 Dockerfile 코드에서 헬스체크 방식으로 올바른 설명은?

```docker
HEALTHCHECK CMD curl --fail http://localhost/health

```

A. 특정 프로세스가 죽었는지 확인

B. 외부 HTTP API 호출 결과로 상태를 확인

C. Dockerfile만 검사

D. 이미지 용량을 확인

---

### 5. 도커 컴포즈 healthcheck 옵션에서 `retries`는 무엇을 의미하는가?

A. 헬스체크를 몇 번 반복 실행할지

B. 비정상 상태로 판단하기 위한 연속 실패 횟수

C. 헬스체크 최소 실행 시간

D. 컨테이너 자동 재시작 횟수

---

### 6. 컨테이너 헬스체크에서 최초 지연 시간을 지정하는 옵션은?

A. timeout

B. interval

C. start_period

D. retries

---

### 7. 컨테이너가 "unhealthy" 상태가 되었을 때 발생하는 현상으로 옳은 것은?

A. 컨테이너가 자동으로 종료된다

B. 컨테이너가 자동으로 재시작된다

C. 상태만 표시되고 실행은 계속된다

D. 컨테이너 로그가 삭제된다

---

### 8. `restart: on-failure`의 의미는?

A. 컨테이너가 정상 종료되면 재시작

B. 컨테이너가 예기치 않게 종료될 경우에만 재시작

C. 항상 컨테이너를 자동 재시작

D. 컨테이너를 수동으로만 재시작 가능

---

### 9. 아래 healthcheck 설정에서 `interval: 5s`가 의미하는 것은?

```yaml
healthcheck:
  interval: 5s
  timeout: 1s
  retries: 2

```

A. 헬스체크 명령을 5번 실행

B. 헬스체크를 5초마다 수행

C. 5초 후 컨테이너를 종료

D. 컨테이너는 5번의 실패 후 unhealthy

---

### 10. 다음 healthcheck test 설정 중 올바른 방식은?

A. `test: ["CHECK", "ping", "localhost"]`

B. `test: ["CMD", "dotnet", "Utilities.HttpCheck.dll", "-t", "150"]`

C. `test: ["CPU", "80"]`

D. `test: ["MEMORY", "check"]`

---

---

## 🎯 정답 & 간단한 설명

| 번호 | 정답 | 간단 설명 |
| --- | --- | --- |
| 1 | B | 컨테이너의 기존 상태는 프로세스(PID 1) 기준으로 확인됨 |
| 2 | B | 헬스체크는 단순 실행 여부보다 실제 응답 가능 상태를 점검 |
| 3 | B | HEALTHCHECK 구문은 Dockerfile에서 헬스체크 설정 시 사용 |
| 4 | B | curl로 HTTP 응답을 기반으로 상태를 확인하는 방식 |
| 5 | B | 연속으로 지정된 횟수만큼 실패하면 unhealthy 판단 |
| 6 | C | start_period는 헬스체크 시작 전 유예 시간 |
| 7 | C | unhealthy는 상태 표시만 하고 컨테이너는 계속 실행됨 |
| 8 | B | on-failure는 비정상 종료된 경우에만 자동 재시작 |
| 9 | B | interval은 헬스체크 실행 주기 (5초마다 수행) |
| 10 | B | CMD 형식이 올바른 healthcheck test 방식 |
