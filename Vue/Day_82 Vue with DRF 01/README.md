# 💻 Day_82 Vue with DRF 01

## 🧠 프로젝트 개요

1. `Vue`와 `DRF` 간 기본적인 요청과 응답
2. `Vue`와 `DRF`에서의 인증 시스템
3. User 커스터마이징

### 📝 DRF 프로젝트 안내

- 스켈레톤 프로젝트 `django-pjt` 활용
- 외부 패키지 및 라이브러리는 `requirements.txt`에 작성되어 있음
- DRF 프로젝트는 스켈레톤 코드의 *주석을 해제*하며 진행한다

![alt text](images/image-4.png)
![alt text](images/image-5.png)
![alt text](images/image-6.png)
![alt text](images/image-7.png)
![alt text](images/image-8.png)
![alt text](images/image-9.png)
![alt text](images/image-10.png)
![alt text](images/image-11.png)
![alt text](images/image-12.png)
![alt text](images/image-13.png)
![alt text](images/image-14.png)

### 📝 Vue 프로젝트 안내

- 스켈레톤 프로젝트 `vue-pjt` 활용
- `Vite`를 사용해 `Pinia` 및 `Vue Router`가 추가되어 있다
- `pinia-plugin-persistedstate`가 설치 및 등록 되어 있다
- Vue 프로젝트는 스켈레톤 코드 위에 *직접 코드를 작성*하며 진행한다

![alt text](images/image-15.png)
![alt text](images/image-16.png)
![alt text](images/image-17.png)
![alt text](images/image-18.png)
![alt text](images/image-19.png)
![alt text](images/image-20.png)
![alt text](images/image-21.png)
![alt text](images/image-22.png)
![alt text](images/image-23.png)


## 📜 메인 페이지 구현

### 📱 게시글 목록 출력

![alt text](images/image-24.png)
![alt text](images/image-25.png)
![alt text](images/image-26.png)
![alt text](images/image-27.png)
![alt text](images/image-28.png)
![alt text](images/image-29.png)


### 🤝 DRF와의 요청과 응답

![alt text](images/image-30.png)
![alt text](images/image-31.png)
![alt text](images/image-32.png)
![alt text](images/image-33.png)
![alt text](images/image-34.png)
![alt text](images/image-35.png)


## 🔒 CORS Policy

- **웹 브라우저의 동일 출처 정책과 보안**
  - 기본적으로 웹 브라우저는 같은 출처에서만 요청하는 것을 허용
  - 다른 출처로 부터의 요청은 보안상 이유로 차단
  - 이는 *SOP*에 의해 다른 출처의 리소스와 상호작용 하는 것이 기본적으로 제한 된다

- **SOP**
  - 동일 출처 정책
  - 같은 출처에서만 리소스를 자유롭게 공유할 수 있다
  - 다른 출처의 데이터를 마음대로 읽어오지 못하도록 막아, 악의적인 사이트가 개인 정보를 탈취하는 것을 방지

- **출처**
  ![출처](images/image.png)
  - **출처** : `Protocol`, `Host`, `Port` 를 포함한 것
    - `http`와 `https`는 다르다
    - `localhost`와 `127.0.0.1`은 다르다
    - `3000` 포트와 `2000` 포트는 다르다
  
  ![출처2](images/image-1.png)
  - `Django`의 경우 : `http://127.0.0.1:8000`
  - `Vue`의 경우 : `http://localhost:5193`
  - 각각의 출처가 다르기 때문에 브라우저에서 오류가 난다

- **CORS Policy의 등장**
  - 현대 웹 애플리케이션은 다양한 출처로부터 리소스를 요청하는 경우가 많기 때문에 CORS 정책이 필요하게 되었다

- **CORS**
  - 교차 출처 리소스 공유
  - 다른 출처의 자원을 공유하기 위해 서버가 발급하는 *허가증* 같은 정책
  - 안전하게 우회하고, 서로 다른 서버간의 통신을 가능하게 만든다
  - 다른 출처의 리소스를 불러오려면 그 다른 출처에서 올바른 **CORS header를 포함한 응답을 반환** 해야한다 

![CORS 적용 방법](images/image-2.png)
![CORS 정리](images/image-3.png)

### 🔑 CORS Headers 설정
![alt text](images/image-36.png)
![alt text](images/image-37.png)
![alt text](images/image-38.png)
![alt text](images/image-39.png)


## 👨‍💻 게시글 생성/조회 구현

### 📝 전체 게시글 조회
![alt text](images/image-40.png)
![alt text](images/image-41.png)

### 📜 단일 게시글 조회
![alt text](images/image-42.png)
![alt text](images/image-43.png)
![alt text](images/image-44.png)
![alt text](images/image-45.png)
![alt text](images/image-46.png)

### 💡 게시글 작성
![alt text](images/image-47.png)
![alt text](images/image-48.png)
![alt text](images/image-49.png)
![alt text](images/image-50.png)
![alt text](images/image-51.png)
![alt text](images/image-52.png)
![alt text](images/image-53.png)

# 🔥 요약 정리

- **동일 출처 정책 (SOP, Same-Origin Policy)**
  - 웹 브라우저의 기본 보안 정책
  - 한 출처(Origin)에서 로드된 문서나 스크립트가 다른 *출처*의 리소스와 상호작용 하는 것을 제한
  - `출처`는 **프로토콜**, **호스트**, **포트 번호**의 조합을 의미

- **CORS(Cross-Origin Resource Sharing)**
  - SOP 제한을 완화하기 위한 정책으로 서버가 특정 출처의 요청을 허용하도록 설정
  - 서버가 자신의 응답 헤더에 `Acess-Control-Allow-Origin` 같은 정보를 포함하여 브라우저에게 다른 출처의 요청을 허용한다고 알리는 정체

- **전체 게시글 조회**
  - `ArticleView`가 마운트될 때 `getArticles` 액션을 호출하여 모든 게시글 데이터를 받아오기
  - `ArticleList` 컴포넌트는 `store`의 `article` 배열을 `v-for`로 순회
  - 각 게시글 데이터를 `ArticleListItem` 자식 컴포넌트에 `props`로 전달하여 화면에 목록을 출력

- **단일 게시글 조회**
  - **동적 라우팅**
    - `route/index.js`에 `/articles/:id`와 같은 동적 경로를 설정
  - **페이지 이동**
    - `ArticleListItem`에서 각 게시글의 고유 `id`를 포함한 `RouteLink`를 만들어 상세 페이지 이동 링크 생성
  - **데이터 조회**
    - `DetailView` 컴포넌트가 마운트되면, `useRoute()`를 사용해 `URL`의 `id` 파라미터 값을 가져오기
    - 이 `id`를 이용해 `DRF 서버`에 특정 게시글 하나에 대한 데이터를 요청하고 받아와 화면에 렌더링

- **게시글 작성**
  - **폼 작성**
    - `CreateView` 컴폰전트에서 `v-model`을 사용해 `<input>`과 `<textarea>`의 값을 반응형 변수와 양방향 바인딩
  - **데이터 전송**
    - `form`을 제출(`@submit.prevent`)하면 c`reateArticle` 함수가 호출
    - 이 함수는 `axios`를 사용해 `title`과 `content` 데이터를 담아 `DRF 서버`에 `POST` 요청 보내기
  - **페이지 이동**
    - 게시글 생성이 성공하면, `useRouter()`의 `push` 메서드를 사용해 사용자를 게시글 목록 페이지로 이동시키기

![정리](images/image-54.png)
![정리](images/image-55.png)