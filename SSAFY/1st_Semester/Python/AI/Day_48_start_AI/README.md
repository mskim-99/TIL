# AI 데이터 분석도구: NumPy & Pandas

---

## 🧮 NumPy (Numerical Python)

### NumPy란?
- **수치 계산을 위한 Python 핵심 라이브러리**입니다.
- 다차원 배열(`ndarray`)을 효율적으로 다루고, 벡터 및 행렬 연산을 빠르게 수행합니다.

### 설치
```bash
pip install numpy
```

### 핵심 생성 함수
| 기능 | 설명 | 예시 |
|---|---|---|
| `np.array()` | 리스트를 배열로 변환 | `np.array([1, 2, 3])` |
| `np.zeros((n, m))` | 0으로 채운 배열 | `np.zeros((3, 3))` |
| `np.ones((n, m))` | 1로 채운 배열 | `np.ones((2, 2))` |
| `np.identity(n)` | n×n 단위행렬 | `np.identity(3)` |
| `np.eye(n, m, k=0)` | 대각선이 1인 배열(비정방/오프셋 가능) | `np.eye(3, 4, k=1)` |
| `np.arange(start, stop, step)` | 등차 수열 | `np.arange(0, 10, 2)` |
| `np.linspace(start, stop, num)` | 구간 균등 분할 | `np.linspace(0, 2*np.pi, 100)` |
| `np.random.randn(n, m)` | 표준정규분포 난수 | `np.random.randn(3, 3)` |

### 연산 & 유틸
- **행렬곱**: `np.dot(A, B)` 혹은 `A @ B`
- **전치**: `A.T`
- **요약 통계**: `np.mean(x)`, `np.sum(x)`
- **형 변환**: `x.astype(bool/int/float)`

### 실전 예시
```python
import numpy as np

# 3x3 단위행렬
x = np.identity(3)

# 표준정규분포 난수 3x3
y = np.random.randn(3, 3)

# 행렬곱
z = x @ y  # 또는 np.dot(x, y)

# 0 ~ 2π를 균등 분할한 100개 값과 그 사인
theta = np.linspace(0, 2*np.pi, 100)
sin_theta = np.sin(theta)

# dtype 변환과 스칼라 곱
x_bool = x.astype(bool)
x_int = x.astype(int)
x_float = x.astype(float) * 1.1
```

---

## 🧾 Pandas (Python Data Analysis Library)

### Pandas란?
- **데이터 분석 및 전처리**를 위한 라이브러리입니다.
- `DataFrame`(2차원 표), `Series`(1차원 열)를 중심으로 테이블 데이터를 다룹니다.

### 설치
```bash
pip install pandas
```

### DataFrame 생성하기

#### 1. List[Dict] → DataFrame
```python
import pandas as pd

alice = {"Name": "Alice", "Age": 25, "Score": 85.5}
bob = {"Name": "Bob", "Age": 30, "Score": 90.3}
charlie = {"Name": "Charlie", "Age": 35, "Score": 78.9}

df_1 = pd.DataFrame([alice, bob, charlie])
```

#### 2. List[List] + columns → DataFrame
```python
data = [
    ["Alice", 25, 85.5],
    ["Bob", 30, 90.3],
    ["Charlie", 35, 78.9]
]
columns = ["Name", "Age", "Score"]

df_2 = pd.DataFrame(data, columns=columns)
```

#### 3. NumPy 배열 + 보조 리스트 → DataFrame
> NumPy 배열은 기본적으로 float로 들어갈 수 있으므로 dtype을 원하는 형태로 맞춰주세요.
```python
import numpy as np

names = ["Alice", "Bob", "Charlie"]
nums = np.array([
    [25, 85.5],
    [30, 90.3],
    [35, 78.9]
])

df_3 = pd.DataFrame(nums, columns=["Age", "Score"])
df_3["Age"] = df_3["Age"].astype(int)  # dtype 정수로 보정
df_3.insert(0, "Name", names)          # 첫 열에 Name 추가
```

### DataFrame 기본 조작
```python
# 열 선택
df["Age"]                # 단일 열(Series)
df[["Name", "Score"]]    # 복수 열(DataFrame)

# 행 선택/슬라이싱
df.iloc[0]               # 0번째 행
df.iloc[0:2]             # 0~1번째 행

# 조건 필터링
df[df["Age"] > 25]

# 열 추가/변환
df["Pass"] = df["Score"] > 80

# 정렬
df.sort_values("Score", ascending=False)

# 확인
df.head()
df.info()
df.describe()
```

### 시각화 (matplotlib 연동 예시)
```python
import matplotlib.pyplot as plt

plt.plot(df["Age"], df["Score"], marker="o")
plt.title("Age vs Score")
plt.xlabel("Age")
plt.ylabel("Score")
plt.show()
```

---

## NumPy vs Pandas 요약 비교

| 항목 | NumPy | Pandas |
|---|---|---|
| 주요 객체 | `ndarray` | `DataFrame`, `Series` |
| 주 목적 | 수치 계산, 배열 처리 | 테이블 데이터 분석/전처리 |
| 성능 | 매우 빠름(C 기반) | 상대적으로 느리지만 고수준 기능 |
| 생태계 | SciPy, scikit-learn 등과 궁합 | CSV/Excel/SQL/JSON 등 I/O에 강함 |

---

### 참고 팁
- `np.identity(n)` vs `np.eye(N, M=None, k=0)`
  - `identity`는 **정방 단위행렬 전용**
  - `eye`는 **행/열 다르게 지정** 가능, 대각선 오프셋 `k` 지원
- NumPy → Pandas 변환 시 **dtype 자동 승격(float화)** 을 주의하고, 필요 시 `astype()`으로 보정하세요.
