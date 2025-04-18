# ✅ 머신러닝 중간고사 정리 (예제 코드 포함)
## 1️⃣ 머신러닝이란?
정의: 데이터를 통해 스스로 학습하는 알고리즘

예시: 스팸 필터, 자율주행, 이미지 분류


# ✅ 머신러닝을 사용하는 이유 요약
## 전통적 프로그래밍 방식의 한계 극복

규칙 기반 프로그래밍은 규칙이 복잡해지고 길어질수록 유지보수가 어렵고, 정확도도 낮아지는 문제가 있음.
→ 머신러닝은 복잡한 규칙을 사람이 직접 정의하지 않고, 데이터에서 자동으로 학습하여 더 간단하고 효과적인 프로그램을 만들 수 있음.

## 자동으로 변화에 적응 가능

머신러닝 시스템은 새로운 데이터를 학습하여 변화하는 환경에 자동으로 적응할 수 있음.
예: 사용자가 스팸으로 지정한 단어(예: "For U")를 자동으로 학습해서 그 단어가 포함된 메일을 스팸으로 분류함.

## 대량의 데이터에서 유용한 패턴 발견 가능

데이터 마이닝 기능: 머신러닝은 방대한 데이터를 분석하여 사람이 찾기 어려운 숨겨진 패턴을 찾아냄.

## 복잡하거나 기존 규칙 기반 시스템으로는 해결이 어려운 문제 처리 가능

예측, 분류, 이상치 탐지 등 다양한 복잡한 문제를 기존 방식보다 더 높은 성능으로 해결.

## 유동적인 환경에서도 적응력 보장

모델은 새로운 데이터를 통해 쉽게 재훈련이 가능하여 항상 최신 상태 유지 가능.

## 정확도 향상

머신러닝 기법은 일반적으로 수동 규칙 기반보다 정확도가 높음.
예: 스팸 필터, 이미지 분류, 음성 인식 등

# 머신러닝의 종류

| 종류            | 설명                                         | 예시                                                       |
|-----------------|----------------------------------------------|------------------------------------------------------------|
| 지도 학습       | 입력과 정답(레이블)을 기반으로 학습           | 분류(스팸 필터, 손글씨 인식), 회귀(주택 가격 예측 등)       |
| 비지도 학습     | 레이블 없이 데이터 구조나 패턴을 학습         | 군집(고객 세분화), 차원 축소(PCA), 이상치 탐지, 연관 규칙 학습 |
| 강화 학습       | 보상/벌점을 통해 최적의 행동 전략 학습        | 게임 AI, 로봇 제어, 자율주행                               |
| 준지도 학습     | 일부만 레이블된 데이터로 학습                 | 소량의 레이블 + 대량의 무라벨 이미지 분류 등               |
| 자기 지도 학습  | 데이터로부터 스스로 레이블 생성해 학습        | GPT, BERT, CLIP 등 사전학습 언어/비전 모델                 |
| 배치 학습       | 모든 데이터를 한꺼번에 학습 (오프라인)         | 대규모 데이터셋을 활용한 모델 학습                         |
| 온라인 학습     | 데이터를 순차적으로 받아 점진적으로 학습       | 실시간 추천 시스템, 금융 트레이딩 시스템                   |
| 사례 기반 학습  | 과거 사례와의 유사도 기반 예측                | K-최근접 이웃(K-NN), 메모리 기반 알고리즘                   |
| 모델 기반 학습  | 일반화된 수학적 모델을 만들어 예측            | 선형 회귀, 결정 트리, SVM, 신경망 등                       |

# 📌 지도 학습(Supervised Learning)
from sklearn.datasets import load_digits
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score

## 데이터 로드
digits = load_digits()
X_train, X_test, y_train, y_test = train_test_split(digits.data, digits.target, test_size=0.2, random_state=42)

## 모델 생성 및 학습
model = RandomForestClassifier(n_estimators=100, random_state=42)
model.fit(X_train, y_train)

