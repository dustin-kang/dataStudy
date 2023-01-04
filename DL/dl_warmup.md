> #### **🔍 BoostCourse 자가진단 문제들을 참고했습니다.**

## Contents
- [샘플 수와 배치 사이즈만으로 신경망 모델의 learning step의 수는?](https://github.com/dustin-kang/dataStudy/blob/main/DL/dl_warmup.md#1)

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

