알겠습니다. 제공해주신 컴퓨터 비전 강의 자료 PDF 파일들의 내용을 개념, 계산 방법 등을 포함하여 자세히 요약하고, 표 형식화가 가능한 부분은 표로 만들어 마크다운 코드로 정리해 드리겠습니다.

---

## 1. 컴퓨터 비전 소개 (2주차)

### 인간의 시각 vs 컴퓨터 비전

#### 인간의 시각 👀
* [cite_start]**능력:** 분류, 검출, 분할, 추적, 행동 분석 등에 능숙하며 3차원 복원 능력도 뛰어남[cite: 858]. [cite_start]빠르고 강건하며 [cite: 859][cite_start], 지식 표현, 추론 등 다른 지능 요소와 협력함[cite: 860]. [cite_start]비주얼 서보잉(Visual Servoing)과 과업 전환(Task Switching)도 우수함[cite: 862, 863].
* [cite_start]**한계:** 착시 현상에 취약하고 [cite: 865][cite_start], 정밀 측정에 오차가 있으며 [cite: 866][cite_start], 시야가 한정되고 [cite: 867][cite_start], 피로와 퇴화가 발생함[cite: 868].

#### 컴퓨터 비전 (CV) 💻
* [cite_start]**정의:** 인간의 시각 능력을 모방하는 컴퓨터 프로그램[cite: 917]. [cite_start]영상을 이해하고 판단하는 기술[cite: 913].
* **목표:**
    * [cite_start]**궁극적 목표 (강한 인공지능):** 일반적인 상황에서 인간처럼 잘 작동하는 시각 구현[cite: 926]. [cite_start]아직은 먼 미래의 목표임[cite: 926].
    * [cite_start]**현실적 목표 (약한 인공지능):** 제한된 환경에서 특정 과업을 높은 성능으로 달성[cite: 926]. [cite_start]세부 문제별 알고리즘 개발[cite: 926].
* [cite_start]**주요 과업:** 분류(Classification), 검출(Detection), 분할(Segmentation), 추적(Tracking), 행동 분석(Action Recognition) 등[cite: 914, 927].
* [cite_start]**어려움:** 시점, 조명 등에 따라 물체 모습이 계속 변하고 [cite: 921][cite_start], 숫자로 이루어진 데이터(픽셀 값)로부터 의미를 해석해야 함[cite: 921]. [cite_start]현재 기술은 약인공지능 수준임[cite: 921].

### 영상 처리 vs 컴퓨터 비전

| 구분         | 영상 처리 (Image Processing) | 컴퓨터 비전 (Computer Vision)            |
| :----------- | :------------------------------------------- | :------------------------------------------------------ |
| **정의** | [cite_start]영상을 가공/보정하는 기술 [cite: 884, 913]         | [cite_start]영상을 이해하고 판단하는 기술 [cite: 913]                 |
| **입/출력** | [cite_start]영상 → 영상 [cite: 883, 915]               | [cite_start]영상 → 심볼 (정보, 판단) [cite: 915]                    |
| **주요 기법** | [cite_start]노이즈 제거, 대비 조절, 필터링 등 [cite: 896, 897, 913]    | [cite_start]분류, 검출, 분할, 추적, 행동 분석 등 [cite: 914]       |
| **응용 분야** | [cite_start]의료 영상, 사진 보정 등 [cite: 913]           | [cite_start]자율주행, 얼굴 인식, AR/VR 등 [cite: 914]             |

**영상 처리 기술 분야 요약**

| 기술 분야        | 요약                                                                |
| :--------------- | :------------------------------------------------------------------ |
| 디지털 영상 개선 | [cite_start]영상의 화질을 **주관적으로** 향상시키는 기술 [cite: 895, 896, 898]                   |
| 디지털 영상 복원 | [cite_start]손상된 영상을 원본 영상과 가깝게 **객관적으로** 복원시키는 기술 [cite: 895, 900] |
| 디지털 영상 변환 | [cite_start]디지털 영상을 다른 형태의 데이터(예: 주파수)로 변환하는 작업 [cite: 895, 902]   |
| 디지털 영상 분석 | [cite_start]디지털 영상으로부터 원하는 정보(통계적/구조적)를 추출하는 작업 [cite: 895, 905] |
| 디지털 영상 압축 | [cite_start]영상을 효율적으로 저장/전송하기 위해 중복/불필요 부분을 제거하는 작업 [cite: 895, 906] |

---

## 2. 디지털 영상 기초 (3, 4주차)

### 디지털 영상 획득 📸
* [cite_start]빛(에너지)을 센서로 감지하여 영상을 형성함[cite: 749].
* [cite_start]연속적인 장면(실제 물체)을 **샘플링(Sampling)** 과 **양자화(Quantization)** 과정을 거쳐 디지털 영상(픽셀 값의 배열)으로 변환함[cite: 749, 755, 779].

### 샘플링 & 양자화
* [cite_start]**샘플링 (Sampling):** 이미지를 몇 개의 픽셀로 표현할지 결정 (공간 해상도)[cite: 781, 784]. [cite_start]간격이 좁을수록 고해상도[cite: 786].
* [cite_start]**양자화 (Quantization):** 각 픽셀의 밝기(또는 색)를 몇 단계로 표현할지 결정 (밝기 해상도)[cite: 782, 788]. [cite_start]단계($L$)는 보통 $2^k$로 표현됨 ($k$는 비트 수)[cite: 798].
    * [cite_start]$k=1$: 이진 영상 (흑/백, L=2) [cite: 799]
    * [cite_start]$k=8$: 명암 영상 (grayscale, L=256, 0~255) [cite: 799]