## 예측 및 평가
y_pred = model.predict(X_test)
accuracy = accuracy_score(y_test, y_pred)
print(f"정확도: {accuracy:.2f}")



# 📌 비지도 학습(Unsupervised Learning) - K-Means 군집화
from sklearn.cluster import KMeans
from sklearn.datasets import make_blobs
import matplotlib.pyplot as plt

## 데이터 생성
X, _ = make_blobs(n_samples=300, centers=3, cluster_std=0.60, random_state=42)

## K-Means 모델 학습
kmeans = KMeans(n_clusters=3, random_state=42)
kmeans.fit(X)
y_kmeans = kmeans.predict(X)

## 데이터 시각화
plt.scatter(X[:, 0], X[:, 1], c=y_kmeans, cmap='viridis')
plt.scatter(kmeans.cluster_centers_[:, 0], kmeans.cluster_centers_[:, 1], s=200, c='red', marker='X')
plt.show()



# 📌 강화 학습(Reinforcement Learning) - Q-Learning 예제
import numpy as np

## Q 테이블 초기화
Q = np.zeros((5, 5))

## 파라미터 설정
alpha = 0.1  # 학습률
gamma = 0.9  # 할인율
epsilon = 0.1  # 탐색 확률

## 학습 과정 (단순 예제)
for episode in range(100):
    state = np.random.randint(5)
    for step in range(10):
        if np.random.rand() < epsilon:
            action = np.random.randint(5)  # 랜덤 행동 선택
        else:
            action = np.argmax(Q[state])  # 최적 행동 선택
        reward = np.random.randint(-1, 2)  # 보상 설정
        Q[state, action] = Q[state, action] + alpha * (reward + gamma * np.max(Q[action]) - Q[state, action])

print("학습된 Q 테이블:")
print(Q)



이렇게 정리하면 코드 부분만 배경색이 다르게 표시되어 가독성이 좋을 거예요. 필요한 부분이 더 있으면 알려주세요! 😊

# ✅ 머신러닝의 주요 도전 과제

| 도전 과제               | 설명                                                                                   |
|------------------------|----------------------------------------------------------------------------------------|
| 믿기 힘든 데이터의 효과 | 알고리즘보다 양질의 데이터가 더 중요함. 충분한 데이터만 있다면 단순한 알고리즘도 성능이 좋을 수 있음 |
| 데이터 부족            | 머신러닝은 많은 양의 훈련 데이터가 필요. 특히 이미지/음성은 수천~수백만 개 필요함                |
| 대표성 부족            | 훈련 데이터가 실제 문제를 잘 대표하지 못하면 일반화가 어렵고 성능 저하                         |
| 낮은 데이터 품질       | 이상치, 오류, 누락된 값 등 데이터 정제가 반드시 필요                                      |
| 관련 없는 특성         | 불필요하거나 상관없는 특성이 많으면 모델 학습을 방해함 → 특성 선택/추출 필요                  |
| 과대적합 (Overfitting) | 모델이 훈련 데이터에 너무 맞춰져 새 데이터에서 성능이 나쁨                                 |
| 과소적합 (Underfitting)| 모델이 너무 단순하거나 학습이 부족하여 데이터의 구조를 잘 학습하지 못함                     |
| 잡음 많은 데이터       | 노이즈가 많은 데이터는 모델이 엉뚱한 패턴을 학습하게 만듦                                   |
| 하이퍼파라미터 설정 문제 | 학습률, 규제 계수 등의 잘못된 설정은 성능 저하로 이어짐                                  |
| 성능 모니터링 어려움   | 특히 온라인 학습에서 실시간으로 성능 감시 및 조치가 필요                                    |
| 모델 부패 (Model Rot)  | 시간이 지나면서 데이터 분포가 바뀌면 기존 모델이 점점 성능이 나빠짐 → 재학습 필요              |

# ✅ 머신러닝의 테스트와 검증 정리

