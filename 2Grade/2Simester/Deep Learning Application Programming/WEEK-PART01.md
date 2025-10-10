# 📚 딥러닝 응용 프로그래밍 핵심 요약 및 코드 분석 (2주차~5주차)

## 1. ⚙️ AI/ML 기초 및 데이터 전처리

| 구분 | 용어/개념 | 상세 기법/원리 | 코드 활용 (목적) |
| :--- | :--- | :--- | :--- |
| **기초** | **AI / ML / DL** | DL은 **인공신경망** 기반의 **ML**이며, 텐서플로(TensorFlow)는 이를 구현하는 핵심 프레임워크입니다. | ```python import tensorflow as tf # 딥러닝 핵심 라이브러리 로드 import pandas as pd # 데이터 처리 라이브러리 로드 ``` |
| **데이터** | **텐서 (Tensor)** | 딥러닝에서 데이터는 $\boldsymbol{N}$차원 배열 형태인 **텐서**로 표현되며, 텐서플로의 기본 연산 단위입니다. | ```python # 텐서 상수 생성 tensor = tf.constant([1.0, 2.0, 3.0]) ``` |
| **전처리** | **원-핫 인코딩** | 범주형 데이터에 순서나 가중치를 부여하지 않기 위해, 해당 범주에만 **1**을 부여한 **이진 벡터**로 변환합니다. | ```python # 원-핫 인코딩을 통한 가변수 생성 data = pd.DataFrame({'color': ['R', 'G', 'B']}) one_hot = pd.get_dummies(data, columns=['color']) ``` |

---

## 2. 🧠 지도 학습 핵심 알고리즘 (Scikit-learn)

| 알고리즘 | 유형 | 핵심 기법 및 원리 분석 | 코드 활용 (목적) |
| :--- | :--- | :--- | :--- |
| **K-NN** | 분류/회귀 | **게으른 학습자**. 새로운 데이터와 **$\boldsymbol{K}$개 이웃** 간의 **거리**를 측정하여 가장 가까운 이웃의 다수결로 분류/예측합니다. | ```python from sklearn.neighbors import KNeighborsClassifier # K-NN 분류기 정의 (K=5) model = KNeighborsClassifier(n_neighbors=5) model.fit(X_train, y_train) ``` |
| **SVM** | 분류 | **서포트 벡터**와 경계면(**초평면**) 사이의 **마진(Margin)을 최대화**하도록 결정 경계를 설정합니다. | ```python from sklearn.svm import SVC # SVM 분류기 구현 model = SVC() model.fit(X, y) ``` |
| **결정 트리** | 분류/회귀 | **불순도(지니 계수/엔트로피)**를 최소화하는 방향으로 분할을 반복하여 트리 구조를 형성. **과적합** 제어가 중요합니다. | ```python from sklearn.tree import DecisionTreeClassifier # 트리의 최대 깊이 제한 (과적합 제어) model = DecisionTreeClassifier(max_depth=5) model.fit(X, y) ``` |
| **로지스틱 회귀**| 분류 | 선형 회귀 결과에 **시그모이드 함수**를 적용하여 출력을 **확률($0 \sim 1$)**로 변환하여 분류에 사용. | ```python from sklearn.linear_model import LogisticRegression model = LogisticRegression() model.fit(X, y) ``` |

---

## 3. 💡 딥러닝 학습 원리 및 최적화 기법 (TensorFlow/Keras)

### 3.1. 모델 구성 및 활성화 함수

| 요소 | 기법/원리 상세 분석 | 코드 활용 (목적) |
| :--- | :--- | :--- |
| **활성화 함수** | **ReLU**: 은닉층에서 사용되어 비선형성을 부여하고 **학습 속도**를 높여 기울기 소실 문제 완화에 기여합니다. | ```python # 은닉층에 ReLU 적용 (비선형성 부여) tf.keras.layers.Dense(units=10, activation='relu') # 출력층에 Softmax 적용 (확률 변환) tf.keras.layers.Dense(units=3, activation='softmax') ``` |
| **CNN** | **합성곱 계층**(**Conv2D**)과 **풀링 계층**(**MaxPooling2D**)을 통해 이미지의 특징을 추출하고 차원을 축소합니다. | ```python # CNN 구조 정의 tf.keras.layers.Conv2D(filters=32, kernel_size=(3, 3), activation='relu') tf.keras.layers.MaxPooling2D(pool_size=(2, 2)) ``` |

### 3.2. 옵티마이저 (최적화)

| 최적화 기법 | 상세 원리 및 특징 | 코드 활용 (목적) |
| :--- | :--- | :--- |
| **경사 하강법 (GD)** | **손실 함수**의 **기울기**($\nabla L$)를 계산하여, **학습률**($\eta$)만큼 반대 방향으로 가중치를 업데이트하는 기본 원리. | ```python # 학습률을 설정한 SGD 옵티마이저 optim_gd = tf.keras.optimizers.SGD(learning_rate=0.01) ``` |
| **모멘텀 / NAG** | **모멘텀**은 이전 이동 방향에 **관성**을 부여해 수렴을 가속합니다. **NAG**는 관성이 적용될 미래 위치에서 미리 기울기를 계산해 안정성을 높입니다. | ```python # 모멘텀 및 NAG 기능을 활성화한 SGD 옵티마이저 optim_nag = tf.keras.optimizers.SGD(learning_rate=0.01, momentum=0.9, nesterov=True) model.compile(optimizer=optim_nag, loss='categorical_crossentropy') ``` **`momentum`** 및 **`nesterov=True`** 옵션을 통해 최적화 성능을 개선합니다. |

---

## 4. 🧭 비지도 학습 알고리즘 및 코드 분석

| 알고리즘 | 유형 | 핵심 기법 및 원리 분석 | 코드 활용 (목적) |
| :--- | :--- | :--- | :--- |
| **K-means** | 군집화 | **$\boldsymbol{K}$개**의 초기 **중심점**을 설정하고, 데이터 할당과 중심점 갱신을 반복하여 **SSD(오차 제곱 합)를 최소화**하며 군집을 형성. | ```python from sklearn.cluster import KMeans # 군집 개수 K=3으로 설정 model = KMeans(n_clusters=3, random_state=42) model.fit(data) ``` **`n_clusters`**를 지정하여 군집 모델을 학습. |
| **PCA** | 차원 축소 | 데이터의 **분산(정보량)**을 최대한 보존하는 **주성분** 축을 찾아 고차원 데이터를 저차원으로 압축. **시각화** 및 **노이즈 제거**에 효과적. | ```python from sklearn.decomposition import PCA # 2차원으로 차원 축소 pca = PCA(n_components=2) reduced_data = pca.fit_transform(data) ``` **`n_components`**로 **축소할 차원 수**를 지정하여 데이터를 전처리. |
| **DBSCAN** | 군집화 (밀도 기반) | **밀도**를 기준으로 군집을 식별. **$\boldsymbol{R}$ 범위(epsilon)** 내의 **최소 데이터 수(minPts)**를 만족하는지 여부로 군집을 형성. **이상치** 식별에 유용. | ```python from sklearn.cluster import DBSCAN # DBSCAN 모델 정의 model = DBSCAN(eps=0.5, min_samples=5) model.fit(data) ``` **`eps`** 및 **`min_samples`**를 설정하여 밀도 기반 군집화를 수행. |