### 디지털 영상 표현
* [cite_start]**좌표계:** 일반적으로 영상의 왼쪽 위 구석이 원점(0, 0)이며, x축은 오른쪽, y축은 아래쪽 방향임[cite: 156, 157]. [cite_start]$f(j, i)$는 j행, i열의 픽셀 값을 의미함[cite: 159].
* [cite_start]**자료 구조 (OpenCV/NumPy):** OpenCV에서는 영상을 `numpy.ndarray` 객체로 표현함[cite: 161]. [cite_start]따라서 NumPy의 다양한 배열 함수(min, max, mean, shape, sort, transpose 등)를 활용할 수 있음[cite: 162, 163].
* **영상 종류 및 텐서 표현:**
    * [cite_start]명암 영상 (Grayscale): 2차원 텐서 (Height, Width) [cite: 229]
    * [cite_start]컬러 영상 (Color): 3차원 텐서 (Height, Width, Channels)[cite: 234]. [cite_start]OpenCV에서는 주로 BGR 순서[cite: 815].
    * [cite_start]컬러 동영상 (Color Video): 4차원 텐서 (Time, Height, Width, Channels) [cite: 235]
    * [cite_start]다분광/초분광/의료 영상 (Multispectral/Hyperspectral/MR/CT): 3차원 또는 그 이상 [cite: 240]
    * [cite_start]RGB-D 영상: 컬러 + 깊이 정보 [cite: 244]
    * [cite_start]점 구름 (Point Cloud): 3D 좌표 집합, 주로 LiDAR로 획득 [cite: 245, 246]

### 컬러 모델 🎨
* [cite_start]**RGB:** 빛의 삼원색(Red, Green, Blue)을 혼합하는 가산 모델[cite: 271]. [cite_start]각 색상의 강도를 조절하여 표현하며, 정육면체(큐브) 형태로 시각화 가능[cite: 272].
* [cite_start]**HSV:** 색상(Hue), 채도(Saturation), 명도(Value)의 세 요소로 색을 표현[cite: 277]. 인간의 색상 인식 방식과 유사함.

### OpenCV 기본 함수 (3주차)

| 함수                     | 설명                                                                 | 예시 (Python)                                                              |
| :----------------------- | :------------------------------------------------------------------- | :------------------------------------------------------------------------- |
| `cv.imread()`            | [cite_start]파일에서 이미지를 읽어 `numpy.ndarray` 객체로 반환 [cite: 171]           | [cite_start]`img = cv.imread('soccer.jpg')` [cite: 171]                                          |
| `cv.imshow()`            | [cite_start]창(window)에 이미지를 표시 [cite: 814]                                  | [cite_start]`cv.imshow('Image Display', img)` [cite: 814]                                          |
| `cv.imwrite()`           | [cite_start]`numpy.ndarray` 이미지를 파일로 저장 [cite: 818]                         | [cite_start]`cv.imwrite('soccer_gray.png', gray)` [cite: 818]                                    |
| `cv.waitKey()`           | [cite_start]지정된 시간(ms) 동안 또는 키 입력이 있을 때까지 대기 [cite: 210, 814]       | [cite_start]`key = cv.waitKey(0)` [cite: 210]                                                      |
| `cv.destroyAllWindows()` | [cite_start]열려있는 모든 OpenCV 창을 닫음 [cite: 212, 814]                              | [cite_start]`cv.destroyAllWindows()` [cite: 212]                                                   |
| `cv.cvtColor()`          | [cite_start]이미지의 컬러 공간을 변환 (예: BGR → Gray) [cite: 818]                  | [cite_start]`gray = cv.cvtColor(img, cv.COLOR_BGR2GRAY)` [cite: 818]                               |
| `cv.resize()`            | [cite_start]이미지 크기 변경[cite: 818]. 보간법 지정 가능                | [cite_start]`small = cv.resize(gray, dsize=(0,0), fx=0.5, fy=0.5)` [cite: 818]                     |
| `cv.VideoCapture()`      | [cite_start]비디오 파일이나 카메라로부터 영상을 받아오는 객체 생성 [cite: 822]             | [cite_start]`cap = cv.VideoCapture(0)` [cite: 822]                                                 |
| `cap.read()`             | [cite_start]VideoCapture 객체로부터 다음 프레임을 읽음 [cite: 822]             | [cite_start]`ret, frame = cap.read()` [cite: 822]                                                  |
| `cap.release()`          | [cite_start]VideoCapture 객체를 해제 [cite: 822]                                   | [cite_start]`cap.release()` [cite: 822]                                                            |
| `cv.rectangle()`         | [cite_start]이미지에 사각형 그리기 [cite: 828]                                  | [cite_start]`cv.rectangle(img, (x1,y1), (x2,y2), (0,0,255), 2)` [cite: 832]                       |
| `cv.putText()`           | [cite_start]이미지에 텍스트 쓰기 [cite: 828]                                    | [cite_start]`cv.putText(img, 'laugh', (830,24), cv.FONT_HERSHEY_SIMPLEX, 1, (255,0,0), 2)` [cite: 832] |
| `cv.circle()`            | [cite_start]이미지에 원 그리기 [cite: 838]                                    | [cite_start]`cv.circle(img, (x,y), BrushSiz, LColor, -1)` [cite: 838]                             |
| `cv.setMouseCallback()`  | [cite_start]특정 창에서의 마우스 이벤트 발생 시 호출될 콜백 함수 지정 [cite: 835] | [cite_start]`cv.setMouseCallback('Painting', painting)` [cite: 838]                                |

[cite_start]**컬러→명암 변환 공식:** $I = round(0.299 \times R + 0.587 \times G + 0.114 \times B)$ [cite: 820]

---

## 3. 영상 연산의 종류 (4, 5주차)

[cite_start]결과 이미지의 한 픽셀 값을 결정할 때 참조하는 원본 이미지의 픽셀 범위에 따라 분류됨[cite: 325].