| 항목                    | 설명                                                                                  |
|-------------------------|-----------------------------------------------------------------------------------------|
| 훈련 세트 (Training Set) | 모델을 학습시키는 데 사용하는 데이터셋                                                |
| 테스트 세트 (Test Set)   | 모델이 학습하지 않은 데이터로 성능을 평가하기 위한 셋                                  |
| 검증 목적               | 모델이 **새로운 데이터에 얼마나 잘 일반화되는지** 확인하기 위해 사용                   |
| 일반화 오차             | 테스트 세트에서 측정한 오류 비율 → 새로운 샘플에 대한 **예상 오차**                      |
| 과대적합 확인            | 훈련 오차는 낮지만 테스트 오차가 높다면 과대적합됨                                      |
| 훈련/테스트 분리 비율    | 일반적으로 **80% 훈련 / 20% 테스트**, 데이터셋 크기에 따라 유동적으로 조절 가능            |
| 데이터 스누핑 방지       | 테스트 세트는 **절대 훈련에 사용하지 않도록 주의**                                     |
| 교차 검증 (Cross Validation) | 데이터를 여러 조각으로 나눠서 반복적으로 훈련/테스트 진행 → **평균 성능을 추정**               |
| k-폴드 교차 검증        | 데이터를 k개의 폴드로 나눠, 그 중 하나를 테스트 세트로 사용하고 나머지를 훈련에 사용 → k번 반복 |
| 검증 세트 (Validation Set) | 하이퍼파라미터 튜닝 등을 위한 추가적인 평가용 데이터셋 (훈련/검증/테스트로 나누기도 함)        |

# ✅ 머신러닝 프로젝트 전체 프로세스 요약 (처음부터 끝까지)

| 단계               | 설명                                                                                   |
|--------------------|------------------------------------------------------------------------------------------|
| 1. 문제 정의       | - 비즈니스 목적 이해<br>- 예측해야 할 대상 정의<br>- 회귀/분류/군집 등 문제 유형 파악   |
| 2. 데이터 수집     | - 다양한 소스로부터 데이터 수집 (CSV, DB, API 등)<br>- 신뢰성과 품질 확인               |
| 3. 데이터 탐색     | - 데이터 구조 파악 (`head()`, `info()`, `describe()` 등)<br>- 시각화 및 상관관계 분석    |
| 4. 데이터 전처리   | - 결측치 처리, 이상치 제거<br>- 범주형/수치형 인코딩<br>- 정규화/표준화                  |
| 5. 특성 엔지니어링 | - 특성 선택/추출<br>- 새로운 유용한 피처 생성<br>- 도메인 지식 활용                     |
| 6. 데이터 분할     | - 훈련/검증/테스트 세트 분할<br>- 계층적 샘플링 사용 권장                               |
| 7. 모델 선택       | - 적절한 알고리즘 선택 (선형 회귀, 결정 트리, 랜덤 포레스트 등)<br>- 베이스라인 모델 구축 |
| 8. 모델 훈련       | - 훈련 세트를 사용해 모델 학습<br>- 비용 함수 최소화로 최적 파라미터 찾기               |
| 9. 모델 평가       | - 검증 세트 또는 교차 검증으로 성능 측정<br>- RMSE, MAE, 정확도, F1, ROC 등 사용         |
|10. 하이퍼파라미터 튜닝| - GridSearchCV 또는 RandomizedSearchCV 사용<br>- 최적 모델 파라미터 탐색             |
|11. 최종 테스트     | - 테스트 세트로 최종 성능 평가<br>- 일반화 능력 확인                                   |
|12. 배포            | - 웹 서비스(API) 또는 앱에 모델 통합<br>- 모델을 pickle, joblib 등으로 저장 후 로드      |
|13. 모니터링 & 유지보수| - 성능 모니터링 및 재학습 필요 시 업데이트<br>- 데이터 드리프트 탐지 및 조치          |

## 데이터 다운 및 로드
from pathlib import Path
import pandas as pd
import tarfile
import urllib.request

