# 🎮 Unreal Engine Viewport 사용 가이드

## 📌 개요

Unreal Engine은 프로젝트 내 오브젝트를 시각적으로 표현하기 위해 **Viewport**를 사용합니다.

Viewport는 다음과 같은 환경에서 사용됩니다.

- 🏗 Level Editor Viewport
- 🎨 Material Editor
- 🎞 Animation Mode Editor
- 🌊 Niagara Systems Editor

이 모든 Viewport는 유사한 네비게이션 방식을 공유하며,  
실제 게임에서 보이는 것과 유사한 조명 및 머티리얼 환경에서 오브젝트를 확인할 수 있습니다.

게임 제작 시 가장 많은 시간을 보내는 공간은 **Level Editor**입니다.  
따라서 Viewport 네비게이션을 숙지하는 것이 매우 중요합니다.

---

# 🔤 약어 (Abbreviations)

| 컨트롤 | 약어 |
|--------|------|
| Left Mouse Button | LMB |
| Middle Mouse Button | MMB |
| Right Mouse Button | RMB |

---

# 🖥 뷰 모드 종류

## 1️⃣ Perspective View
- 3D 공간에서 레벨 편집
- 일반적인 게임 시점

## 2️⃣ Orthographic View
- 2D 기반 편집 (Top / Side / Front View)

단축키 변경 경로:  
`Edit → Editor Preferences → General → Keyboard Shortcuts`

---

# 🎯 오브젝트 선택

선택된 오브젝트는 **Details Panel**에서 속성 수정이 가능하며,  
Viewport 내에서 이동, 회전, 스케일 조정이 가능합니다.

## 🔹 Perspective View

| 조작 | 동작 |
|------|------|
| LMB 클릭 | 오브젝트 선택 (기존 선택 해제) |
| Ctrl 또는 Shift + LMB | 선택 추가 |

## 🔹 Orthographic View

| 조작 | 동작 |
|------|------|
| LMB 클릭 | 오브젝트 선택 |
| LMB 드래그 | 다중 선택 박스 생성 |
| Shift + LMB 드래그 | 선택 영역 추가 |
| Ctrl + RMB 드래그 | 선택 영역 제거 |

---

# 👀 Viewport 둘러보기

## 🖱 일반 마우스 사용

### 🎥 Perspective

| 조작 | 동작 |
|------|------|
| LMB + 드래그 | 전/후 이동 + 좌/우 회전 |
| RMB + 드래그 | 시점 회전 |
| LMB + RMB 드래그 | 상/하/좌/우 이동 |
| MMB 드래그 | 상/하/좌/우 이동 |
| 마우스 휠 | 전/후 이동 |

### 📐 Orthographic

| 조작 | 동작 |
|------|------|
| LMB 드래그 | 다중 선택 |
| RMB 드래그 | 화면 이동(Pan) |
| LMB + RMB 드래그 | 전/후 이동 |
| 마우스 휠 | 전/후 이동 |

---

# 🚀 Perspective View에서 이동

| 조작 | 동작 |
|------|------|
| RMB + 마우스 휠 | 이동 속도 증가/감소 |
| RMB + W | 전진 |
| RMB + S | 후진 |
| RMB + A | 좌측 이동 |
| RMB + D | 우측 이동 |
| RMB + E | 위로 이동 |
| RMB + Q | 아래로 이동 |
| RMB + Z | 시야각(FOV) 증가 |
| RMB + C | 시야각(FOV) 감소 |

---

# 🔄 카메라 오브젝트 중심 회전

| 조작 | 동작 |
|------|------|
| F | 선택 오브젝트로 포커스 |
| Alt + LMB 드래그 | 오브젝트 중심 회전 |
| Alt + RMB 드래그 | 줌 인/아웃 |
| Alt + MMB 드래그 | 좌/우/상/하 이동 |

> 💡 Maya / Unity 사용자에게 익숙한 조작 방식입니다.

---

# 🛠 오브젝트 이동 / 회전 / 스케일

## ⌨ 단축키

| 키 | 기능 |
|----|------|
| Spacebar | Move / Rotate / Scale 전환 |
| Q | 선택 도구 |
| W | 이동 도구 |
| E | 회전 도구 |
| R | 스케일 도구 |

## 🎛 Gizmo 조작

- X, Y, Z 축을 드래그하여 해당 방향으로 조작
- 중앙 Pivot 사용 시 균등 스케일 가능
- 두 축 사이를 선택하면 2축 동시 이동 가능

## 🔹 추가 기능

| 조작 | 기능 |
|------|------|
| V 누르고 이동 | Vertex Snap 활성화 |
| Pivot에서 MMB 드래그 | Pivot 임시 이동 |

> 📌 Orthographic View에서는 2축 이동만 가능합니다.

---

# 🎨 표시(Display) 기능

| 키 | 기능 |
|----|------|
| G | Game Mode 전환 (에디터 Gizmo 숨김) |
| Ctrl + R | 실시간 렌더링 On/Off |
| F11 | 전체 화면 모드 |

> ⚡ 실시간 렌더링을 끄면 고사양 씬에서 성능 향상이 가능합니다.

---

# ⚙ Viewport 설정 변경

경로:  
`Edit → Editor Preferences → Level Editor → Viewports`

## 🔧 Controls
- 카메라 이동 속도 조절
- 마우스 감도 조절

## 🎨 Look and Feel
- Arcball 회전 활성화
- 통합 이동/회전 위젯 설정
- 선택 강조 강도 조절

---

# ✅ 정리

Viewport는 Unreal Engine에서 가장 많이 사용하는 핵심 작업 공간입니다.

✔ 오브젝트 선택  
✔ 카메라 이동  
✔ Transform 조작  
✔ 표시 설정 변경  

위 기능을 숙지하면 레벨 제작 속도가 크게 향상됩니다. 🚀