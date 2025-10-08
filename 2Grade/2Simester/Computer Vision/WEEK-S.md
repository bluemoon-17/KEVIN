# ==============================================================================
# 2주차 & 3주차: 컴퓨터 비전 기초 및 디지털 영상 처리
# ==============================================================================

# 1. 디지털 영상 획득 과정 (Sampling & Quantization)
def digitize_image(analog_image):
    """
    연속적인 아날로그 영상을 디지털 영상으로 변환하는 과정
    """
    # 1. 샘플링 (Sampling): 공간 해상도 결정 (픽셀 수)
    spatial_resolution = sample(analog_image) 
    
    # 2. 양자화 (Quantization): 명암 레벨 해상도 결정 (밝기 단계)
    grayscale_levels = quantize(spatial_resolution)
    
    # OpenCV 특징: 영상은 numpy.ndarray 객체로 표현됨
    # -> NumPy의 min, max, shape, mean 등의 함수를 활용 가능
    print(f"OpenCV Image Type: {type(grayscale_levels)}")
    return grayscale_levels

# 2. OpenCV 기본: 컬러 공간 변환
import cv2 as cv
# img = cv.imread('image.jpg')
# gray_img = cv.cvtColor(img, cv.COLOR_BGR2GRAY) # 필수 암기: BGR -> Grayscale 변환

# 3. 인간 시각의 한계: 착시, 정밀 측정 오차

# 4. 영상 처리 5대 분야: 개선, 복원, 변환, 분석, 압축

# ==============================================================================
# 4주차 & 5주차 Part 1: 영상 처리의 3대 연산 및 모폴로지
# ==============================================================================

# 1. 영상 처리의 3대 연산 구분
OPERATION_TYPES = {
    "점 연산 (Point Op)": "원본의 같은 위치 픽셀 '하나'만 참조 (예: 밝기 조정)",
    "영역 연산 (Area Op)": "주변 '이웃 화소'들을 함께 고려 (예: 블러, 컨볼루션)",
    "기하 연산 (Geometric Op)": "픽셀 '위치'를 변환 (예: 회전, 이동, 크기 조절)"
}

# 2. 영역 연산의 핵심: 컨볼루션
def convolution(image_block, kernel):
    """
    컨볼루션 연산 원리: 필터(커널)와 이미지 블록을 곱하고 더함
    시험 대비: 필터 값과 픽셀 값을 곱한 후 모두 더하는 계산 과정을 숙지해야 함.
    """
    # result_pixel = sum(image_block * kernel)
    return 'new_pixel_value'

# 3. 기하 연산의 핵심: 보간 (Interpolation)
INTERPOLATION_METHODS = {
    "최근접 이웃 보간 (Nearest Neighbor)": "가장 가까운 픽셀 값 복사 (속도 빠름, 계단 현상)",
    "양선형 보간 (Bilinear Interpolation)": "주변 4개 픽셀의 **가중 평균** 사용 (화질 부드러움)",
    "동차 행렬": "이동, 회전, 크기 조절 등을 하나의 행렬 곱셈으로 처리하기 위해 사용"
}

# 4. 이진 영상 모폴로지 연산
def morphology_operation(binary_image, kernel, op_type):
    """
    형태(Morphology) 기반 연산
    """
    if op_type == "Dilation":
        return "팽창 (객체 영역 확장)"
    elif op_type == "Erosion":
        return "침식 (객체 영역 축소)"
    elif op_type == "Opening":
        return "침식 -> 팽창 (작은 돌출부 제거)"
    elif op_type == "Closing":
        return "팽창 -> 침식 (작은 구멍 채우기)"

# ==============================================================================
# 5주차 Part 2: 에지 검출 및 영역 분할 (계산 공식 필수 암기)
# ==============================================================================

# 1. 에지 검출 원리: 영상의 미분 (밝기 변화율)

# 2. 소벨 필터 (Sobel Filter)를 이용한 에지 계산
import numpy as np

def calculate_edge_properties(Gx, Gy):
    """
    Sobel 필터 결과인 Gx, Gy를 이용해 에지 강도와 방향을 계산
    시험 필수 공식!!!
    """
    # 1. 에지 강도 (Gradient Magnitude): 피타고라스 정리 이용
    magnitude = np.sqrt(Gx**2 + Gy**2)
    
    # 2. 그래디언트 방향 (Direction): 아크탄젠트 이용
    direction = np.arctan2(Gy, Gx) # atan2를 사용하여 사분면 고려
    
    return magnitude, direction

# 3. 주요 에지 검출기 및 분할 기법
ADVANCED_METHODS = {
    "Canny Edge Detector": "잡음 제거와 정확도가 높은 **최적의** 에지 검출기",
    "Hough Transform": "**직선**이나 원과 같은 기하학적 형태를 **매개변수 공간**으로 변환하여 검출",
    "Active Contour (Snake)": "초기 곡선을 에너지 최소화를 통해 **객체 경계선에 자동 수축/팽창**",
    "GrabCut": "사용자 지정(붓칠) 기반으로 **객체와 배경을 자동 분리**하는 대화식 분할"
}

# 4. 결론: 시험 대비 핵심 암기 대상
# - 컨볼루션 계산 원리 (곱셈 후 덧셈)
# - 양선형 보간 원리 (가중 평균)
# - 에지 강도/방향 공식 (위 calculate_edge_properties 함수 참고)