def load_housing_data():
    tarball_path = Path("datasets/housing.tgz")
    if not tarball_path.is_file():
        Path("datasets").mkdir(parents=True, exist_ok=True)
        url = "https://github.com/ageron/data/raw/main/housing.tgz"
        urllib.request.urlretrieve(url, tarball_path)
    with tarfile.open(tarball_path) as housing_tarball:
        housing_tarball.extractall(path="datasets")
    
    return pd.read_csv(Path("datasets/housing/housing.csv"))

housing = load_housing_data()

## 데이터 탐색 시각화
import matplotlib.pyplot as plt

housing.hist(bins=50, figsize=(12, 8))
plt.show()

## 데이터 전처리 및 모델 훈련
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LinearRegression

### 데이터 분리
X = housing.drop("median_house_value", axis=1)
y = housing["median_house_value"]

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

### 데이터 스케일링
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

### 선형 회귀 모델 훈련
model = LinearRegression()
model.fit(X_train_scaled, y_train)

### 예측 및 평가
y_pred = model.predict(X_test_scaled)

## 모델 평가
from sklearn.metrics import mean_squared_error

rmse = mean_squared_error(y_test, y_pred, squared=False)
print(f"테스트 데이터 RMSE: {rmse}")

# 머신러닝의 분류 방법

| 분류 기준           | 분류 방식                     | 설명                                                                 |
|----------------------|------------------------------|----------------------------------------------------------------------|
| **지도 방식**         | - 지도 학습 (Supervised)      | 입력과 정답(레이블) 존재. 예: 회귀, 분류                              |
|                      | - 비지도 학습 (Unsupervised)  | 레이블 없음. 예: 군집, 차원 축소                                     |
|                      | - 준지도 학습 (Semi-Supervised)| 일부 레이블만 있는 데이터로 학습                                      |
|                      | - 자기 지도 학습 (Self-Supervised)| 입력으로부터 레이블 생성해 학습. 예: GPT 등                            |
|                      | - 강화 학습 (Reinforcement)   | 보상/벌점을 통해 최적 정책을 학습                                     |
| **학습 시점**         | - 배치 학습 (Batch)           | 전체 데이터를 한꺼번에 학습                                           |
|                      | - 온라인 학습 (Online)        | 데이터를 순차적으로 받아 점진적으로 학습                              |
| **일반화 방식**       | - 사례 기반 학습 (Instance-based) | 훈련 샘플을 기억, 유사도 비교로 예측. 예: K-NN                        |
|                      | - 모델 기반 학습 (Model-based)| 모델을 수학적으로 일반화해서 예측. 예: 선형 회귀, 신경망 등           |

# 📌 MNIST 데이터셋 다운로드 및 로드
from sklearn.datasets import fetch_openml

## MNIST 데이터셋을 다운로드하고 로드
mnist = fetch_openml('mnist_784', as_frame=False)

## 입력 데이터(X)와 레이블(y) 분리
X, y = mnist.data, mnist.target



# 📌 데이터셋 분리 및 시각화
import matplotlib.pyplot as plt

## 훈련 데이터와 테스트 데이터 분리
X_train, X_test, y_train, y_test = X[:60000], X[60000:], y[:60000], y[60000:]

## 숫자 이미지 확인 함수
def plot_digit(image_data):
    image = image_data.reshape(28, 28)
    plt.imshow(image, cmap="binary")
    plt.axis("off")
    plt.show()

## 샘플 숫자 출력
some_digit = X[0]
plot_digit(some_digit)

## 실제 레이블 확인
print(y[0])  # '5'



# 📌 이진 분류기(SGDClassifier)
from sklearn.linear_model import SGDClassifier

## '5'를 감지하는 이진 분류기 학습
y_train_5 = (y_train == '5')  # '5'면 True, 나머지는 False
y_test_5 = (y_test == '5')

sgd_clf = SGDClassifier(random_state=42)
sgd_clf.fit(X_train, y_train_5)

## 예측 실행
print(sgd_clf.predict([some_digit]))  # True



# 📌 다중 분류 (OvR & OvO 전략)
from sklearn.svm import SVC
from sklearn.multiclass import OneVsRestClassifier

