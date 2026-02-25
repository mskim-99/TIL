# 🎮 Unreal Engine C++ TIL - Jump Input & UE_LOG

## 📌 프로젝트 정보
- 프로젝트명: **IntroCpp**
- 엔진: Unreal Engine 5
- 개발 툴: Visual Studio
- 학습 내용: 점프 입력 처리 및 UE_LOG 출력

---

# 🚀 프로젝트 실행 방법 (IntroCpp.uproject 실행)

## 1️⃣ .uproject 파일 실행하기

📁 경로 예시:
```
IntroCpp/IntroCpp.uproject
```

### 실행 방법

1. `IntroCpp.uproject` 파일을 더블 클릭
2. Unreal Engine이 자동 실행됨
3. 프로젝트가 열리면 Play 버튼으로 실행 가능

---

## 💡 만약 실행이 안 될 경우

- Visual Studio C++ 빌드 환경이 설치되어 있는지 확인
- 우클릭 → "Generate Visual Studio project files"
- 다시 실행

---

# 🔄 C++ 코드 수정 후 리빌드 방법

C++ 파일을 수정했다면 반드시 **빌드(Build)** 또는 **리빌드(Rebuild)** 해야 합니다.

---

## 📌 방법 1 : Unreal Editor에서 컴파일

1. Unreal Editor 실행
2. 상단의 **Compile 버튼 클릭**

👉 빠르게 확인할 때 사용

---

## 📌 방법 2 : Visual Studio에서 빌드 (권장)

📁 수정 파일 위치:
```
Source/IntroCpp/IntroCppCharacter.cpp
```

### 빌드 방법

1. Visual Studio 열기
2. 상단 메뉴 → Build
3. **Build Solution (Ctrl + Shift + B)**

또는

- 우클릭 → Rebuild Solution (전체 재빌드)

---

## 🔥 언제 Rebuild를 해야 할까?

- 헤더(.h) 파일 수정했을 때
- 빌드 오류가 꼬였을 때
- 엔진 충돌 후 이상할 때

---

# 🗂 Visual Studio에서 수정한 파일

```
IntroCpp
 └─ Source
     └─ IntroCpp
         ├─ IntroCppCharacter.h
         └─ IntroCppCharacter.cpp   ⭐ (여기를 수정)
```

---

# 🎯 오늘 배운 내용

스페이스 바 입력에 따라 로그를 출력하는 기능 구현

| 입력 상태 | 실행 내용 |
|-----------|------------|
| 스페이스 바를 눌렀을 때 | "Hello World!" 출력 |
| 스페이스 바를 뗐을 때 | "Superhero Landing!" 출력 |

---

# ⌨️ 1️⃣ SetupPlayerInputComponent 수정

```cpp
void AIntroCppCharacter::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent)
{
    Super::SetupPlayerInputComponent(PlayerInputComponent);

    PlayerInputComponent->BindAction("Jump", IE_Pressed, this, &AIntroCppCharacter::JumpStart);
    PlayerInputComponent->BindAction("Jump", IE_Released, this, &AIntroCppCharacter::JumpEnd);
}
```

---

# 🚀 2️⃣ 점프 시작 함수

```cpp
void AIntroCppCharacter::JumpStart()
{
    UE_LOG(LogTemp, Display, TEXT("Hello World!"));
    Jump();
}
```

---

# 🦸 3️⃣ 점프 종료 함수

```cpp
void AIntroCppCharacter::JumpEnd()
{
    UE_LOG(LogTemp, Display, TEXT("Superhero Landing!"));
    StopJumping();
}
```

---

# 🧠 UE_LOG 정리

```cpp
UE_LOG(LogTemp, Display, TEXT("출력할 메시지"));
```

| 요소 | 설명 |
|------|------|
| LogTemp | 로그 카테고리 |
| Display | 로그 레벨 |
| TEXT() | 유니코드 문자열 매크로 |

---

# 🖥 로그 확인 방법

Unreal Editor → Window → Developer Tools → Output Log

또는

Visual Studio → Output 창 확인

---

# ✨ 배운 점

- 입력은 BindAction으로 연결한다.
- IE_Pressed / IE_Released로 입력 상태 구분 가능
- UE_LOG는 디버깅의 핵심 도구
- C++ 수정 후에는 반드시 빌드 필요

---

# 🔥 한 줄 정리

> C++ 코드 수정 → 빌드 → .uproject 실행 → 로그 확인  
> 이것이 언리얼 C++ 개발의 기본 루틴이다.

---

📅 TIL 작성일: 2026-02-25