| 연산 종류           | 설명                                                                                                                               | 예시                                                                 |
| :------------------ | :--------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------- |
| **점 연산 (Point)** | [cite_start]결과 픽셀 값이 원본의 **같은 위치 픽셀 하나**에만 의존 [cite: 326]                                                                         | [cite_start]밝기/명암 조절(감마 보정, 히스토그램 평활화), 색상 반전 등 [cite: 326, 328] |
| **영역 연산 (Area)** | [cite_start]결과 픽셀 값이 원본의 **해당 위치 주변 픽셀들**에도 의존[cite: 326]. [cite_start]주로 **컨볼루션(Convolution)** 연산을 통해 이루어짐 [cite: 346] | [cite_start]블러(Blurring), 샤프닝(Sharpening), 에지 검출, 모폴로지 [cite: 326] |
| **기하 연산 (Geo.)** | [cite_start]결과 픽셀 값이 원본 이미지의 **좌표 변환**을 통해 결정됨 [cite: 327]                                                                 | [cite_start]확대/축소(크기 변경), 이동(Translation), 회전(Rotation), 뒤집기 등 [cite: 327] |

---

## 4. 점 연산 (Point Operations) (4주차)

### 감마 보정 (Gamma Correction)
* [cite_start]비선형 밝기 조절 기법[cite: 328]. [cite_start]입력 픽셀 값 $I$ (0~1로 정규화)에 대해 출력 $O = I^{\gamma}$ 계산[cite: 329].
* [cite_start]$\gamma < 1$: 이미지가 밝아짐[cite: 329].
* [cite_start]$\gamma = 1$: 변화 없음[cite: 329].
* [cite_start]$\gamma > 1$: 이미지가 어두워짐[cite: 329].
* [cite_start]인간 시각 특성이나 디스플레이 장치 특성을 보정하는 데 사용[cite: 328].

### 히스토그램 평활화 (Histogram Equalization)
* [cite_start]이미지의 픽셀 값 분포(히스토그램)를 균일하게 만들어 명암 대비를 향상시키는 기법[cite: 328, 330].
* [cite_start]픽셀 값들이 특정 범위에 몰려 있는 어둡거나 밝은 영상의 대비를 효과적으로 개선함[cite: 328].

---

## 5. 이진 영상 및 모폴로지 (4주차)

### 이진 영상 (Binary Image)
* [cite_start]픽셀 값이 흑(0) 또는 백(1) 두 가지로만 구성된 영상[cite: 282].
* [cite_start]주로 명암 영상에 **임계값 처리(Thresholding)** 를 적용하여 생성함[cite: 283]:
    [cite_start]$b(j,i) = \begin{cases} 1 & \text{if } f(j,i) \ge T \\ 0 & \text{if } f(j,i) < T \end{cases}$ [cite: 283]
