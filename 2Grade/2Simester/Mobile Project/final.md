# 1. ML Kit을 사용해야 하는 이유

## 배경: 기존 클라우드 기반 AI의 한계
- **지연 시간(Latency)**: 서버 왕복 때문에 실시간 처리 어려움  
- **네트워크 의존성**: 오프라인/불안정 환경에서 기능 작동 불가  
- **개인정보 보호 문제**: 사진·음성 등 민감 데이터가 서버로 전송됨  
- **비용 문제**: 서버 연산 + 대량 데이터 전송 비용 발생  

## ML Kit의 사용 이유
- **개발자 접근성 향상**: TFLite 모델 직접 관리 없이 API로 바로 사용  
- **모바일 최적화**: TensorFlow Lite 기반 고속·경량 모델 실행  
- **보안 강화**: 온디바이스 처리로 민감 데이터 외부 전송 감소  
- **확장성**: 온디바이스 + 클라우드 혼합 구조 지원  

---

# 2. 온디바이스(On-device)의 목적·장점·이용

## 개념
> AI 연산을 서버가 아닌 **기기 내부에서 직접 수행**하는 방식

## 장점
- **개인정보 보호 강화**  
- **오프라인에서도 작동**  
- **실시간 응답(저지연)**  
- **전력·자원 최적화(경량 모델)**  

## 적용 서비스 예
- 실시간 번역  
- 카메라 기반 이미지 처리  
- 맞춤형 사용자 행동 분석  
- 온디바이스 LLM 실행  

---

# 3. 이미지 처리 (ML Kit Vision API)

| API | 주요 기능 | 적용 예 |
|-----|-----------|---------|
| **Image Labeling** | 이미지 내 객체 라벨 자동 분류 | 갤러리 분류, 검색 |
| **Object Detection & Tracking** | 객체 탐지 및 추적 | AR, 보안, 물류 |
| **Text Recognition v2** | 이미지 텍스트 분석 | 문서 스캔, 명함 인식 |
| **Face Detection** | 얼굴·표정·랜드마크 분석 | AR 필터, 얼굴 인식 |
| **Pose Detection** | 인체 관절 33개 추적 | 운동 분석, 모션 캡처 |

---

# 4. Smart Reply 내부 동작 (옵션 선언 → 삽입 → 처리 흐름)

1. **입력 단계**: 대화 로그 수집  
2. **전처리 및 필터링**: 언어 판별, 욕설·폭력 콘텐츠 필터  
3. **텍스트 토큰화**: SentencePiece 기반  
4. **대화 벡터화**: Transformer 인코더로 문맥 임베딩 생성  
5. **답장 후보 선택**:  
   - 대규모 "답장 후보 풀"에서  
   - **유사도 계산 → Top-3 추천**  
6. **최종 검증**: 안전성·품질 점검 후 결과 제공  

> Smart Reply는 "답장을 생성"하지 않고 **답장을 고르는 방식**이다.

---

# 5. 디지털 잉크 (Digital Ink Recognition)

## 개념
터치·펜 입력을 **좌표 기반 스트로크(x, y, t)** 로 분석해  
문자·수식·도형으로 변환하는 기술.

---

## OCR과 Digital Ink 차이

| 항목 | Digital Ink | OCR |
|------|-------------|-----|
| **입력** | 스트로크 좌표(X, Y, 시점 t) | 이미지 픽셀 |
| **영향** | 배경 영향 적음 | 배경·조명 영향 큼 |
| **사용 정보** | 획순·속도 포함 | 최종 이미지 형태 |

---

## Digital Ink Recognition 처리 과정
1. **Stroke Capture**: (x, y, t) 스트로크 저장  
2. **Stroke Grouping**: 떨어졌다 다시 그린 스트로크 구분  
3. **Normalization**: 크기, 속도, 노이즈 보정  
4. **TFLite 모델 추론**  
5. **후처리 및 최종 결과 출력**

---

## 적용 종류
- **텍스트 인식**(손글씨 → 글자)  
- **도형 인식**(원, 삼각형, 화살표 등)  
- **수식 인식**(분수, 루트, 지수 등)

---

# 6. TensorFlow Lite 차이점·구분

## TensorFlow vs TensorFlow Lite

| 항목 | TensorFlow | TensorFlow Lite |
|------|------------|------------------|
| 목적 | 학습 + 서버/PC 추론 | 모바일·엣지 추론 |
| 크기 | 큼 | 경량 |
| 최적화 | 학습 최적화 | 추론 속도·메모리 최적화 |

---

## ML Kit vs TensorFlow Lite

| 항목 | ML Kit | TensorFlow Lite |
|------|--------|------------------|
| 레벨 | 고수준 SDK | 저수준 엔진 |
| 역할 | API·입출력 관리·후처리 | 모델 로드·추론 실행 |
| 난이도 | 매우 쉬움 | 모델 직접 관리 필요 |

---

# 7. ObjectDetectorOptions 옵션 정리

## 주요 옵션

### **setDetectorMode(int mode)**
- `SINGLE_IMAGE_MODE`: 이미지 1장 감지  
- `STREAM_MODE`: 연속 영상 스트림 감지 + 추적  

---

### **setMultipleObjects(boolean enabled)**
- 여러 객체 감지 여부  
- 기본값: `false`

---

### **setClassificationEnabled(boolean enabled)**
- 객체 분류 라벨 활성화  
- 기본값: `true`

---

### **setConfidenceThreshold(float threshold)**
- 최소 신뢰도 점수  
- 기본값: `0.5f`

---

### **setMaxPerObjectLabelCount(int count)**
- 객체당 최대 라벨 반환 개수  
- 기본값: `1`

---

### **setExecutor(Executor executor)**
- 감지 연산을 처리할 스레드 설정  
- 예: `Executors.newSingleThreadExecutor()`

---

## 예시 코드

```java
ObjectDetectorOptions options =
        new ObjectDetectorOptions.Builder()
                .setDetectorMode(ObjectDetectorOptions.STREAM_MODE)
                .setMultipleObjects(true)
                .setClassificationEnabled(true)
                .setConfidenceThreshold(0.5f)
                .setMaxPerObjectLabelCount(1)
                .setExecutor(Executors.newSingleThreadExecutor())
                .build();


