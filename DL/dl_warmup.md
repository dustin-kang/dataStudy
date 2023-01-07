> #### **🔍 BoostCourse 자가진단 문제들을 참고했습니다.**

## Contents
- [샘플 수와 배치 사이즈만으로 신경망 모델의 learning step의 수는?](https://github.com/dustin-kang/dataStudy/blob/main/DL/dl_warmup.md#1)
- [다음 중 손실 함수에서 극소 값의 위치를 구하기 위해 사용하는 방법으 고르시오.](https://github.com/dustin-kang/dataStudy/blob/main/DL/dl_warmup.md#2)
- [다음 아래 그래프르 나타내는 활성화 함수는?](https://github.com/dustin-kang/dataStudy/blob/main/DL/dl_warmup.md#3)
- [다음 중 신경망에서 활성화함수가 필요한 가장 적절한 이유는?](https://github.com/dustin-kang/dataStudy/blob/main/DL/dl_warmup.md#4)
- [다음 중 RNN에 대한 설명으로 올바르지 않은 것은?](https://github.com/dustin-kang/dataStudy/blob/main/DL/dl_warmup.md#5)
- [네트워크 파라미터 수에 해당되는 설명 중 틀린 것은?](https://github.com/dustin-kang/dataStudy/blob/main/DL/dl_warmup.md#6)
---
## #1
#### 학습 데이터셋의 총 샘플 수가 10,000개이고 batch size가 100인 신경망(neural network) 모델이 모든 데이터를 학습에 사용하는데 필요한 learning step의 수는?

<details> <summary>정답</summary>
<strong>100</strong>

- Epoch : 전체 Sample 데이터를 한바퀴 돌며 학습하는 것
- Step : 1개의 배치로부터 loss를 계산 후 1회 업데이트 하는 것
- Batch Size : 1 Step에서 사용한 데이터 개수
 
 s * b = n * e
 n : 전체 학습 데이터 수

📌 이해 하기
 n = 1회 운동 당 벤치 프레스 목표 개수 (40개)
e = epochs: 몇 번 반복할 것인가? 1회
b = batch size: 1세트 당 회수. 8개
s = steps: 몇 세트로 나누어 할 것인가. 5 세트
</details>


- [012. Epoch, Step, Batch size 개념 정리 - 사상최강 ](http://esignal.co.kr/ai-ml-dl/?board_name=ai_ml_dl&search_field=fn_title&order_by=fn_pid&order_type=asc&board_page=1&list_type=list&vid=15)

---
## #2
#### 다음 중 손실 함수에서 극소 값의 위치를 구하기 위해 사용하는 방법으 고르시오.

- [ ] 오일러 급수
- [ ] 경사 하강법
- [ ] 경사 상승법
- [ ] SVM

<details> <summary>정답</summary>
<strong> 경사하강법 </strong>
 
 경사하강법은 최적화를 위해 사용하며, 함수의 기울기(경사)를 구하고 경사의 절댓값이 낮은 쪽으로 계속 이동시켜 극소값에 이를 때까지 반복시키는 것입니다. (점점 가중치 변경)
</details>

- [경사하강법 - 공돌의 수학정리노트](https://angeloyeo.github.io/2020/08/16/gradient_descent.html)


---
## #3
#### 다음 아래 그래프르 나타내는 활성화 함수는?

<img src="https://hvidberrrg.github.io/deep_learning/activation_functions/assets/sigmoid_function.png" width=300>

- [ ] ReLU
- [ ] Maxout
- [ ] Dropout
- [ ] Sigmoid

<details> <summary>정답</summary>
<strong> 시그모이드 함수 </strong>
 
 시그모이드 함수는 인공 뉴런에 사용되는 활성화 함수로 로지스틱 함수라고도 합니다.
 0을 넘기면 1에 가깝게 그렇지 않으며 0에 가깝게 가중합을 출력합니다. 
</details>

---
## #4
#### 다음 중 신경망에서 활성화함수가 필요한 가장 적절한 이유는?


- [ ] 계산복잡도를 줄이기 위해
- [ ] 비선형 근사를 하기 위해
- [ ] 수치의 오차를 줄이기 위해
- [ ] 모델 파라미터 수를 늘리기 위해

<details> <summary>정답</summary>
<strong> 비선형 근차를 하기 위해 </strong>
 

모든 활성화 함수의 공통점은 비선형 함수 이다!?
그럼 왜 활성화 함수가 선형이면 안되는 이유가 무엇일까요?
이유는 선형인 활성화 함수 l(x) = ax+b 를 겹겹이 쌓을 때, 
여전히 같은 형태의 함수가 사용하게 됩니다.
즉, 아무리 깊게 쌓아도 이점을 못살린다는 얘기죠.

</details>

---
## #5
#### 다음 중 RNN에 설명으로 올바르지 않은 것은?


- [ ] RNN은 Hidden 노드가 방향을 가진 엣지로 연결되어 순환을 이루는 인공 신경망 구조의 한 종류 이다.
- [ ] RNN은 Input 길이에 비례하여 모델 Parameter를 증가시킨다.
- [ ] RNN은 input 길이가 길어질 수록, 역전파시 그래디언트가 점차 줄어 학습능력이 줄어든다.
- [ ] RNN의 변형 종류로는 GRU, LSTM 등이 있다.

<details> <summary>정답</summary>
<strong> RNN은 Input 길이에 비례하여 모델 Parameter를 증가시킨다. </strong>
- RNN은 연속형 데이터를 잘 처리하기 위해 고안된 신경망입니다. 
- RNN은 Input 길이에 상관없이 **동일한 파라미터** 를 가지고 동작하는 모델입니다. 
</details>

---
## #6
#### 네트워크 파라미터 수에 해당되는 설명 중 틀린 것은? 
다음 그림은 LeNET5의 구조를 도식화한 것이다. M@NxN로 표기된 부분에서 M은 출력 채널 수이고, N은 출력 feature map의 크기이다.
> 예: 첫 번째 convolution 연산 후에 feature map은 총 6개가 생겨나고 각 채널의 feature map 크기는 28x28이다.

이때, 네트워크 파라미터 수에 해당되는 설명 중 틀린 것은?  (단, 입력이미지의 채널은 1, convolution 연산에서의 strides는 모두 1, padding은 없다고 가정한다.)

<img src="https://images.velog.io/images/5050/post/b184f9ee-5898-417b-96cc-41d8c2316c9f/image.png">

- [ ] 첫 번째 convolution layer (C1)의 파라미터 수는 총 156개이다.
- [ ] 두 번째 pooling layer (S2)의 파라미터 수는 총 0개이다.
- [ ] 세 번째 convolution layer (C3)의 파라미터 수는 총 2016개이다.
- [ ] 여섯 번째 full connection layer (F6)의 파라미터 수는 총 10164개이다.

<details> <summary>정답</summary>
<strong> RNN은 Input 길이에 비례하여 모델 Parameter를 증가시킨다. </strong>
 
- CNN과 Convolution 연산 방법에 대한 기본적인 이해가 합니다.
- 세 번째 convolution layer (C3)의 파라미터 수는, 아래 표에 나온 연산에 따라 총 2416개 입니다
 
![mceclip0](https://user-images.githubusercontent.com/55238671/211156524-ff746344-cd21-4689-9e61-62bcc3dcfd24.png)
</details>
