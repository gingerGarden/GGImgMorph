## GGImgMorph
시나리오를 기반으로 한 확률적 이미지 증강 알고리즘의 적용을 고려한 이미지 증강 라이브러리입니다. numpy와 opencv-python을 기반으로 하고 있습니다.
* 현재 개발 진행 중인 코드로, 내부 코드들과 라이브러리 구조는 언제든지 수정될 수 있습니다.

</br>
</br>
</br>

* 해당 라이브러리는 다음과 같은 패키지들로 구성되어 있습니다.

### 1. scenario
* 이미지 증강 알고리즘들을 시나리오 기반으로 적용하는 class의 모음입니다
* 해당 코드에는 다음과 같은 method 들로 구성되어 있습니다
> * RandomScenario: 이 클래스는 입력된 n개의 이미지 증강 method들 중 하나를 무작위로 선택하여 적용하는 것을 목적으로 설계 되었습니다
>> * Callable: 주요 기능으로 p의 확률로 무작위 증강 method를 적용합니다.
> * OrderScenario: 이 클래스는 입력된 n개의 이미지 증강 method들을 입력 순서대로 적용하는 것을 목적으로 설계 되었습니다
>> * Callable: 주요 기능으로 입력된 이미지 증강 method 순서대로 증강을 합니다.

</br>
</br>
</br>

## A. geometric
geometric 기반의 이미지 증강 method들의 모음입니다.
### 1. base
* 가장 기본적인 geometric 기반 이미지 증강 알고리즘 method 들을 포함합니다. 다른 geometric 증강 알고리즘은 해당 모듈의 method들을 기반으로 합니다.
> * crop(): 이미지를 x, y, x_size, y_size를 기준으로 자름
> * padding(): 이미지를 pixel 값으로 padding 
> * padding_border_replicate(): 이미지를 가장자리 픽셀 값으로 채우는 border replicate 방식으로 패딩함
> * resize(): 이미지를 new_x, new_y 크기로 조
> * interpolation_quality(): 이미지 보간 방법 선택

</br>

### 2. distortion
* 이미지를 왜곡하는 계열의 증강 알고리즘 method 들을 포함합니다.
> * Perspective: 이 클래스는 입력된 이미지를 원근 왜곡하는 instance를 생성하는 것을 목적으로 설계 되었습니다.
>> * Callable: 주요 기능으로 p의 확률로 원근 왜곡을 적용합니다.

</br>

### 3. frame
* 이미지에 특정한 형태의 frame을 생성하는 method 들을 포함합니다.
> * Frame: 이 클래스는 p의 확률로 동일 module에 존재하는 frame 클래스 들 중 하나를 무작위로 선택하여 적용하는 것을 목적으로 설계되었습니다.
>> * Callable: 주요 기능으로 p의 확률로 입력된 Frame 중 하나를 무작위로 적용합니다.
> * Circle: 이 클래스는 p의 확률로 이미지에 원으로 된 frame을 생성하는 것을 목적으로 설계되었습니다.
>> * Callable: 주요 기능으로 p의 확률로 설정된 방식되로 원으로 된 frame을 생성합니다.
> * Square: 이 클래스는 p의 확률로 이미지에 네모로 된 frame을 생성하는 것을 목적으로 설계되었습니다.
>> * Callable: 주요 기능으로 p의 확률로 설정된 방식되로 네모로 된 frame을 생성합니다.

</br>

