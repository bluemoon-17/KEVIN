# 컴퓨터 비전 강의 자료 (9주차 ~ 14주차) 주요 이론 및 개념 정리 (표 형식)

| 주차/영역 | 주요 개념 | 정의 및 설명 |
| :--- | :--- | :--- |
| **9주차 (PyQt 기초)** | **에이전트 (Agent)** | 환경으로부터 정보를 받아 인식(perception)하고, 그 정보를 바탕으로 행동(action)하며 상호작용하는 지능적 시스템. |
| | **비전 에이전트** | 영상 센싱을 통해 환경을 인식하고 행동을 수행하며 상호작용하는 에이전트. |
| | **PyQt 라이브러리** | Python에서 GUI(Graphical User Interface) 프로그램을 개발하기 위한 라이브러리. |
| **10주차 (CNN 심화)** | **Focal Loss** | 불균형 데이터(imbalanced data) 문제 해결을 위해 제안된 손실 함수. 쉬운 샘플 영향은 줄이고 어려운 샘플에 가중치를 줌. |
| | **모멘텀 (Momentum)** | 이전 운동량이 현재 가중치 변경에 영향을 미치게 하여 SGD(경사 하강법) 학습을 개선하는 기법. |
| | **백본 모델 (Backbone)** | 영상 인식의 특징 추출을 담당하는 기본 신경망 모델 (VGGNet, GoogLeNet, ResNet 등). |
| | **ResNet** | 지름길 연결(Skip Connection)을 적용하여 깊은 신경망의 학습이 용이하도록 설계된 모델. |
| **11주차 (객체 인식)** | **분류 (Classification)** | 영상에 있는 물체가 무엇인지 하나의 라벨로 예측하는 문제. (출력: 클래스 확률 벡터). |
| | **검출 (Detection)** | 영상에서 객체의 위치(바운딩 박스)와 클래스를 모두 예측하는 문제. |
| | **분할 (Segmentation)** | 영상의 각 화소(Pixel)가 어떤 클래스에 속하는지 예측하는 문제. |
| | **IoU** | **Intersection over Union**. 객체 검출에서 정답 박스와 예측 박스가 겹친 정도를 나타내는 수치. |
| | **U-Net** | 의료 영상 분할 목적으로 개발. 샘플링/업샘플링 및 지름길 연결(Skip Connection)을 특징으로 함. |
| **12주차 (동적 비전)** | **동영상 구조** | 너비 × 높이 × 3의 3차원 텐서가 시간축으로 나열된 **4차원 텐서** 형태. |
| | **Optical Flow** | **광학 흐름**. 연속된 영상에서 화소의 밝기 변화를 기반으로 물체의 움직임(모션 벡터)을 추정하는 기법. 결과물은 벡터 필드. |
| | **추적 (Tracking)** | 비디오에서 같은 물체를 시간에 따라 계속 식별하고 위치를 추적하는 문제. 프레임 간 **연속성 유지**가 핵심. |
| | **KLT Tracker** | 지역 특징점 기반 추적 알고리즘. 밝기가 변하지 않는다고 가정함. |
| | **자세 추정** | 사람의 관절 위치를 랜드마크(keypoint)로 검출하고 연결하여 **스켈레톤**을 구성하는 기술. |
| **13주차 (ViT)** | **트랜스포머 (Transformer)** | 순차적 처리 없이 입력 시퀀스 관계를 효과적으로 학습. 병렬 처리 가능하여 RNN보다 빠름. |
| | **Self-Attention** | 입력 시퀀스 내 모든 요소 간의 관계를 동적으로 학습하는 핵심 메커니즘. |
| | **구조** | 토크나이저, 임베딩 레이어(위치 정보 추가), 인코더 등으로 구성되며 Encoder-Decoder 구조를 사용. |
| **14주차 (3D/생성 모델)**| **Point Cloud (점 구름)** | 3차원 공간 안의 점들을 모아놓은 데이터 구조. 실세계 3D 형태를 수많은 점들로 표현. |
| | **생성 모델** | 데이터의 분포를 배운 후, 그 분포에서 새로운 샘플을 만들어내는 모델 (VAE, GAN, Diffusion Model 등). |
| | **VAE** | **Variational Autoencoder**. 오토인코더의 잠재 공간에서 잠재 벡터 근처에 데이터를 생성하는 방식. |
| | **GAN** | **Generative Adversarial Network**. **생성자**와 **판별자**가 경쟁(Adversarial)하며 정교한 이미지를 만들도록 학습되는 신경망. |


