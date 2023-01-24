# 퍼셉트론 과 인공신경망

# 퍼셉트론(Perceptron)
> 신경망을 이루는 가장 기본적인 단위로 **다수의 신호를 입력받아 하나의 신호를 출력하는 구조** 입니다.

<img width="473" alt="image" src="https://user-images.githubusercontent.com/55238671/214320918-465db793-669d-4659-923d-463a7e990921.png">


## 1단계) 가중합 (Weighted Sum)
입력된 신호(X)에 가중치(w)를 곱하고 그 결과들을 합하여 반환하는 단계
$$ \sum(b + w_0x_0 + w_1x_1 + ... + w_nx_n)$$

```py
import numpy as np

input = np.array([1, 2, 3]) # 입력 신호
weight = np.array([0.2, 0.3, -0.1]) # 가중치

np.dot(input, weight) # 내적 연산을 통해서 가중합이 이루어집니다.
# (1*0.2) + (2*0.3) + (3*-0.1) = 0.5
```
`np.dot`을 이용해 가중합을 만들 수 있습니다. 

> #### 📌 가중치(weight)
> -  인공지능이 점차 학습을 할수록 최적의 답을 유도해나가는 값입니다. 
> - 답과 가깝지 않은 노드와의 연결은 해제하고 수정해가며 최적의 값을 찾아나가는 거죠.

## 2단계) 활성화 함수(Activation Function)
데이터의 패턴을 더욱 잘 학습하게끔 가중합을 **얼마 만큼 신호를 출력할지** 결정합니다. 

### 활성화 함수의 종류

- 모든 활성화 함수는 비선형 함수 입니다. 선형함수는 아무리 깊게 쌓아도 같은 형태이기 때문에 이점을 못 살리기 때문이죠.

<img width="616" alt="image" src="https://user-images.githubusercontent.com/55238671/214321632-5fb8069a-12a6-4acf-b6bb-4a37499ea6ca.png">


|종류|배경|특징|
|:---:|:---:|:---:|
|계단함수 (Step)||0을 넘기면 1, 그렇지 않으면 0 (임계값 지점(0.5)은 미분이 불가능)|
|시그모이드 (Sigmoid)|미분이 가능해짐|	0을 넘기면 1에 가깝게, 그렇지않으면 0에 가깝게 (모든 지점에서 미분 가능)|
|ReLU|[기울기 소실 문제]() 해결| 양의 값은 그대로, 음의 값은 0으로 반환|
|SoftMax||다중분류 문제의 적용, 모든 클래스 확률의 합이 1로 변환 |

> #### 💡 기울기 소실 문제
> - 기울기 소실 문제는 활성화 함수의 미분값이 0에 가까워져서 학습이 잘 안되는 현상을 말합니다. (작은 값이 곱해지게 되면 점점 값이 작아집니다.)
> - 반면 `ReLU`는 층이 곱해지더라도 기울기가 과도하게 커지거나 작아지는 문제는 발생하지 않습니다. 

> #### 💡 퍼셉트론의 한계
> - XOR 게이트 문제를 해결하기 위해 **2개 이상의 경계나 곡선을 사용하면** 선형 분류기로 XOR 게이트 문제를 해결할 수 있습니다.
> - 위 그림을 보시면 NAND 를 분류하는 직선과 `OR` 를 분류하는 직선을 `AND(교차)`하면 XOR 연산을 만족합니다.
> - 즉, 이 얘기는 **여러 층을 쌓아서 XOR 문제를 해결할 수 있듯, 퍼셉트론을 여러층 쌓아 문제를 해결할 수 있는 것이죠.**

---

# 인공 신경망(ANN)
> - 딥러닝 기술은 인공 신경망의 층을 **깊게 쌓은 것**을 가리 킵니다.
> - 그리고 **인공 신경망**은 퍼셉트론을 여러 층을 쌓아서 만든 것 입니다.
> - 이렇게 퍼셉트론을 여러 층을 쌓아 구축한 신경망을 **다층 퍼셉트론 신경망(MLP)** 이라고 합니다.

<img width="300" alt="image" src="https://user-images.githubusercontent.com/55238671/214321676-82b430c3-a284-447b-b08d-52a2abe584ab.png">


## 입력층 (Input Layer)
> 값을 전달하는 역할을 합니다.

- 데이터의 특성(Features)에 따라 노드 수가 결정됩니다.
- 신경망의 층을 셀 때 포함하지 않습니다.

## 은닉층 (Hidden Layer)
> 입력된 신호로 **가중치와 편향이 연산되는 층(가중합)** 입니다.

- 원하는 대로 입력이 가능하고 **통상 2개 이상**이어야 딥러닝이라고 합니다.

> #### 💡 가중치 행렬 구하기
> - 가중치 구하는 방법 :  입력층 갯수 + 은닉층 갯수
> - 가중치 행렬 구하는 방법 :  (이전 층 노드, 다음 층 노드)

## 출력층 (Output Layer)
> 연산이 끝나면 출력되는 층입니다.

- 문제 종류에 따라 활성화 함수, 노드가 달라지게 됩니다.

|문제 종류|활성화 함수|출력층의 노드 수|모듈|
|:---:|:---:|:---:|:---|
|이진 분류|시그모이드 함수|1개(0과 1 사이의 확률)|`binary_crossentropy`|
|다중 분류|소프트맥스 함수|레이블의 클래스(class) 수|`sparse_categorical_crossentropy`|
|회귀 |X|출력값의 특성(Feature) 수와 동일|`mse`|


# Reference
- [🔗 Tensorflow Playground](https://playground.tensorflow.org/#activation=tanh&batchSize=10&dataset=circle&regDataset=reg-plane&learningRate=0.03&regularizationRate=0&noise=0&networkShape=4,2&seed=0.84579&showTestData=false&discretize=false&percTrainData=50&x=true&y=true&xTimesY=false&xSquared=false&ySquared=false&cosX=false&sinX=false&cosY=false&sinY=false&collectStats=false&problem=classification&initZero=false&hideText=false)
- [🔗 다양한 신경망의 구조들 - the Neural Network Zoo](https://www.asimovinstitute.org/neural-network-zoo/)
- [💻 MNIST 손글씨 예제 실습]()