### 4. geometric
* 이미지에 base보다 고도화된 geometic 계열의 증강 알고리즘 method 들을 포함합니다.
> * Rotate: 이 클래스는 p의 확률로 이미지를 무작위 분포의 각도만큼 회전하는 것을 목적으로 설계되었습니다.
>> * Callable: 주요 기능으로 p의 확률로 이미지를 instance에 지정된 무작위 각도만큼 회전합니다.
> * Shear: 이 클래스는 p의 확률로 이미지를 무작위 크기만큼 Shear 변환하는 것을 목적으로 설계되었습니다.
>> * Callable: 주요 기능으로 p의 확롤로 이미지를 Shear 변환합니다.
>> * Shear 변환은 'x축', 'y축', 'xy축', 'Shear 변환으로 인한 이미지 밀림 보정 여부' 4가지 방법의 조합을 포함합니다(무작위 설정 가능).
> * Translate: 이 클래스는 p의 확률로 이미지를 무작위 크기만큼 평행 이동 변환하는 것을 목적으로 설계되었습니다.
>> * Callable: 주요 기능으로 p의 확률로 이미지를 평행 이동 변환 합니다.
>> * 평행 이동 변환 후 빈 영역은 임의의 픽셀 또는 가장자리 픽셀로 채워지는 것을 포함합니다(무작위 설정 가능).
> * Scaling: 이 클래스는 p의 확률로 이미지를 무작위 비율만큼 이미지의 크기를 변환하는 것을 목적으로 설계되었습니다.
>> * Callable: 주요 기능으로 p의 확률로 이미지의 크기를 변환 합니다.
>> * 'x, y축 모두 무작위 비율 조정', 'x, y축 모두 동일 비율 조정', 'x축만 조정', 'y축만 조정' 4가지 방법으로 포함합니다(무작위 설정 가능).
> * Resize: 이 클래스는 이미지의 크기를 특정한 방법으로 조정하는 것을 목적으로 합니다.
>> * Callable: 주요 기능으로 instance에 지정된 방법으로 이미지의 크기를 조정합니다.
>> * '비율 유지(장방 행렬 가능)', '비율 유지 후 padding', '비율 유지 후 border replicate', '비율 무시' 이 4가지 방법을 포함합니다(무작위 설정 가능).
> * Flip: 이 클래스는 p의 확률로 이미지를 무작위 방법으로 이미지를 flip하는 것을 목적으로 설계되었습니다.
>> * Callable: 주요 기능으로 p의 확률로 이미지를 flip 합니다.
>> * '좌우반전', '상하반전', '상하좌우반전' 이 3가지 방법을 포함합니다(무작위 설정 가능).
> * Crop: 이 클래스는 p의 확률로 이미지를 무작위 방법으로 crop하는 것을 목적으로 설계되었습니다.
>> * Callable: 주요 기능으로 p의 확률로 이미지를 crop 합니다.
>> * 위치: 'padding 후 중앙 crop', 'padding 후 무작위 위치 crop', 'border replicated로 패딩 후 중앙 crop', 'border replicated로 패딩 후 무작위 위치 crop', '중앙 crop', '무작위 위치 crop' 이 6가지 방법을 포함합니다(무작위 설정 가능).
>> * 박스: '원본 비율 유지', '가장 작은 축을 기준으로 정사각형', '모든 축의 무작위 비율' 이 3가지 방법을 포함합니다(무작위 설정 가능).

</br>
</br>
</br>

## B. color
color 기반의 이미지 증강 method들의 모음입니다.
* 해당 코드에는 개발 예정인 상태로 비어 있는 package 입니다.
### 1. base
</br>
</br>
</br>

## C. mask
이미지 증강 알고리즘에서 mask

</br>
</br>
</br>

## D. mixing
* 해당 코드에는 개발 예정인 상태로 비어 있는 package 입니다.

</br>
</br>
</br>

## E. noise
* 해당 코드에는 개발 예정인 상태로 비어 있는 package 입니다.

</br>
</br>
</br>

## F. 외부 라이브러리 의존성
* 해당 코드는 현재 개발중인 단계로 CI/CD 를 위한 외부 라이브러리 의존성 버전 확인이 진행되지 않은 상태입니다.
* 현재 작성되어 있는 각 라이브러리의 버전은 개발 환경의 버전입니다.
> * opencv-python == 4.10.0
> * numpy == 1.26.4
> * GGUtils == 0.0.0
> * GGStatify == 0.0.0