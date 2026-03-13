# ✨ AnimNotify 기반 VFX 시스템

애니메이션 재생 중 특정 타이밍에 **Niagara VFX를 생성하기 위한 AnimNotify 시스템**입니다.  

예를 들어 다음과 같은 상황에서 사용됩니다.

- ⚔️ 칼을 휘두를 때 검기 이펙트
- 🦶 달릴 때 발 먼지 효과
- 💥 공격 시 충격파 이펙트
- 🔥 스킬 발동 시 마법 효과

AnimNotify를 활용하여 **애니메이션 타이밍과 정확히 동기화된 VFX**를 생성할 수 있습니다.

---

# 📂 파일 구조

```
Animation/
 └─ Notify/
     ├─ SpawnVFX.h
     └─ SpawnVFX.cpp
```

| 파일 | 설명 |
|---|---|
| `SpawnVFX.h` | AnimNotify 클래스 정의 |
| `SpawnVFX.cpp` | Niagara VFX 생성 로직 구현 |

---

# 🧩 시스템 구조

```
Animation Montage
      │
      │ (AnimNotify Trigger)
      ▼
USpawnVFX (AnimNotify)
      │
      ▼
NiagaraFunctionLibrary::SpawnSystemAttached
      │
      ▼
Niagara VFX 생성
      │
      ▼
Socket에 Attach
```

즉,

```
애니메이션 → Notify 발생 → Niagara VFX Spawn
```

---

# 📜 코드 설명

## SpawnVFX.h

AnimNotify 클래스를 정의합니다.

```cpp
UCLASS()
class A302_API USpawnVFX : public UAnimNotify
```

AnimNotify를 상속하여 **애니메이션 타이밍에 이벤트를 발생**시킵니다.

### 주요 변수

#### 🎇 NiagaraEffect

```cpp
UPROPERTY(EditAnywhere, BlueprintReadWrite, Category="VFX")
UNiagaraSystem* NiagaraEffect;
```

- 사용할 **Niagara VFX 에셋**
- 애니메이션에서 Notify를 추가할 때 설정 가능

예

```
NS_SwordTrail
NS_AttackImpact
NS_FootDust
```

---

#### 🔗 SocketName

```cpp
UPROPERTY(EditAnywhere, BlueprintReadWrite, Category="VFX")
FName SocketName = "weapon_socket";
```

VFX가 붙을 **소켓 이름**

예

```
weapon_socket
hand_r_socket
foot_l_socket
```

---

# ⚙️ 코드 동작 방식

## SpawnVFX.cpp

```cpp
void USpawnVFX::Notify(USkeletalMeshComponent* MeshComp, UAnimSequenceBase* Animation)
```

AnimNotify가 실행되면 호출됩니다.

---

### 1️⃣ 유효성 검사

```cpp
if (!MeshComp || !NiagaraEffect)
{
    return;
}
```

- Mesh가 없거나
- Niagara VFX가 설정되지 않은 경우

VFX 생성 중단

---

### 2️⃣ Niagara VFX 생성

```cpp
UNiagaraFunctionLibrary::SpawnSystemAttached(
    NiagaraEffect,
    MeshComp,
    SocketName,
    FVector::ZeroVector,
    FRotator::ZeroRotator,
    EAttachLocation::SnapToTarget,
    true
);
```

Niagara VFX를 **특정 소켓에 Attach하여 생성**

---

### 주요 파라미터

| 파라미터 | 설명 |
|---|---|
| `NiagaraEffect` | 생성할 Niagara 시스템 |
| `MeshComp` | 붙일 Skeletal Mesh |
| `SocketName` | Attach할 소켓 |
| `FVector::ZeroVector` | 위치 오프셋 |
| `FRotator::ZeroRotator` | 회전 오프셋 |
| `SnapToTarget` | 소켓 위치에 정확히 붙임 |
| `true` | 자동 Destroy |

---

# 🎮 실제 사용 방법

## 1️⃣ AnimNotify 추가

애니메이션 또는 몽타주에서

```
Add Notify
```

선택

```
SpawnVFX
```

추가

---

## 2️⃣ VFX 설정

Notify 설정에서

```
NiagaraEffect → 원하는 Niagara VFX 선택
SocketName → weapon_socket
```

---

## 3️⃣ 실행 흐름

```
캐릭터 공격
      ↓
Attack Animation 재생
      ↓
AnimNotify Trigger
      ↓
SpawnVFX 실행
      ↓
Niagara VFX 생성
```

---

# 🧠 사용 예시

## ⚔️ 칼 휘두르기 이펙트

```
SocketName = weapon_socket
NiagaraEffect = NS_SwordTrail
```

결과

```
검을 휘두를 때 검기 생성
```

---

## 🦶 발 먼지

```
SocketName = foot_l
NiagaraEffect = NS_FootDust
```

결과

```
달릴 때 발 먼지 생성
```

---

# 🚀 장점

### 🎯 애니메이션과 정확한 동기화

AnimNotify를 사용하여

```
공격 타이밍 = VFX 타이밍
```

정확하게 맞출 수 있습니다.

---

### 🧩 확장성

이 시스템 하나로

- 공격 이펙트
- 발 먼지
- 스킬 효과
- 충격파

모든 VFX를 관리할 수 있습니다.

---

### 🛠 디자이너 친화적

코드 수정 없이

```
AnimNotify에서 VFX만 변경
```

가능합니다.

---

# 🔮 확장 아이디어

추후 다음 기능을 추가할 수 있습니다.

### 🎛 Scale 옵션

```cpp
float Scale = 1.0f;
```

---

### 🎛 Rotation Offset

```cpp
FRotator RotationOffset;
```

---

### 🎛 Location Offset

```cpp
FVector LocationOffset;
```

---

### 🎛 Socket 자동 감지

```
Weapon
Hand
Foot
```

자동 설정 시스템

---

# 📌 정리

이 시스템은

```
AnimNotify + Niagara
```

기반으로 **애니메이션 타이밍에 맞춰 VFX를 생성하는 구조**입니다.

게임에서 매우 많이 사용하는 패턴이며

- ⚔️ 공격 이펙트
- 🦶 발 먼지
- 💥 충격파
- 🔥 스킬 효과

등 다양한 상황에 활용할 수 있습니다.