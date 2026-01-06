# 💻 Day_84 Vue with DRF 03

## 🧭 인증 with Vue
![alt text](images/image.png)
![alt text](images/image-1.png)
![alt text](images/image-2.png)

### 🗣️ 회원가입
![alt text](images/image-3.png)
![alt text](images/image-4.png)
![alt text](images/image-5.png)
![alt text](images/image-6.png)
![alt text](images/image-7.png)
![alt text](images/image-8.png)
![alt text](images/image-9.png)
![alt text](images/image-10.png)
![alt text](images/image-11.png)

### 📝 로그인
![alt text](images/image-12.png)
![alt text](images/image-13.png)
![alt text](images/image-14.png)
![alt text](images/image-15.png)
![alt text](images/image-16.png)
![alt text](images/image-17.png)
![alt text](images/image-18.png)
![alt text](images/image-19.png)
![alt text](images/image-20.png)

### 📡 요청과 토큰
![alt text](images/image-21.png)
![alt text](images/image-22.png)

- **토큰이 필요한 요청**
  1. 게시글 전체 목록 조회 시
  2. 게시글 작성 시

![alt text](images/image-23.png)
- 헤더에 토큰을 같이 넘긴다

![alt text](images/image-24.png)

### 🔑 인증 여부 확인

- **사용자의 인증(로그인) 여부에 따른 추가 기능 구현**
  1. 인증되지 않은 사용자
    - 메인 페이지 접근 제한
  2. 인증된 사용자
    - 회원 가입 및 로그인 페이지에 접근 제한
  - 토큰 여부에 따라 로그인 했는지 안했는지 판단

![alt text](images/image-25.png)
![alt text](images/image-26.png)
![alt text](images/image-27.png)
![alt text](images/image-28.png)
![alt text](images/image-29.png)

## 🏗️ User Customize
![alt text](images/image-30.png)

### ⚙️ User Model Field 수정
![alt text](images/image-31.png)
![alt text](images/image-32.png)

![alt text](images/image-33.png)
![alt text](images/image-34.png)

![alt text](images/image-35.png)
![alt text](images/image-36.png)
![alt text](images/image-37.png)

- 유효성 검사가 통과되면 값이 리턴되기 때문에 여기서 age정보를 추가하면 된다
```python
from dj_rest_auth.registration.serializers import RegisterSerializer
from rest_framework import serializers


class CustomRegisterSerializer(RegisterSerializer):
    age = serializers.IntegerField()

    def get_cleaned_data(self):
        data = super().get_cleaned_data()
        data['age'] = self.validated_data.get('age')
        return data
    
    def save(self, request):
        user = super().save(request)
        user.age = self.validated_data.get('age')
        user.save()
        return user
```

### ⚙️ RegisterSerializer 수정
![alt text](images/image-38.png)
![alt text](images/image-39.png)
![alt text](images/image-40.png)
![alt text](images/image-41.png)
![alt text](images/image-42.png)
![alt text](images/image-43.png)

## 📖 참고

### 🔌 로그아웃
![alt text](images/image-44.png)
![alt text](images/image-45.png)

### 📚 기타 기능 구현

- 자연스러운 흐름을 위한 기타 기능 구현
  1. 로그인 성공 후 자동으로 메인 페이지로 이동하기
  2. 회원가입 성공 후 자동으로 로그인까지 진행하기

![alt text](images/image-46.png)
![alt text](images/image-47.png)

### 🚀 Django Signals
![alt text](images/image-48.png)
- `post_save` 신호를 `Article`이 받는다
- `create` : 생성 유무를 받는 인자

https://docs.djangoproject.com/en/5.2/topics/signals/

### 📜 환경 변수

- 애플리케이션의 설정이나 동작을 제어하기 위해 사용되는 변수
- 개발, 테스트 및 프로덕션 환경에서 다르게 설정되어야 하는 설정 값이나 **민감한 정보(예: API key)를 포함**
- 환경 변수를 사용하여 애플리케이션의 설정을 관리하면, 다양한 환경에서 일관된 동작을 유지하면서 필요에 따라 변수를 쉽게 변경할 수 있다
- **보안적인 이슈를 피하고,** 애플리케이션을 다양한 환경에 대응하기 쉽게 만들어 준다

![alt text](images/image-49.png)

### 📝 Vue 참고 자료
![alt text](images/image-50.png)

### 📦 설치한 라이브러리 정리
![alt text](images/image-51.png)


# 🔥 요약 정리

- **DRF 인증과 Vue 연동**
  - `DRF 서버`의 토큰 기반 인증 시스템을 `Vue 애플리케이션`과 연동하여 회원가입, 로그인, 로그아웃 기능을 구현
  - **회원가입**
    - `Vue`에서 회원가입 폼을 만들고 `v-model`로 사용자 입력받기
    - 폼을 제출하면 `Pinia`의 `signUp` 액션을 호출
    - `signUp` 액션은 `axios`를 사용해 `DRF`의 회원가입 `API(/account/signup/)`로 `POST` 요청 보내기
  - **로그인 및 토큰 관리**
    - `Vue`에서 로그인 폼을 만들고 `v-model`로 사용자 입력을 받기
    - 폼을 제출하면 `Pinia`의 `login` 액션을 호출
    - `login` 액션은 `axios`를 사용해 DRF의 로그인 `API(/account/signup/)`로 `POST` 요청 보내기
    - 요청이 성공하면 DRF 서버는 응답으로 인증 토큰(`Token`)을 보내주고, `Pinia state`에 `token`을 저장하여 로그인 상태를 유지
  - 인증된 요청 보내기
    - 게시글 조회처럼 인증이 필요한 API를 요청할 때는, Pinia에 저장된 토큰을 axios 요청 헤더에 포함하기
    - 헤더 형식은 headers: `{'Authorization': Token ${token}}`

- 인증 여부에 따른 접근 제어
  - 로그인 상태 확인
    - `Pinia store`에 `token`의 존재 여부에 따라 `true` 또는 `false`를 반환하는 `computed` 속성(`isLogin`)을 만들어 로그인 상태를 쉽게 확인
  - 네비게이션 가드 활용
    - `Vue Router`의 전역 가드(`beforeEach`)를 사용하여 페이지 접근을 제어
    - 로그인이 필요한 페이지에 비로그인 사용자가 접근하면 로그인 페이지로 `redirection`
    - 로그인된 사용자가 회원가입이나 로그인 페이지에 접근하면 메인 페이지로 `redirection`

- **DRF User 모델 커스터마이징**
  - `dj-rest-auth`의 기본 회원가입 기능에 `age`와 같은 추가 필드를 포함시키기 위해 `Serializer`를 커스터마이징
  - `Django` 모델 수정
    - `accouts/models.py`의 `User 모델`에 `age 필드`를 추가하고 `makemigrations` 및 `migrate`를 실행
  - 커스텀 `Serializer` 생성
    - `dj-rest-auth`의 `RegisterSerializer`를 상속받는 `CustomRegisterSerializer`를 생성하고, `age 필드`를 추가
    - `get_cleaned_data`와 `save` 메서드도 오버라이딩하여 `age` 데이터를 처리하도록 수정
  - `Django` 설정
    - `sttengs.py`에서 `dj-rest-auth`가 이 커스텀 `Serializer`를 사용하도록 `REST_AUTH` 설정을 추가
  - `Vue` 폼 수정
    - `Vue`의 회원가입 폼에도 `age`를 입력받는 `<input>` 필드를 추가

![alt text](images/image-52.png)
![alt text](images/image-53.png)