# 주요 함수 이름, 파라미터의 역할

# 컴퓨터 비전 강의 자료 (9주차 ~ 14주차) 주요 함수 및 파라미터 역할 정리

## 1. PyQt 및 OpenCV 기본/GUI 함수 (9주차)

| 함수 이름 | 주요 파라미터 | 역할 |
| :--- | :--- | :--- |
| **`winsound.Beep()`** | `frequency` (주파수 Hz), `duration` (지속 시간 ms) | 지정된 주파수와 지속 시간으로 시스템 소리를 출력합니다. |
| **`cv.VideoCapture()`** | `index` (카메라 ID) 또는 `filename` (동영상 파일 경로) | 비디오 스트림 캡처 객체를 생성합니다. |
| **`cap.read()`** | (없음) | 비디오에서 다음 프레임을 읽어옵니다. `success`, `frame`을 반환합니다. |
| **`cv.resize()`** | `src` (원본 이미지), `dsize` (출력 크기 튜플) | 이미지의 크기를 변경합니다. |
| **`cv.cvtColor()`** | `src` (입력 이미지), `code` (변환 코드) | 이미지의 색 공간을 변환합니다 (예: BGR -> RGB). |
| **`cv.Canny()`** | `image` (입력 이미지), `threshold1` (낮은 임계값), `threshold2` (높은 임계값) | Canny 엣지 검출 알고리즘을 적용합니다. |
| **`cv.Sobel()`** | `src`, `ddepth` (출력 이미지 깊이), `dx`, `dy` (x, y 미분 차수) | Sobel 필터를 적용하여 엣지를 검출합니다. |
| **`cv.bitwise_not()`** | `src` (입력 이미지) | 이미지의 비트 단위 NOT 연산을 수행하여 반전 효과를 만듭니다. |
| **`self.setWindowTitle()`** | `title` (문자열) | PyQt 윈도우의 제목을 설정합니다. |
| **`self.setGeometry()`** | `x`, `y` (위치), `width`, `height` (크기) | 윈도우의 위치와 크기를 설정합니다. |
| **`widget.clicked.connect()`** | `method` (호출할 메서드) | 버튼 클릭 시그널을 지정된 메서드(`slot`)에 연결합니다. |

## 2. CNN, Keras 및 딥러닝 학습 함수 (10주차, 13주차)

| 함수 이름 | 주요 파라미터 | 역할 |
| :--- | :--- | :--- |
| **`ds.mnist.load_data()`** | (없음) | MNIST 데이터셋을 로드합니다. |
| **`x.reshape()`** | `shape` (튜플) | 데이터의 형태를 변경합니다. |
| **`x.astype()`** | `dtype` (데이터 타입) | 데이터 타입을 변경합니다 (예: `np.float32`). |
| **`Sequential()`** | (없음) | 레이어를 순차적으로 쌓는 Keras 모델 객체를 생성합니다. |
| **`cnn.add(Conv2D)`** | `filters`, `kernel_size`, `activation`, `input_shape` | 2차원 컨볼루션 레이어를 추가합니다. |
| **`cnn.add(MaxPooling2D)`** | `pool_size` (풀링 윈도우 크기) | 최대 풀링(Max Pooling) 레이어를 추가합니다. |
| **`cnn.add(Flatten)`** | (없음) | 다차원 입력을 1차원 벡터로 평탄화합니다. |
| **`cnn.add(Dense)`** | `units` (출력 뉴런 수), `activation` (활성화 함수) | 완전 연결(Fully Connected) 레이어를 추가합니다. |
| **`cnn.compile()`** | `loss`, `optimizer`, `metrics` | 모델 학습 방식을 설정합니다. |
| **`cnn.fit()`** | `x`, `y`, `epochs`, `batch_size` | 모델을 훈련시킵니다. |
| **`cnn.evaluate()`** | `x`, `y` | 모델의 성능을 평가합니다. |
| **`cnn.predict()`** | `x` (입력 데이터) | 훈련된 모델로 예측을 수행합니다. |
| **`tf.keras.utils.to_categorical()`** | `y` (정수 레이블), `num_classes` (클래스 개수) | 정수 레이블을 원-핫 인코딩 벡터로 변환합니다. |
| **`tf.keras.preprocessing.image.ImageDataGenerator()`** | `rotation_range` 등 | 데이터 증강을 위한 객체를 생성합니다. |