* [cite_start]임계값 $T$는 수동으로 설정하거나, 히스토그램 분석을 통해 자동으로 결정 가능[cite: 283].
* [cite_start]**오츄 알고리즘 (Otsu's Algorithm):** 클래스 내 분산(intra-class variance)을 최소화하거나 클래스 간 분산(inter-class variance)을 최대화하는 최적의 임계값을 자동으로 찾아주는 알고리즘[cite: 283].

### 연결성 (Connectivity)
* [cite_start]픽셀들이 서로 연결되어 있는지를 판단하는 기준[cite: 287].
    * [cite_start]**4-연결성:** 상하좌우 픽셀만 이웃으로 간주[cite: 287].
    * [cite_start]**8-연결성:** 상하좌우 및 대각선 픽셀까지 이웃으로 간주[cite: 287].

### 연결 요소 (Connected Components)
* [cite_start]이진 영상에서 값이 1인 픽셀들이 연결성(4 또는 8)에 따라 서로 연결된 집합[cite: 288]. [cite_start]하나의 물체나 덩어리를 나타냄[cite: 288].

### 모폴로지 (Morphology)
* [cite_start]형태(shape)를 기반으로 이미지를 처리하는 연산 기법 모음[cite: 289]. 주로 이진 영상에 적용됨.
* [cite_start]**구조 요소 (Structuring Element, SE):** 연산의 기준이 되는 작은 마스크(커널)[cite: 290].
* **기본 연산:**
    * [cite_start]**침식 (Erosion):** 객체 영역을 축소시킴[cite: 292]. [cite_start]작은 돌출부 제거 효과[cite: 292]. SE가 객체 영역 내부에 완전히 포함될 때 해당 픽셀을 1로 설정.
    * [cite_start]**팽창 (Dilation):** 객체 영역을 확장시킴[cite: 291]. [cite_start]작은 구멍을 메우거나 끊어진 부분을 연결하는 효과[cite: 291]. SE와 객체 영역이 한 픽셀이라도 겹치면 해당 픽셀을 1로 설정.
* **복합 연산:**
    * [cite_start]**열림 (Opening):** 침식 후 팽창[cite: 293, 311]. 작은 객체(노이즈) 제거, 가는 연결 끊기 효과.
    * [cite_start]**닫힘 (Closing):** 팽창 후 침식[cite: 293, 311]. 작은 구멍 메우기, 끊어진 객체 연결 효과.

---

## 6. 영역 연산 (Area Operations) (5주차 - part1)

### 컨볼루션 (Convolution)
* [cite_start]영역 연산의 기본적인 방법[cite: 346].
* [cite_start]**필터(커널, 마스크)** 를 이미지 위에서 이동시키면서, 필터 값과 겹치는 이미지 픽셀 값들을 곱한 후 모두 더하여 결과 이미지의 픽셀 값을 결정함[cite: 394, 395].
* [cite_start]**패딩 (Padding):** 컨볼루션 시 이미지 가장자리 처리를 위해 사용[cite: 374].
    * [cite_start]**Zero padding:** 가장자리를 0으로 채움[cite: 375, 415, 417].
    * [cite_start]**Copy padding (Replication):** 가장자리 픽셀 값으로 채움[cite: 376, 418, 420].

### 다양한 필터
* [cite_start]**샤프닝 필터 (Sharpening Filter):** 이미지의 경계를 강조하여 선명하게 만듦[cite: 424]. 중심 값은 크고 주변 값은 음수인 필터 사용 (예: 라플라시안 필터).
* [cite_start]**스무딩 필터 (Smoothing Filter):** 이미지의 노이즈를 줄이고 부드럽게 만듦 [cite: 430] (블러링 효과) [cite_start][cite: 435].
    * [cite_start]**평균 필터 (Averaging Filter):** 주변 픽셀 값들의 평균으로 대체[cite: 431]. [cite_start]모든 이웃 픽셀이 동일한 영향력을 가짐[cite: 432]. [cite_start]필터 크기가 클수록 더 흐려짐[cite: 434].
    * [cite_start]**가우시안 필터 (Gaussian Filter):** 가우시안 함수 형태의 가중치를 사용하여 평균을 계산[cite: 437, 439]. [cite_start]중심 픽셀에 가까울수록 높은 가중치를 부여함[cite: 432].
* [cite_start]**엠보싱 필터 (Embossing Filter):** 이미지를 양각 또는 음각 효과처럼 보이게 만듦[cite: 440].

### 컨볼루션 결과 처리
* [cite_start]컨볼루션 결과 픽셀 값이 표현 범위를 벗어날 수 있음 (예: 0 미만 또는 255 초과)[cite: 442].
* [cite_start]이 경우, 값을 범위 내로 제한(clipping)하거나 비율 조절(rescaling)하여 처리해야 데이터 손실을 관리할 수 있음[cite: 443].

---

## 7. 기하 연산 (Geometric Operations) (5주차 - part1)

### 동차 좌표계 (Homogeneous Coordinates)
* [cite_start]2차원 좌표 $(x, y)$에 1을 추가하여 3차원 벡터 $(x, y, 1)$로 표현하는 방식[cite: 446].
* [cite_start]$(x, y, 1)$과 $(wx, wy, w)$는 같은 2D 점을 나타냄 (단, $w \neq 0$)[cite: 446].
* [cite_start]이동, 회전, 크기 변환 등 다양한 기하 변환을 **단일 행렬 곱셈**으로 통합하여 표현할 수 있게 함[cite: 447].

### 동차 행렬 (Homogeneous Matrix)
* [cite_start]동차 좌표를 변환하는 데 사용되는 3x3 행렬[cite: 447].

| 기하 변환   | 동차 행렬                                                                                                 | 설명                                                                   |
| :---------- | :-------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------- |
| **이동** | [cite_start]$T(t_x, t_y) = \begin{pmatrix} 1 & 0 & t_x \\ 0 & 1 & t_y \\ 0 & 0 & 1 \end{pmatrix}$ [cite: 449]           | [cite_start]$x$ 방향으로 $t_x$, $y$ 방향으로 $t_y$ 만큼 이동 [cite: 449]                 |
| **회전** | [cite_start]$R(\theta) = \begin{pmatrix} \cos\theta & \sin\theta & 0 \\ -\sin\theta & \cos\theta & 0 \\ 0 & 0 & 1 \end{pmatrix}$ [cite: 449] | [cite_start]원점을 중심으로 **반시계 방향**으로 $\theta$ 만큼 회전 [cite: 449]           |
| **크기 조절** | [cite_start]$S(s_x, s_y) = \begin{pmatrix} s_x & 0 & 0 \\ 0 & s_y & 0 \\ 0 & 0 & 1 \end{pmatrix}$ [cite: 449]         | [cite_start]$x$ 방향으로 $s_x$ 배, $y$ 방향으로 $s_y$ 배 조절 (1보다 크면 확대) [cite: 449] |

* [cite_start]**어파인 변환 (Affine Transformation):** 이동, 회전, 크기 변환, 전단(shear) 등을 포함하며, 직선의 평행성은 유지되는 변환[cite: 447, 448].

### 보간법 (Interpolation)
* [cite_start]기하 변환(특히 크기 변경, 회전) 시 결과 이미지의 픽셀 값을 결정하기 위해, 원본 이미지에서 해당 위치 주변의 픽셀 값들을 참조하여 새로운 픽셀 값을 추정하는 방법[cite: 452].
* [cite_start]**최근접 이웃 보간 (Nearest Neighbor):** 가장 가까운 원본 픽셀 값을 그대로 사용[cite: 452]. [cite_start]빠르지만 계단 현상(aliasing) 발생 가능[cite: 452].
* [cite_start]**양선형 보간 (Bilinear):** 주변 4개 픽셀 값을 거리에 따라 선형 가중 평균하여 계산[cite: 452]. [cite_start]부드러운 결과를 얻지만 계산량이 증가[cite: 453].
* [cite_start]**바이큐빅 보간 (Bicubic) / 스플라인 보간:** 주변 16개 또는 더 많은 픽셀을 사용하여 고차 다항식으로 추정[cite: 453]. [cite_start]화질이 가장 좋지만 계산 복잡도가 높음[cite: 453].

---

## 8. 에지 및 영역 (5주차 - part2)

### 에지 검출 (Edge Detection)
* [cite_start]**에지 (Edge):** 이미지에서 밝기가 급격하게 변하는 부분[cite: 486]. 객체의 경계선에 해당되는 경우가 많음.
* [cite_start]**미분 활용:** 밝기 변화율을 측정하기 위해 미분 개념을 사용함[cite: 503, 518]. [cite_start]디지털 영상에서는 이웃 픽셀 간의 차이를 이용[cite: 520, 521].
    * [cite_start]**1차 미분:** 밝기 변화율[cite: 554]. [cite_start]필터 `[-1, 1]` 또는 `[-1, 0, 1]` 컨볼루션으로 근사[cite: 523, 543]. [cite_start]에지의 위치를 정확히 찾기 어려움[cite: 578]. [cite_start]램프 에지에서 봉우리 형태로 나타남[cite: 604].
    * [cite_start]**2차 미분:** 밝기 변화율의 변화율 (가속도)[cite: 579]. [cite_start]필터 `[1, -2, 1]` 컨볼루션으로 근사[cite: 601]. [cite_start]**영교차(Zero-crossing)** 지점이 에지의 중심으로 간주될 수 있음[cite: 604].

### 1차 미분 기반 에지 연산자
* [cite_start]**프레윗 (Prewitt) / 소벨 (Sobel) 연산자:** x 방향과 y 방향 각각의 미분 필터(3x3 크기)를 사용하여 그래디언트를 계산[cite: 605, 606]. [cite_start]소벨은 중심부에 더 큰 가중치를 둠[cite: 605].
    * [cite_start]$f'_x(y,x) \approx f(y, x+1) - f(y, x-1)$ [cite: 605]
    * [cite_start]$f'_y(y,x) \approx f(y+1, x) - f(y-1, x)$ [cite: 605]
* [cite_start]**에지 강도 (Edge Strength):** 그래디언트 벡터의 크기[cite: 607]. [cite_start]$s(y,x) = \sqrt{f'_x(y,x)^2 + f'_y(y,x)^2}$[cite: 607]. [cite_start]에지일 가능성을 나타냄[cite: 607].
* [cite_start]**그래디언트 방향 (Gradient Direction):** 밝기가 가장 빠르게 증가하는 방향[cite: 607]. [cite_start]$d(y,x) = \arctan \left( \frac{f'_y(y,x)}{f'_x(y,x)} \right)$[cite: 607].
* [cite_start]**에지 방향 (Edge Direction):** 그래디언트 방향에 수직인 방향 (그래디언트 방향 + 90도)[cite: 607].

### 캐니 에지 검출 (Canny Edge Detector)
* 성능 좋은 에지 검출 알고리즘. [cite_start]낮은 에러율 [cite: 623][cite_start], 정확한 에지 위치 [cite: 624][cite_start], 단일 에지 응답 [cite: 625]을 목표로 함.
* **단계:**
    1.  [cite_start]**노이즈 제거:** 가우시안 필터 적용[cite: 628].
    2.  [cite_start]**그래디언트 계산:** 소벨 필터 등으로 에지 강도와 방향 계산[cite: 630].
    3.  [cite_start]**비최대 억제 (Non-maximum Suppression):** 에지 방향을 따라가며, 국소적으로 최대 강도를 갖는 픽셀만 남기고 나머지는 제거하여 에지를 얇게 만듦[cite: 632, 633, 634].
    4.  [cite_start]**이중 임계값 (Double Thresholding):** 두 개의 임계값(T_high, T_low)을 사용하여 픽셀을 강한 에지(strong), 약한 에지(weak), 에지 아님(non-edge)으로 분류[cite: 635, 636].
    5.  [cite_start]**에지 연결 (Edge Tracking by Hysteresis):** 강한 에지 픽셀에서 시작하여 연결된 약한 에지 픽셀들을 추적하여 최종 에지로 포함시킴[cite: 639]. [cite_start]강한 에지와 연결되지 않은 약한 에지는 제거[cite: 639].

### 직선 검출: 허프 변환 (Hough Transform)
* [cite_start]이미지에서 직선, 원 등의 특정 기하학적 형태를 검출하는 알고리즘[cite: 648].
* [cite_start]**원리:** 이미지 공간(x, y)의 점들을 파라미터 공간(예: 직선의 경우 $(\rho, \theta)$)으로 변환하여 투표(voting) 방식으로 형태를 찾음[cite: 648]. [cite_start]에지 맵의 각 에지 픽셀이 파라미터 공간에서 자신이 속할 수 있는 모든 직선(또는 원)에 투표함[cite: 648]. 가장 많이 투표받은 파라미터가 검출된 형태로 간주됨.
* [cite_start]**장점:** 노이즈나 끊어진 에지에 비교적 강건함[cite: 648].
* [cite_start]**단점:** 파라미터 공간의 크기에 따라 계산량과 메모리 사용량이 증가함[cite: 652]. [cite_start]이상치(outlier)에 민감할 수 있음[cite: 652]. [cite_start]끊어진 에지 검출 어려움[cite: 653].

### RANSAC (RANdom SAmple Consensus)
* [cite_start]이상치(outlier)가 많은 데이터에서 원하는 모델(예: 직선, 평면)의 파라미터를 추정하는 강건한(robust) 알고리즘[cite: 654].
* **원리:**
    1.  [cite_start]데이터에서 모델 추정에 필요한 최소 개수의 샘플을 무작위로 선택[cite: 654].
    2.  [cite_start]선택된 샘플들로 모델 파라미터를 계산[cite: 654].
    3.  [cite_start]전체 데이터 중 계산된 모델과 잘 맞는 데이터(inlier)의 수를 셈[cite: 654].
    4.  [cite_start]위 과정을 여러 번 반복하여 가장 많은 inlier를 확보한 모델을 최종 결과로 선택[cite: 654].

### 영역 분할 (Region Segmentation)
* [cite_start]이미지를 의미 있거나 유사한 특성을 가진 여러 영역(region)으로 나누는 작업[cite: 656].
* [cite_start]**워터셰드 알고리즘 (Watershed Algorithm):** 이미지 밝기(또는 그래디언트 크기)를 지형의 높이로 간주하고 [cite: 657][cite_start], 낮은 지점(골짜기)부터 물을 채워나가면서 물이 만나는 지점을 경계로 영역을 분할하는 방식[cite: 657].
* [cite_start]**슈퍼픽셀 (Superpixel):** 색상, 밝기 등 유사한 특성을 가진 인접 픽셀들을 그룹화한 작은 영역[cite: 658]. [cite_start]픽셀 단위 처리를 슈퍼픽셀 단위 처리로 대체하여 연산 효율을 높이고 의미론적 처리를 용이하게 함[cite: 659].
    * [cite_start]**SLIC (Simple Linear Iterative Clustering):** 슈퍼픽셀 생성 알고리즘 중 하나 [cite: 661][cite_start]. k-means 클러스터링과 유사한 방식으로 색상과 공간적 근접성을 함께 고려하여 반복적으로 픽셀들을 군집화함[cite: 661].
* [cite_start]**정규화 절단 (Normalized Cut):** 이미지를 그래프로 표현하고, 그래프 분할(graph partitioning) 이론을 적용하여 영역을 나누는 알고리즘[cite: 668]. [cite_start]영역 내부의 유사도는 높게, 영역 간의 유사도는 낮게 분할하는 것을 목표로 함[cite: 668]. [cite_start]이미지 전체 정보를 고려함[cite: 668].

### 대화식 분할 (Interactive Segmentation)
* [cite_start]사용자가 초기 정보(예: 객체/배경 영역 일부 지정)를 제공하여 분할 정확도를 높이는 방식[cite: 672].
* [cite_start]**Active Contour (Snake):** 사용자가 대략적인 윤곽선을 그리면, 이 곡선이 이미지의 에지 등 특징을 따라 이동(수축/팽창)하여 객체의 정확한 경계선을 찾아가는 방식[cite: 673].
* [cite_start]**GrabCut:** 사용자가 객체를 포함하는 사각형을 그리거나, 객체와 배경 영역을 붓으로 일부 지정하면 [cite: 675][cite_start], 가우시안 혼합 모델(GMM)과 그래프 컷(Graph Cut) 알고리즘을 사용하여 전경(객체)과 배경을 분리하는 방식[cite: 674].

### 영역 특징 (Region Features)
* [cite_start]분할된 영역의 특성을 나타내는 값들을 계산함[cite: 681, 682].
* **기본 특징:**
    * [cite_start]**면적 (Area):** 영역을 구성하는 픽셀 수[cite: 684].
    * [cite_start]**둘레 (Perimeter):** 영역 경계선의 길이[cite: 684].
    * [cite_start]**중심 (Centroid):** 영역의 무게 중심 좌표 $(c_x, c_y)$[cite: 684]. [cite_start]모멘트(moments)를 이용하여 계산 가능[cite: 684].
    * [cite_start]**원형성 (Roundness / Circularity):** 영역이 원에 얼마나 가까운지를 나타내는 척도[cite: 684]. [cite_start]예를 들어, $\frac{4\pi \times \text{Area}}{\text{Perimeter}^2}$[cite: 684]. 값이 1에 가까울수록 원형임.
* **형태 관련 특징:**
    * [cite_start]**볼록 껍질 (Convex Hull):** 영역을 포함하는 가장 작은 볼록 다각형[cite: 684].
    * **경계 상자 (Bounding Box):** 영역을 포함하는 가장 작은 축 평행 직사각형.
    * **방향 (Orientation):** 영역의 주축 방향.
    * **편심률 (Eccentricity):** 영역이 얼마나 길쭉한지를 나타냄.

---

## 9. 지역 특징 (Local Features) (6, 7주차)

### 대응점 문제 (Correspondence Problem)
* [cite_start]서로 다른 영상(다른 시점, 시간 등)에서 동일한 물체의 동일한 지점을 찾는 문제[cite: 21].
* [cite_start]파노라마 영상 제작, 물체 인식/추적, 3D 복원 등 컴퓨터 비전의 핵심 과제[cite: 22, 23].
* [cite_start]조명 변화, 시점 변화, 크기 변화, 회전, 가려짐(Occlusion) 등으로 인해 어려움[cite: 29].
* [cite_start]**해결책:** **지역 특징(Local Feature)** 사용[cite: 30]. [cite_start](예: SIFT, SURF, ORB 등 [cite: 31])

### 지역 특징 (Local Feature)
* [cite_start]이미지의 특정 부분(작은 패치)에서 추출되는 고유한 정보[cite: 41]. [cite_start]다른 영상에서도 안정적으로 같은 지점을 찾을 수 있도록 함[cite: 41].
* **유용한 지역 특징의 조건:**
    * [cite_start]**반복성 (Repeatability):** 다른 영상에서도 동일한 위치에서 특징점이 검출되어야 함[cite: 44, 46].
    * [cite_start]**불변성 (Invariance):** 이동, 회전, 크기(스케일), 조명 변화에도 특징 기술자(descriptor) 값이 크게 변하지 않아야 함[cite: 47, 48].
    * [cite_start]**분별력 (Discriminative power):** 다른 위치의 특징과는 구별되어야 함[cite: 49, 50].
    * [cite_start]**지역성 (Locality):** 작은 영역 기반으로 추출되어 가려짐(occlusion)에 강해야 함[cite: 51, 53].
    * [cite_start]**적당한 양:** 너무 적으면 매칭이 어렵고, 너무 많으면 계산량이 증가함[cite: 54, 55].
    * [cite_start]**계산 효율:** 실시간 처리가 가능해야 함[cite: 56, 57].

### 특징점 검출 알고리즘
* [cite_start]**모라벡 (Moravec) 알고리즘:** 주변 모든 방향으로 이동했을 때 픽셀 값 변화가 큰 지점을 코너(특징점)로 간주[cite: 63]. [cite_start]단순하지만 회전, 조명 변화에 취약[cite: 68].
* [cite_start]**해리스 코너 검출 (Harris Corner Detection):** 모라벡 알고리즘 개선[cite: 68]. [cite_start]각 픽셀마다 **코너 응답 함수(R)** 값을 계산하여 코너 가능성을 판단[cite: 70].
    * [cite_start]$R$ 값이 크면 코너 [cite: 71][cite_start], 0에 가까우면 평탄 [cite: 71][cite_start], 음수면 에지 영역일 가능성이 높음[cite: 71].
    * [cite_start]이동과 회전에는 불변하지만 [cite: 72][cite_start], **스케일 변화에는 불변하지 않음**[cite: 72].

### 불변성 (Invariance)
* [cite_start]**이동 불변 (Translation Invariance):** 객체 위치가 변해도 같은 특징점 검출[cite: 67].
* [cite_start]**회전 불변 (Rotation Invariance):** 객체가 회전해도 같은 특징점 검출[cite: 67].
* [cite_start]**크기/스케일 불변 (Scale Invariance):** 객체 크기가 변해도 같은 특징점 검출[cite: 67].

### 스케일 불변성 확보: 스케일 공간 (Scale Space)
* [cite_start]동일한 장면을 다양한 크기(스케일)에서 본 것처럼 여러 버전의 이미지를 생성하는 기법[cite: 79].
* [cite_start]**가우시안 스무딩 방법:** 원본 이미지 크기는 유지한 채, 다양한 표준편차($\sigma$) 값을 가진 가우시안 필터를 적용하여 여러 단계의 흐릿한(blurred) 이미지를 생성[cite: 82]. [cite_start]$\sigma$가 클수록 더 멀리서 본 것처럼 흐려짐[cite: 82].
* [cite_start]**피라미드 방법:** 이미지 크기를 점진적으로 줄여나가면서(예: 1/2, 1/4, 1/8) 여러 해상도의 이미지를 생성[cite: 85]. [cite_start]각 단계를 스케일 레벨로 간주[cite: 85]. [cite_start]계산이 빠르지만 스케일 변화가 이산적임[cite: 85].

### SIFT (Scale-Invariant Feature Transform)
* [cite_start]크기, 회전, 조명 변화에 강인한 지역 특징점을 검출하고 기술(describe)하는 대표적인 알고리즘[cite: 89].
* **주요 단계:**

    | 단계                                                              | 설명                                                                                                                                                                                                                           | 결과물                                                    |
    | :---------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------- |
    | 1. **스케일 공간 생성** | [cite_start]여러 옥타브(Octave, 해상도 단계)와 각 옥타브 내 여러 인터벌(Interval, $\sigma$ 단계)에 대해 가우시안 블러 이미지를 생성하여 **가우시안 피라미드** 구성[cite: 91].                                                                   | [cite_start]여러 장의 가우시안 블러 영상 [cite: 92]                   |
    | 2. **DoG 피라미드 생성** | [cite_start]가우시안 피라미드에서 인접한 스케일(인터벌)의 이미지 간 차이(Difference of Gaussian)를 계산[cite: 94]. 이는 라플라시안(LoG)의 근사이며, 블롭(blob) 특징을 효과적으로 검출.                                                               | [cite_start]여러 장의 DoG 영상 [cite: 94]                             |
    | 3. **키포인트(극값) 검출** | [cite_start]DoG 피라미드에서 각 픽셀을 공간적(같은 스케일의 8개 이웃) 및 스케일적(인접 스케일의 9x2=18개 이웃)으로 총 26개 이웃과 비교하여 극대/극소점(Extrema)을 찾음[cite: 95, 96]. 이들이 키포인트 후보가 됨.                                                  | [cite_start]키포인트 후보 위치 리스트 [cite: 96]                      |
    | 4. **키포인트 정제** | [cite_start]부정확한 위치 보정 (서브픽셀 정밀도) [cite: 97][cite_start], 대비(contrast)가 낮은 점 제거 [cite: 98][cite_start], 에지 응답(한 방향으로만 변화가 큰 점) 제거[cite: 98].                                                                                  | [cite_start]정제된 키포인트 위치 [cite: 98]                           |
    | 5. **방향 할당** | [cite_start]각 키포인트 주변 영역의 그래디언트 방향과 크기를 계산하여 방향 히스토그램 생성[cite: 99]. [cite_start]최빈 방향을 키포인트의 **대표 방향**으로 할당하여 회전 불변성 확보[cite: 99]. [cite_start]필요시 보조 방향 할당[cite: 100].                                  | [cite_start]대표 방향이 할당된 최종 키포인트 [cite: 100]              |
    | 6. **기술자(Descriptor) 생성** | [cite_start]키포인트 주변 16x16 영역을 대표 방향 기준으로 회전시킨 후 [cite: 101][cite_start], 4x4개의 4x4 소영역으로 나눔[cite: 104]. [cite_start]각 소영역에서 8방향 그래디언트 히스토그램을 계산하여 총 4x4x8 = **128차원 벡터** 생성[cite: 104]. [cite_start]가우시안 가중 적용 및 정규화 수행[cite: 101, 102]. | [cite_start]각 키포인트당 128차원 실수 벡터 (SIFT 기술자) [cite: 102] |
    | 7. **매칭 (Matching)** | (다음 섹션에서 설명) [cite_start][cite: 105]                                                                                                                                                                                                            | [cite_start]매칭 쌍 목록 [cite: 105]                                  |

* [cite_start]**SIFT 이후 알고리즘:** SURF, FAST, ORB 등[cite: 108]. SIFT의 성능을 유지하거나 개선하면서 계산 속도를 높이는 데 초점을 둠.

---

## 10. 특징점 매칭 (Feature Matching) (6, 7주차)

* [cite_start]**목표:** 두 이미지에서 추출된 지역 특징 기술자(descriptor)들을 비교하여 서로 대응되는 쌍(같은 지점을 나타내는 쌍)을 찾는 과정[cite: 105].
* [cite_start]**어려움:** 특징점 개수가 많고(수백~수천 개) [cite: 111][cite_start], 기술자 벡터에 노이즈(조명, 가려짐 등)가 있으며 [cite: 111][cite_start], 실제 대응점이 없는 경우(배경, 시점 차이)도 많음[cite: 111].

### 매칭 전략
* [cite_start]**최근접 이웃 (Nearest Neighbor, NN) 매칭:** 한 이미지의 특징점 $a_i$에 대해 다른 이미지의 모든 특징점 $b_j$들과의 거리(주로 유클리드 거리)를 계산하여, 거리가 가장 가까운 $b_j$(NN1)를 매칭 쌍으로 선택[cite: 112].
* [cite_start]**최근접 이웃 거리 비율 (Nearest Neighbor Distance Ratio, NNDR) 매칭:** 단순 NN 매칭은 잘못된 매칭(false match)이 많을 수 있음[cite: 113]. [cite_start]이를 개선하기 위해 $a_i$에 대해 가장 가까운 이웃(NN1, 거리 $d_1$)과 두 번째로 가까운 이웃(NN2, 거리 $d_2$)을 찾음[cite: 112]. [cite_start]그 거리 비율 $d_1 / d_2$가 특정 임계값 $T$ (보통 0.75 사용 [cite: 113][cite_start])보다 작을 때만 신뢰할 수 있는 매칭으로 간주[cite: 113, 114]. [cite_start]즉, 가장 가까운 이웃이 두 번째 가까운 이웃보다 **확실히** 더 가까워야 함[cite: 114].

### 매칭 성능 측정
* [cite_start]**혼동 행렬 (Confusion Matrix):** 매칭 결과를 실제 정답(Ground Truth)과 비교하여 분류[cite: 116].

    | 예측 \ 정답 | 긍정 (실제 매칭) | 부정 (실제 매칭 아님) |
    | :---------- | :--------------- | :-------------------- |
    | **긍정** | [cite_start]**TP** (참 긍정) [cite: 116] | [cite_start]**FP** (거짓 긍정) [cite: 116]    |
    | **부정** | [cite_start]**FN** (거짓 부정) [cite: 116] | [cite_start]**TN** (참 부정) [cite: 116]      |

* **성능 지표:**
    * [cite_start]**정밀도 (Precision):** $\frac{TP}{TP + FP}$ [cite: 116] (매칭 성공으로 예측한 것 중 실제 매칭 성공 비율)
    * [cite_start]**재현율 (Recall) / 참 긍정률 (TPR):** $\frac{TP}{TP + FN}$ [cite: 116, 117] (실제 매칭 성공 중 예측 성공 비율)
    * [cite_start]**거짓 긍정률 (FPR):** $\frac{FP}{TN + FP}$ [cite: 117] (실제 매칭 아님 중 예측 실패 비율)
    * [cite_start]**F1 점수:** $\frac{2 \times \text{정밀도} \times \text{재현율}}{\text{정밀도} + \text{재현율}}$ [cite: 116] (정밀도와 재현율의 조화 평균)
    * [cite_start]**정확도 (Accuracy):** $\frac{TP + TN}{TP + TN + FP + FN}$ [cite: 116] (전체 중 올바르게 예측한 비율)
* [cite_start]**ROC 곡선 (Receiver Operating Characteristic Curve):** NNDR 매칭의 임계값 T를 변경해가며 FPR(x축)에 따른 TPR(y축)의 변화를 그린 그래프[cite: 119]. [cite_start]곡선이 왼쪽 위로 갈수록 성능이 좋음[cite: 117].
* [cite_start]**AUC (Area Under the Curve):** ROC 곡선 아래 면적[cite: 119]. [cite_start]1에 가까울수록 좋은 알고리즘[cite: 120].

### FLANN (Fast Library for Approximate Nearest Neighbors)
* [cite_start]대규모 데이터셋에서 최근접 이웃을 빠르게 (근사적으로) 검색하기 위한 라이브러리[cite: 121]. 특징점 매칭 속도를 향상시키는 데 사용됨.

---

## 11. 호모그래피 추정 (Homography Estimation) (6, 7주차)

### 호모그래피 (Homography)
* [cite_start]하나의 평면(plane)에서 다른 평면으로의 투영 변환(projective transformation)을 나타내는 3x3 행렬 $H$[cite: 126].
* 두 이미지 간의 관계가 평면 투영으로 근사될 수 있을 때 (예: 카메라 회전만 있거나, 멀리 있는 평면 장면을 찍은 경우) 사용됨.
* 점 $(x, y)$가 다른 이미지의 점 $(x', y')$으로 변환되는 관계는 동차 좌표계를 사용하여 $\begin{pmatrix} x' \\ y' \\ 1 \end{pmatrix} \sim H \begin{pmatrix} x \\ y \\ 1 \end{pmatrix}$ 로 표현됨 ($\sim$는 스케일 차이를 무시한다는 의미).

### 호모그래피 추정 (Homography Estimation)
* [cite_start]두 이미지 사이에서 매칭된 대응점 쌍들(최소 4쌍 필요)을 이용하여 호모그래피 행렬 $H$를 계산하는 과정[cite: 126].
* [cite_start]**필요 이유:** 단순히 대응점만으로는 이미지 전체의 뒤틀림이나 정렬을 설명하기 어려움[cite: 127]. [cite_start]$H$ 행렬은 이미지 전체를 변환하여 다른 이미지와 정렬하는 데 사용됨[cite: 127].
* [cite_start]**알고리즘:** 주로 DLT(Direct Linear Transform) 알고리즘과 RANSAC을 함께 사용하여 잘못된 매칭(이상치)에 강인하게 $H$를 추정함[cite: 129].
* [cite_start]**응용:** 파노라마 이미지 스티칭(stitching) [cite: 127][cite_start], 이미지 정렬, 증강현실(AR) 객체 배치[cite: 128], 카메라 자세 추정 등.
* [cite_start]**OpenCV 함수:** `cv.findHomography(points1, points2, cv.RANSAC)`[cite: 130].
