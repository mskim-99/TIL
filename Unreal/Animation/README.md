# 📘 TIL - Unreal Engine 5 Manny 3인칭 캐릭터 세팅

## 📅 날짜
2026.03.03

---

## 🎯 오늘의 목표
- Manny 스켈레탈 메시 적용
- Animation Blueprint 연결
- 3인칭 카메라 구성
- 캐릭터 회전 구조 이해 및 설정
- 애니메이션 미끄러짐 확인을 위한 디버깅 환경 구축

---

# 1️⃣ Manny 스켈레탈 메시 적용

### ✔ BP_MyCharacter에서 설정

- `CharacterMesh (Mesh)` 선택
- Skeletal Mesh → `SKM_Manny_Simple` 적용
- Animation Mode → `Use Animation Blueprint`
- Anim Class → `ABP_Manny` 또는 `ABP_Unarmed` 선택

👉 결과: Manny가 정상적으로 애니메이션 재생됨

---

# 2️⃣ 3인칭 카메라 구성

## ① SpringArm 추가

- Add Component → Spring Arm
- 이름: `ThirdPersonSpringArm`

### SpringArm 세팅

- Target Arm Length: 300 ~ 350
- Socket Offset Z: 50
- Use Pawn Control Rotation: ✅ 체크

---

## ② Camera 추가

- Add Component → Camera
- SpringArm 하위에 배치

### Camera 세팅

- Use Pawn Control Rotation: ❌ 해제

---

# 3️⃣ 3인칭 회전 구조 설정 ⭐ (핵심)

## ① Self 회전 설정

BP_MyCharacter (Self) 선택 후:

- Use Controller Rotation Pitch ❌
- Use Controller Rotation Yaw ❌
- Use Controller Rotation Roll ❌

👉 캐릭터가 카메라 방향을 따라 회전하지 않도록 설정

---

## ② CharacterMovement 회전 설정

CharacterMovement 선택 후:

- Orient Rotation to Movement ✅ 체크
- Use Controller Desired Rotation ❌ 해제

👉 이동 방향으로 캐릭터가 회전하도록 설정

---

# 🔄 최종 회전 구조 정리

마우스 → 카메라 회전  
이동 입력 → 캐릭터 이동 방향으로 회전  

### 최종 옵션 요약

Self  
- Use Controller Rotation Yaw ❌  

CharacterMovement  
- Orient Rotation to Movement ✅  

SpringArm  
- Use Pawn Control Rotation ✅  

Camera  
- Use Pawn Control Rotation ❌  

---

# 4️⃣ 플레이 테스트 결과

✅ Manny 정상 작동  
✅ 달리기 / 멈춤 정상  
✅ 점프 정상  
✅ 카메라 회전 정상  
✅ 이동 방향 회전 정상  

---

# 5️⃣ 배운 점 💡

- 3인칭 구조에서는 카메라 회전과 캐릭터 회전을 분리해야 한다.
- Use Controller Rotation Yaw와 Orient Rotation to Movement의 차이를 이해했다.
- 3인칭 카메라는 애니메이션 디버깅에 매우 유리하다.
- 미끄러짐 문제는 대부분 이동 속도와 애니메이션 속도 불일치에서 발생한다.

---

# 6️⃣ 다음 학습 예정

- 3인칭 ↔ 1인칭 전환 구조
- Root Motion vs In-Place 차이
- BlendSpace 속도 정밀 조정
- Manny → 커스텀 캐릭터 리타게팅

---

# 🧠 오늘의 한 줄 정리

> 3인칭 캐릭터의 핵심은 "카메라 회전과 캐릭터 회전을 분리하는 것"이다.