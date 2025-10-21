# 도커 이미지 만들기
### **Q1.**

다음 명령어의 기능으로 **가장 올바른 것**은?

```bash
docker image pull diamol/ch03-web-ping

```

A. 도커 허브에 이미지를 업로드한다

B. 도커 허브에서 이미지를 다운로드받아 로컬에 저장한다

C. 로컬 이미지를 삭제한다

D. 컨테이너를 실행한다

---

### **Q2.**

다음 Dockerfile 인스트럭션 중 **환경 변수를 설정**하기 위한 것은?

```docker
FROM diamol/node
ENV TARGET="blog.sixeyed.com"
ENV METHOD="HEAD"
ENV INTERVAL="3000"

```

A. FROM

B. COPY

C. CMD

D. ENV

---

### **Q3.**

다음 중 Dockerfile의 `CMD` 인스트럭션에 대한 설명으로 올바른 것은?

A. 이미지를 빌드할 때 실행되는 명령어이다

B. 컨테이너를 실행할 때 기본으로 실행되는 명령어이다

C. 빌드 캐시를 무효화시키는 명령어이다

D. 환경 변수를 초기화하는 명령어이다

---

### **Q4.**

`docker image history web-ping` 명령의 목적은?

A. 이미지의 이전 버전을 모두 삭제한다

B. 이미지의 빌드 히스토리와 각 레이어를 확인한다

C. 이미지 실행 로그를 출력한다

D. 컨테이너의 로그를 확인한다

---

### **Q5.**

도커 이미지는 여러 레이어로 구성된다.

다음 중 **레이어 캐시를 사용하는 이유**로 올바른 것은?

A. 동일한 명령어 결과를 재활용하여 빌드 속도를 높이기 위해

B. 모든 레이어를 삭제하기 위해

C. 컨테이너 크기를 강제로 고정하기 위해

D. 네트워크 전송 속도를 제한하기 위해

---

### **Q6.**

아래 두 Dockerfile 중, 캐시 효율성이 **더 좋은** 것은?

```docker
# (1)
FROM diamol/node
ENV TARGET="blog.sixeyed.com"
WORKDIR /web-ping
COPY app.js .
CMD ["node", "/web-ping/app.js"]

# (2)
FROM diamol/node
CMD ["node", "/web-ping/app.js"]
ENV TARGET="blog.sixeyed.com"
WORKDIR /web-ping
COPY app.js .

```

A. (1) — CMD를 마지막에 두어 캐시 효율이 높다

B. (2) — CMD를 위쪽에 두어 캐시가 더 잘 유지된다

C. 두 Dockerfile은 동일한 빌드 결과를 갖는다

D. (1)은 CMD 명령을 무시하므로 캐시가 없다

---

### **Q7.**

`FROM diamol/node` 문장이 여러 Dockerfile에서 사용될 때, 다음 중 올바른 설명은?

A. 각 Dockerfile이 별도로 용량을 차지한다

B. 동일한 FROM 이미지는 공유되어 용량이 중복되지 않는다

C. FROM 이미지마다 별도 컨테이너가 자동 생성된다

D. FROM 이미지는 항상 새로 다운로드된다

---

### **Q8.**

FROM 이미지가 업데이트되면 생길 수 있는 문제를 방지하기 위해 권장되는 방법은?

A. FROM 이미지를 쓰기 가능 상태로 둔다

B. FROM 이미지를 읽기 전용으로 고정한다

C. FROM을 여러 개 병렬로 선언한다

D. FROM 단계마다 캐시를 비운다

---

## ✅ 정답표

| 번호 | 정답 | 핵심 개념 |
| --- | --- | --- |
| **Q1** | ✅ B | `pull` → 도커 허브에서 이미지 다운로드 |
| **Q2** | ✅ D | `ENV` → 컨테이너 내부 환경 변수 설정 |
| **Q3** | ✅ B | `CMD` → 컨테이너 실행 시 기본 명령 지정 |
| **Q4** | ✅ B | `image history` → 이미지 빌드 레이어 확인 |
| **Q5** | ✅ A | 캐시 재사용으로 빌드 시간 단축 |
| **Q6** | ✅ B | 자주 변경되지 않는 `CMD`를 위에 두면 캐시 효율 ↑ |
| **Q7** | ✅ B | 동일한 FROM 이미지는 레이어 공유 |
| **Q8** | ✅ B | 변경 리스크 방지를 위해 읽기 전용 이미지 사용 |
