# 🧠 AI 2일차 학습 정리

## 📘 머신 러닝 (Machine Learning)
머신 러닝은 데이터로부터 규칙을 학습하여 스스로 판단하거나 예측하는 인공지능의 한 분야입니다.  
크게 **지도 학습**, **비지도 학습**, **강화 학습**으로 구분됩니다.

### 1️⃣ 지도 학습 (Supervised Learning)
- 입력 데이터(Input)와 정답(Label)이 함께 주어짐  
- 모델이 입력 → 정답의 관계를 학습하여 새로운 데이터를 예측  
- 예시: 스팸 메일 분류, 주가 예측, 이미지 인식

### 2️⃣ 비지도 학습 (Unsupervised Learning)
- 정답(Label)이 없는 데이터에서 숨겨진 패턴이나 구조를 찾음  
- 예시: 고객 세분화, 차원 축소, 군집화(Clustering)

### 3️⃣ 강화 학습 (Reinforcement Learning)
- 에이전트(Agent)가 환경(Environment)과 상호작용하며 보상(Reward)을 최대화하도록 학습  
- 예시: 게임 AI, 자율 주행, 로봇 제어


---

## 📈 선형 회귀 (Linear Regression)
선형 회귀는 입력 변수와 출력 변수 간의 **선형 관계**를 모델링하여 예측하는 알고리즘입니다.

### 🔹 가설 (Hypothesis)
- 예측 함수:  
  $$ h(x) = w_0 + w_1x $$  
  → 입력값 \( x \)에 대해 직선을 그려 예측값 \( h(x) \)를 구함
  ![h(x) = w₀ + w₁x](https://latex.codecogs.com/png.image?\dpi{120}&space;h(x)=w_0+w_1x)

### 🔹 비용함수 (Cost Function)
- 예측값과 실제값의 차이를 측정하는 함수  
  $$ J(w) = \frac{1}{2m}\sum_{i=1}^{m}(h(x_i) - y_i)^2 $$
  ![J(w) = \frac{1}{2m}\sum_{i=1}^{m}(h(x_i)-y_i)^2](https://latex.codecogs.com/png.image?\dpi{120}&space;J(w)=\frac{1}{2m}\sum_{i=1}^{m}(h(x_i)-y_i)^2)

### 🔹 평균 제곱 오차 (MSE, Mean Squared Error)
- 예측값과 실제값의 오차를 제곱해 평균을 낸 값  
  - 작을수록 모델의 성능이 좋음

### 🔹 최소 제곱법 (Least Squares)
- 오차 제곱합이 최소가 되도록 하는 회귀 계수 \( w \)를 구하는 방법

### 🔹 정규 방정식 (Normal Equation)
- 미분을 통해 오차를 최소화하는 해를 직접 계산  
  $$ w = (X^TX)^{-1}X^Ty $$
  ![w = (XᵀX)⁻¹Xᵀy](https://latex.codecogs.com/png.image?\dpi{120}&space;w=(X^TX)^{-1}X^Ty)

### 🔹 경사 하강법 (Gradient Descent)
- 비용함수를 최소화하기 위해 가중치를 반복적으로 조정하는 최적화 방법  
  $$ w := w - \alpha \frac{\partial J(w)}{\partial w} $$
  ![w := w - α ∂J(w)/∂w](https://latex.codecogs.com/png.image?\dpi{120}&space;w:=w-\alpha\frac{\partial&space;J(w)}{\partial&space;w})


---

## ⚙️ 로지스틱 회귀 (Logistic Regression)
로지스틱 회귀는 **이진 분류(Binary Classification)** 문제를 해결하는 알고리즘입니다.  
출력값이 0~1 사이의 확률로 표현됩니다.

### 🔹 시그모이드 함수 (Sigmoid Function)
- 선형 회귀 결과를 0~1 사이로 변환  
  $$ \sigma(x) = \frac{1}{1 + e^{-x}} $$
  ![σ(x) = 1 / (1 + e^{-x})](https://latex.codecogs.com/png.image?\dpi{120}&space;\sigma(x)=\frac{1}{1+e^{-x}})

### 🔹 이진 교차 엔트로피 (Binary Cross Entropy)
- 로지스틱 회귀의 비용함수로 사용  
  $$ J(w) = -\frac{1}{m}\sum[y\log(h(x)) + (1-y)\log(1-h(x))] $$
  ![J(w) = -\frac{1}{m}\sum[y\log(h(x)) + (1-y)\log(1-h(x))]](https://latex.codecogs.com/png.image?\dpi{120}&space;J(w)=-\frac{1}{m}\sum[y\log(h(x))+(1-y)\log(1-h(x))])

### 🔹 소프트맥스 함수 (Softmax Function)
- 여러 클래스 중 하나를 예측할 때 사용  
  $$ P(y_i) = \frac{e^{z_i}}{\sum_j e^{z_j}} $$
  ![P(y_i) = e^{z_i} / \sum_j e^{z_j}](https://latex.codecogs.com/png.image?\dpi{120}&space;P(y_i)=\frac{e^{z_i}}{\sum_j&space;e^{z_j}})


---

## 📚 정리
| 구분 | 주요 개념 | 핵심 포인트 |
|------|------------|--------------|
| 머신 러닝 | 지도/비지도/강화 학습 | 학습 데이터 존재 여부에 따른 분류 |
| 선형 회귀 | 가설, 비용함수, 경사하강법 | 연속형 예측 문제에 사용 |
| 로지스틱 회귀 | 시그모이드, 교차엔트로피 | 분류 문제(0/1)에 사용 |

---

> 💡 **Tip:**  
> 선형 회귀는 “값”을 예측하고,  
> 로지스틱 회귀는 “확률”을 예측합니다.