## SVC 기반으로 다중 분류 수행
svm_clf = SVC(random_state=42)
svm_clf.fit(X_train[:2000], y_train[:2000])  # 샘플 데이터를 사용해 학습

## 예측 실행
print(svm_clf.predict([some_digit]))  # ['5']

## OvR 전략 강제 적용
ovr_clf = OneVsRestClassifier(SVC(random_state=42))
ovr_clf.fit(X_train[:2000], y_train[:2000])

## 예측 실행
print(ovr_clf.predict([some_digit]))  # ['5']



# 📌 성능 평가 및 교차 검증
from sklearn.model_selection import cross_val_score
from sklearn.preprocessing import StandardScaler

## 데이터 스케일링 및 SGDClassifier 학습
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train.astype("float64"))

sgd_clf.fit(X_train_scaled, y_train)

## 교차 검증 평가
print(cross_val_score(sgd_clf, X_train_scaled, y_train, cv=3, scoring="accuracy"))



이 코드들은 MNIST 데이터셋을 활용한 머신러닝 분류 학습 과정에서 중요한 부분을 정리한 것입니다. 필요하신 추가 내용이 있으면 언제든 말씀해주세요! 😊


# SWM

| 개념          | 설명 |
|--------------|--------------------------------------------------------|
| **SVM(Support Vector Machine)** | 데이터 포인트를 분류하는 강력한 머신러닝 알고리즘 |
| **라지 마진 분류** | 서로 다른 클래스의 데이터를 최대한 분리하는 경계를 찾음 |
| **서포트 벡터** | 결정 경계를 형성하는 중요한 데이터 포인트 |
| **하드 마진 분류** | 모든 샘플이 마진 밖에 있도록 결정 경계를 설정 (이상치에 민감) |
| **소프트 마진 분류** | 마진 내 샘플이 허용되며, 일정 수준의 오류를 감내하여 일반화 성능을 높임 |
| **C 값** | 마진을 조정하는 하이퍼파라미터 (작으면 마진 넓고, 크면 마진 좁음) |
| **비선형 분류** | 데이터를 변환하여 선형적으로 구분할 수 있도록 변형 |
| **커널 트릭** | 높은 차원의 공간에서 데이터를 변환하여 선형적으로 분류하는 기법 |
| **다항식 커널** | 다항식을 이용하여 데이터 포인트의 변환을 수행 |
| **가우스 RBF 커널** | 데이터 간의 거리를 기반으로 특성을 변환하여 복잡한 결정 경계를 생성 |
| **SVM 회귀** | 마진 오류 안에서 가장 많은 데이터 포인트를 포함하는 회귀 모델을 생성 |
| **LinearSVC** | 선형 SVM 분류를 수행하는 모델 (대규모 데이터셋에 적합) |
| **SVR** | SVM을 이용한 회귀 모델 |****

# 📌 선형 SVM 분류 - 붓꽃 데이터셋 활용
from sklearn.datasets import load_iris
from sklearn.pipeline import make_pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.svm import LinearSVC

## 데이터 로드
iris = load_iris(as_frame=True)
X = iris.data[["petal length (cm)", "petal width (cm)"]].values
y = (iris.target == 2)  # Iris-Virginica 감지

## 선형 SVM 모델 학습
svm_clf = make_pipeline(StandardScaler(), LinearSVC(C=1, random_state=42))
svm_clf.fit(X, y)

## 예측 실행
X_new = [[5.5, 1.7], [5.0, 1.5]]
print(svm_clf.predict(X_new))



# 📌 비선형 SVM 분류 - 다항식 커널 사용
from sklearn.datasets import make_moons
from sklearn.preprocessing import PolynomialFeatures
from sklearn.svm import SVC

## 데이터 생성
X, y = make_moons(n_samples=100, noise=0.15, random_state=42)

## 다항 커널 SVM 모델 학습
poly_kernel_svm_clf = make_pipeline(StandardScaler(),
                                    SVC(kernel="poly", degree=3, coef0=1, C=5))
poly_kernel_svm_clf.fit(X, y)



