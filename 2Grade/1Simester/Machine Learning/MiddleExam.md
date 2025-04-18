# ✅ 머신러닝 중간고사 정리 (예제 코드 포함)
## 1️⃣ 머신러닝이란?
정의: 데이터를 통해 스스로 학습하는 알고리즘

예시: 스팸 필터, 자율주행, 이미지 분류

python
복사
편집
# 스팸 필터 예시 (지도 학습, 분류 문제)
X = ["free money", "hi there", "win cash", "hello friend"]
y = [1, 0, 1, 0]  # 1 = spam, 0 = not spam
## 2️⃣ 머신러닝 분류

구분	설명	예시
지도 학습	레이블 있는 데이터 → 예측	분류, 회귀
비지도 학습	레이블 없음 → 구조 찾기	군집화, 차원 축소
강화 학습	보상 기반 학습	게임, 로봇 제어
python
복사
편집
# 지도 학습: 회귀 예제
from sklearn.linear_model import LinearRegression

X = [[1], [2], [3], [4]]
y = [2000, 4000, 6000, 8000]  # 거리(km) vs 택시 요금
model = LinearRegression()
model.fit(X, y)

print(model.predict([[3.5]]))  # [7000.]
## 3️⃣ 프로젝트 흐름
문제 정의

데이터 수집 & 시각화

전처리 (결측치, 정규화, 인코딩)

모델 훈련

평가 & 튜닝

배포 및 유지보수

python
복사
편집
### 데이터 나누기
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)
# 4️⃣ 전처리
🔹 결측치 처리
python
복사
편집
from sklearn.impute import SimpleImputer

imputer = SimpleImputer(strategy="median")
X = [[1, 2], [3, None], [7, 6]]
X_imputed = imputer.fit_transform(X)
🔹 범주형 데이터 인코딩
python
복사
편집
from sklearn.preprocessing import OneHotEncoder

encoder = OneHotEncoder()
encoded = encoder.fit_transform([["INLAND"], ["<1H OCEAN"]]).toarray()
# 5️⃣ 분류 예제 (MNIST)
python
복사
편집
from sklearn.datasets import fetch_openml
from sklearn.linear_model import SGDClassifier

mnist = fetch_openml("mnist_784", version=1, as_frame=False)
X, y = mnist.data, mnist.target
y = (y == "5")  # 5 감지기

clf = SGDClassifier()
clf.fit(X[:60000], y[:60000])
# 6️⃣ 모델 평가
python
복사
편집
from sklearn.model_selection import cross_val_score
from sklearn.metrics import precision_score, recall_score, f1_score

scores = cross_val_score(clf, X[:60000], y[:60000], cv=3, scoring="accuracy")
print("정확도:", scores)

# 정밀도, 재현율, F1 점수
from sklearn.model_selection import cross_val_predict
from sklearn.metrics import confusion_matrix

y_pred = cross_val_predict(clf, X[:60000], y[:60000], cv=3)
print("정밀도:", precision_score(y[:60000], y_pred))
print("재현율:", recall_score(y[:60000], y_pred))
print("F1 점수:", f1_score(y[:60000], y_pred))
# 7️⃣ SVM 분류기
python
복사
편집
from sklearn.svm import SVC
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
X_scaled = scaler.fit_transform(X[:2000])

svm_clf = SVC(kernel="poly", degree=3)
svm_clf.fit(X_scaled, y[:2000])
# 8️⃣ 회귀 예제 (주택 가격 예측)
python
복사
편집
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
import numpy as np

X = [[1], [2], [3], [4]]
y = [2.0, 4.0, 6.0, 8.0]  # 집 크기 vs 가격

model = LinearRegression()
model.fit(X, y)

predictions = model.predict([[5]])
rmse = np.sqrt(mean_squared_error([10], predictions))
print("예측:", predictions, "RMSE:", rmse)
# 9️⃣ 하이퍼파라미터 튜닝
python
복사
편집
from sklearn.model_selection import GridSearchCV
from sklearn.ensemble import RandomForestRegressor

param_grid = {
    "n_estimators": [10, 50],
    "max_features": [2, 4, 6]
}
grid_search = GridSearchCV(RandomForestRegressor(), param_grid, cv=3)
grid_search.fit(X_train, y_train)
# 🔟 배포 예시 (API 형태)
python
복사
편집
# Flask 예시
from flask import Flask, request, jsonify
app = Flask(__name__)

@app.route("/predict", methods=["POST"])
def predict():
    input_data = request.json["features"]
    prediction = model.predict([input_data])
    return jsonify({"prediction": prediction.tolist()})

# ✅ 머신러닝을 사용하는 이유 요약
전통적 프로그래밍 방식의 한계 극복

규칙 기반 프로그래밍은 규칙이 복잡해지고 길어질수록 유지보수가 어렵고, 정확도도 낮아지는 문제가 있음.
→ 머신러닝은 복잡한 규칙을 사람이 직접 정의하지 않고, 데이터에서 자동으로 학습하여 더 간단하고 효과적인 프로그램을 만들 수 있음.

자동으로 변화에 적응 가능

머신러닝 시스템은 새로운 데이터를 학습하여 변화하는 환경에 자동으로 적응할 수 있음.
예: 사용자가 스팸으로 지정한 단어(예: "For U")를 자동으로 학습해서 그 단어가 포함된 메일을 스팸으로 분류함.

대량의 데이터에서 유용한 패턴 발견 가능

데이터 마이닝 기능: 머신러닝은 방대한 데이터를 분석하여 사람이 찾기 어려운 숨겨진 패턴을 찾아냄.

복잡하거나 기존 규칙 기반 시스템으로는 해결이 어려운 문제 처리 가능

예측, 분류, 이상치 탐지 등 다양한 복잡한 문제를 기존 방식보다 더 높은 성능으로 해결.

유동적인 환경에서도 적응력 보장

모델은 새로운 데이터를 통해 쉽게 재훈련이 가능하여 항상 최신 상태 유지 가능.

정확도 향상

머신러닝 기법은 일반적으로 수동 규칙 기반보다 정확도가 높음.
예: 스팸 필터, 이미지 분류, 음성 인식 등

# ✅ 정리 요약
머신러닝은 데이터를 통한 학습이며, 전처리 → 모델 훈련 → 평가 → 배포 순서

지도 학습이 중심 (분류, 회귀)

SVM, 선형 회귀, 랜덤 포레스트, kNN 등 알고리즘 이해

정확도뿐 아니라 정밀도·재현율·F1 점수 활용한 평가 필수

실습 예제는 코드 중심으로 암기보단 실행하며 이해하는 것이 중요
