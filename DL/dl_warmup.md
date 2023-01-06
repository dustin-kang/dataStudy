> #### **🔍 BoostCourse 자가진단 문제들을 참고했습니다.**

## Contents
- [샘플 수와 배치 사이즈만으로 신경망 모델의 learning step의 수는?](https://github.com/dustin-kang/dataStudy/blob/main/DL/dl_warmup.md#1)
- [다음 중 손실 함수에서 극소 값의 위치를 구하기 위해 사용하는 방법으 고르시오.](https://github.com/dustin-kang/dataStudy/blob/main/DL/dl_warmup.md#2)
- [다음 아래 그래프르 나타내는 활성화 함수는?](https://github.com/dustin-kang/dataStudy/blob/main/DL/dl_warmup.md#3)
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
