### 📘 1. 도커 컴포즈를 사용하는 가장 큰 이유는?

A. Dockerfile 없이 이미지 빌드하기 위해

B. 여러 컨테이너의 실행 상태와 구성을 하나의 파일에서 정의하고 관리하기 위해

C. 도커 이미지 용량을 줄이기 위해

D. 컨테이너를 자동 삭제하기 위해

---

### 📘 2. 도커 컴포즈 파일에서 `services` 항목의 역할은?

A. 사용할 Dockerfile 위치 지정

B. 컨테이너의 실행 정책과 구성 요소들을 정의하는 영역

C. 네트워크 종류와 IP 정보를 자동 생성

D. 도커 버전을 최신으로 업데이트

---

### 📘 3. 아래의 도커 컴포즈 설정과 동일한 명령은?

```yaml
services:
  todo-web:
    image: diamol/ch06-todo-list
    ports:
      - "8020:80"
    networks:
      - app-net

```

A. docker run diamol/ch06-todo-list

B. docker container run -p 8020:80 --network app-net diamol/ch06-todo-list

C. docker image pull diamol/ch06-todo-list

D. docker-compose network create app-net

---

### 📘 4. 도커 컴포즈에서 `external: true`로 네트워크를 선언하는 이유는?

A. 항상 새 네트워크를 생성하기 위해

B. 이미 존재하는 네트워크를 그대로 사용하기 위해

C. 네트워크를 삭제하지 않기 위해

D. 외부 인터넷 연결을 막기 위해

---

### 📘 5. 아래 중 도커 컴포즈의 주요 명령 설명으로 잘못된 것은?

A. `docker-compose up` → 컨테이너 생성 및 실행

B. `docker-compose down` → 컨테이너와 네트워크 모두 제거

C. `docker-compose stop` → 컨테이너 실행 중지

D. `docker-compose start` → 컨테이너 새로 빌드 후 실행

---

### 📘 6. 다음 중 도커 컴포즈에서 컨테이너 실행 순서를 지정하는 옵션은?

A. depends_on

B. environment

C. ports

D. scale

---

### 📘 7. `docker-compose up -d --scale iotd=3` 명령의 설명으로 올바른 것은?

A. iotd 컨테이너를 3개 삭제한다

B. iotd 서비스를 3개 복제해서 부하 분산 가능한 다중 컨테이너로 만든다

C. iotd 컨테이너의 포트를 3개 노출한다

D. iotd 서비스를 자동으로 다운시킨다

---

### 📘 8. 도커 컨테이너 간 통신이 가능한 근본적인 이유는?

A. Docker는 모든 컨테이너에 고정 IP를 제공

B. Docker에는 서비스 이름 기반 통신이 가능한 내장 DNS가 있음

C. Docker는 모든 네트워크를 외부 공유 네트워크로 사용

D. Docker 컨테이너끼리는 기본적으로 브리지 네트워크를 공유하지 않음

---

### 📘 9. 도커 컴포즈 파일에서 `environment:` 옵션의 역할은?

A. 도커 네트워크 구성

B. 컨테이너 내부에서 사용할 환경 변수 값을 설정

C. 이미지 자동 다운로드

D. 컨테이너 크기 조정

---

### 📘 10. 아래 설명에 해당하는 옵션은?

> 컨테이너 내부 파일에 기록될 비밀 값 정의.
> 
> 
> 파일 형태로 전달되며, 환경 변수보다 높은 보안을 제공함.
> 

A. volumes

B. secrets

C. configs

D. environment

---

---

## 🎯 정답 & 간단한 설명

| 번호 | 정답 | 간단 설명 |
| --- | --- | --- |
| 1 | B | 여러 컨테이너의 실행 상태와 설정을 한 파일로 관리 가능 |
| 2 | B | services는 컨테이너 설정을 정의하는 핵심 영역 |
| 3 | B | 포트, 네트워크 지정까지 포함된 docker run 명령과 동일 |
| 4 | B | external은 기존 네트워크를 새로 만들지 않고 사용함 |
| 5 | D | start는 기존 컨테이너 재시작이지 새 빌드가 아님 |
| 6 | A | depends_on은 컨테이너 실행 순서를 지정함 |
| 7 | B | scale은 동일 서비스 컨테이너를 여러 개 실행 |
| 8 | B | Docker에는 서비스 이름 기반 통신 가능한 DNS가 내장 |
| 9 | B | environment는 컨테이너의 환경 변수 설정 |
| 10 | B | secrets는 파일 형태로 전달되는 안전한 데이터 |