# 📌 가우스 RBF 커널을 이용한 비선형 SVM 분류
from sklearn.svm import SVC

## RBF 커널을 사용한 SVM 모델
rbf_kernel_svm_clf = make_pipeline(StandardScaler(), 
                                   SVC(kernel="rbf", gamma=5, C=0.001))
rbf_kernel_svm_clf.fit(X, y)



# 📌 SVM을 활용한 회귀 모델 학습
from sklearn.svm import SVR
import numpy as np

## 데이터 생성
X = np.linspace(-1, 1, 100).reshape(-1, 1)
y = X**2 + np.random.randn(100, 1) * 0.1  # 2차 함수 데이터

## SVM 회귀 모델 학습
svm_poly_reg = make_pipeline(StandardScaler(),
                            SVR(kernel="poly", degree=2, C=0.01, epsilon=0.1))
svm_poly_reg.fit(X, y.ravel())



이렇게 정리하면 코드 부분만 배경색이 다르게 표시되므로 가독성이 좋을 거예요.
추가적으로 필요한 부분이 있으면 말씀해주세요! 😊

# 실습코드
## 📌 🚖 택시 요금 예측 실습 코드
import numpy as np
import pandas as pd
from sklearn.linear_model import LinearRegression

### 가상의 택시 요금 데이터 생성
data = {"Distance": [1, 5, 10, 15, 20], "Fare": [2000, 7000, 12000, 17000, 22000]}
df = pd.DataFrame(data)

### 데이터 분리
X = df[["Distance"]]
y = df[["Fare"]]

### 선형 회귀 모델 학습
model = LinearRegression()
model.fit(X, y)

### 새로운 거리(3.5km)에 대한 예상 요금 예측
X_test = [[3.5]]
predicted_fare = model.predict(X_test)
print(f"3.5km 이동 시 예상 요금: {predicted_fare[0][0]}원")



## 📌 🎮 FIFA 선수 포지션 예측 코드
데이터 전처리 및 모델 학습
import pandas as pd
import pickle
from sklearn.model_selection import train_test_split
from sklearn.svm import SVC
from sklearn.preprocessing import StandardScaler
from sklearn.metrics import accuracy_score

### 데이터 로드
df = pd.read_csv("./data/fifa_data.csv")

### 필요한 컬럼 선택 및 전처리
df = df[['Name', 'Position', 'Crossing', 'Finishing', 'HeadingAccuracy',
         'ShortPassing', 'Volleys', 'Dribbling', 'BallControl', 'Acceleration',
         'SprintSpeed', 'Interceptions', 'Positioning', 'Vision', 'Penalties',
         'Marking', 'StandingTackle', 'SlidingTackle', 'GKDiving', 'GKHandling',
         'GKKicking', 'GKPositioning', 'GKReflexes']]
df.dropna(inplace=True)

### 데이터 분할
X = df.drop(['Name', 'Position'], axis=1)
y = df["Position"]
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

### 데이터 스케일링
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

### SVM 모델 학습
svm_clf = SVC(kernel="rbf", C=10, gamma=0.0001)
svm_clf.fit(X_train_scaled, y_train)

### 예측 및 평가
y_pred = svm_clf.predict(X_test_scaled)
accuracy = accuracy_score(y_test, y_pred)
print(f"FIFA 포지션 예측 정확도: {accuracy:.2f}")



이렇게 정리하면 코드 부분만 배경색이 다르게 표시되어 가독성이 좋을 거예요. 추가적으로 필요한 부분이 있으면 언제든 말씀해주세요! 😊


# ✅ 정리 요약
머신러닝은 데이터를 통한 학습이며, 전처리 → 모델 훈련 → 평가 → 배포 순서

지도 학습이 중심 (분류, 회귀)

SVM, 선형 회귀, 랜덤 포레스트, kNN 등 알고리즘 이해

정확도뿐 아니라 정밀도·재현율·F1 점수 활용한 평가 필수

실습 예제는 코드 중심으로 암기보단 실행하며 이해하는 것이 중요