## 3. 객체 검출 및 분할 함수 (11주차)

| 함수 이름 | 주요 파라미터 | 역할 |
| :--- | :--- | :--- |
| **`YOLO.detectObjectsOf()`** | `input_image` (입력 이미지), `output_image_path` (결과 저장 경로) | YOLO 모델을 사용하여 객체를 검출하고 결과를 저장합니다. |
| **`YOLO.setModelTypeAsYOLOv3()`** | (없음) | 모델 타입을 YOLOv3로 설정합니다. |
| **`YOLO.loadModel()`** | (없음) | 미리 훈련된 YOLO 모델을 메모리에 로드합니다. |
| **`pixellib.semantic_segmentation.Segmentation.segmentImage()`** | `image_path` (입력 이미지), `output_image_name` (출력 이미지 이름), `overlay` | 이미지의 의미론적 분할(Semantic Segmentation)을 수행합니다. |
| **`pixellib.instance_segmentation.MaskRCNN.segmentFrame()`** | `video_path` (입력 동영상), `save_video` (동영상 저장 여부) | 동영상의 인스턴스 분할(Instance Segmentation)을 수행합니다. |

## 4. 동적 비전 및 추적 함수 (12주차)

| 함수 이름 | 주요 파라미터 | 역할 |
| :--- | :--- | :--- |
| **`cv.goodFeaturesToTrack()`** | `image` (입력 이미지), `maxCorners`, `qualityLevel`, `minDistance` | Shi-Tomasi 방법을 사용하여 추적하기 좋은 특징점(코너)을 검출합니다. |
| **`cv.calcOpticalFlowPyrLK()`** | `prevImg`, `nextImg`, `prevPts`, `nextPts` (출력), `winSize` | Lucas-Kanade 광학 흐름(Optical Flow) 추적을 계산합니다. |
| **`cv.calcOpticalFlowFarneback()`** | `prev`, `next`, `flow` (출력), `pyr_scale`, `levels`, `winsize` 등 | Farneback 알고리즘을 사용하여 광학 흐름을 계산합니다. |
| **`cv.magnitude()`** | `x`, `y` (흐름 벡터의 x, y 성분) | 2차원 벡터의 크기(Magnitude)를 계산합니다. |
| **`mp_drawing.draw_landmarks()`** | `image`, `landmark_list`, `connections` | MediaPipe에서 검출된 랜드마크와 연결선을 이미지에 그립니다. |
| **`mp_pose.Pose()`** | `min_detection_confidence` (최소 검출 신뢰도) | MediaPipe의 자세 추정(Pose Estimation) 모델 객체를 생성합니다. |

## 5. 3차원 비전 및 생성 모델 함수 (14주차)

| 함수 이름 | 주요 파라미터 | 역할 |
| :--- | :--- | :--- |
| **`trimesh.load()`** | `file_path` (파일 경로) | 3D 모델 파일을 로드하여 `trimesh` 메쉬 객체를 생성합니다. |
| **`mesh.sample()`** | `count` (샘플링할 점의 개수) | 3D 메쉬 객체에서 지정된 개수만큼 점을 샘플링하여 Point Cloud를 생성합니다. |
| **`PointNet.get_model()`** | `num_classes` (분류할 클래스 개수) | PointNet 모델 구조를 생성하여 반환합니다. |
| **`tf.keras.utils.get_file()`** | `fname` (저장할 파일 이름), `origin` (다운로드 URL), `extract` (압축 해제 여부) | URL에서 파일을 다운로드하고 로컬 경로를 반환합니다. |
| **`tf.data.Dataset.from_tensor_slices()`** | `tensors` (텐서 튜플) | 텐서로부터 `tf.data.Dataset` 객체를 생성합니다. |
| **`tf.data.Dataset.batch()`** | `batch_size` (배치 크기) | 데이터셋을 배치 단위로 묶습니다. |
| **`tf.data.Dataset.shuffle()`** | `buffer_size` (버퍼 크기) | 데이터셋을 섞습니다. |
| **`model.train_step()`** | `data` (입력 데이터) | GAN/VAE와 같은 사용자 정의 모델의 훈련 단계를 정의하고 실행합니다. |


