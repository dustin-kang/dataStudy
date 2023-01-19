# 분류 (Classifier)
분류 모델은 **데이터를 카테고리 별로 나누는 모델**을 의미합니다. 명확하게 선으로 나눌 수 있는 **선형 모델**로는 로지스틱 회귀(Rogistic Regression), 서포트 벡터머신(SVM)이 있으며 불규칙하게 흩어진 데이터를 분류하기 위해서(**비선형 모델**)는 커널 서포트 벡터머신과 결정트리 kNN, 랜덤포레스트 등이 있습니다.


> ### 💡 기준 모델 (Baseline Model)
> 모든 데이터가 항상 균형된 데이터라고 생각하시면 안됩니다. 가끔 분류 문제를 해결할 때 타겟 값이 **편중되어 있는 경우가 있기 때문**에 정확도라는 지표만으로 판단하면 안됩니다. _감염자와 비감염자 비율이 1:9니까 정확도 90%이라해서 좋은 성능이라고 판단하면 안됩니다._
> 기준 모델을 세우고 기준 모델보다 좋은 성능이 되게끔 노력해야합니다.
> - 회귀 문제 : 평균값으로 기준 모델을 설정합니다.
> - 분류 문제 : 최대 빈도 값으로 기준 모델을 설정합니다.
> - 시계열 문제 : 이전 시간의 데이터가 기준 모델이 됩니다. 
> 
> 클래스가 많은 경우에도 정확도가 낮아지기 때문에 **회귀 문제**로 풀어야합니다.
> [💻 실습자료]()

## 이진 분류 (Binary Classification)

$$ Log Loss = -(y-\log(p)) + (1-y)\log(1-p) $$

이진 분류기에 대표적인 모델로는 로지스틱 회귀와 서포트 벡터머신이 있습니다. 위 문제를 해결하기 위해서는 시그모이드 함수라는 것을 사용합니다. 

### 시그모이드 함수 (Sigmoid Function)
<img src="https://velog.velcdn.com/images%2Fmetterian%2Fpost%2Fee23f919-20f3-4acd-8110-b39a99df6096%2Fimage-20210413212222497.png" width = 400>



시그모이드 함수는 로지스틱 회귀에서 주로 사용되는데요. 관측값이 특정 클래스에 속할 확률 값을 계산하게 됩니다. 만약 확률값이 기준 값보다 크면 1 아니면 0으로 예측하게 되는 거죠.

[🔗 로지스틱 회귀]()에 대해서는 다음 페이지에서 확인하실 수 있습니다.

## 다중 분류 (Multiclass Classification)

$$ Categorical CrossEntropy = -\frac{1}{N}\sum_{i=1}^N\sum_{j=1}^My_{ij}*\log(p_{ij}) $$

다중 분류는 셋 이상의 클랫를 분류하는 알고리즘입니다. 대표적인 모델로 SGD 분류기, 랜덤 포레스트, 나이브 베이즈 분류기 등이 있습니다. 

> 💡 **이중 분류 알고리즘을 통해 다중 분류를 진행할 수 있는데요.** 그 전략들로 두가지가 있습니다. (이중분류에서 다중 클래스로 확장하는 방법)

### OvR 전략 (One-versus-the-Rest)
- OvA(One-versus-all)이라고 하는 이 알고리즘은 각기 다른 N개의 이진 분류기를 실행 한 후  N개의 클래스를 가진 이미지 분류 시스템을 만드는 것입니다.

### OvO 전략 (One-versus-One)
- 각 숫자의 조합마다 이진 분류기를 실행한 후 가장 많이 선택된 클래스를 선택합니다.
- $  N \text{클래스} = \frac{N *(N-1)}{2}  $

```py
# OVR, OVO를 강제로 사용할 수 있습니다.
from sklearn.multiclass import OneVsRestClassifier
ovr_clf = OneVsRestClassifier(SVC())

```

> 보통 OvR 방법을 선호하지만 일부 알고리즘은 훈련세트의 크기에 민감하기 때문에 작은 훈련 세트에서 많은 분류기를 훈련시키는게 더 빠르기 떄문에 OvO 전략을 선호합니다. 

### 소프트맥스 함수 (Softmax Function)
- 세 개 이상으로 분류를 하는 다중 클래스 분류에서 사용되는 활성화 함수입니다.

$$softmax(z) = [\frac{e^{z1}}{e^{z1}+e^{z2}+e^{z3}}, \frac{e^{z2}}{e^{z1}+e^{z2}+e^{z3}}, \frac{e^{z3}}{e^{z1}+e^{z2}+e^{z3}}] = [p1,p2,p3]$$

> 이외에도 다중 레이블 분류 또는 다중 풀력 분류가 존재합니다.
> - 다중 레이블 분류 : 이진 답을 다중으로 출력하는 분류 시스템 _홀수인지 짝수인지와 8보다 높은 수 인지 분류
> - 다중 출력 분류 : 한 레이블이 여러 클래스가 될 수 있도록 일반화 한 것 입니다. 
> ```py
> y_train_large = (y_train >= 7)
> y_train_odd = (y_train %2 == 1)
> y_multilabel = np.c[y_train_large, y_train_odd]
> knn_clf.fit(X_train, y_nultilabel)
>```

# 평가 지표 (Metrics)
- 분류모델에는 정확도 말고도 다른 평가지표들이 있습니다.

### 정확도(Accuracy)
$$ Accuracy = \frac{Same Predict}{Total Predict} $$
- 모델의 예측이 얼마나 정확한지를 의미합니다. 
- 라벨이 불균형한 데이터에서는 사용하면 안됩니다.

[🔗 정확도 공식 도큐먼트 ](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.accuracy_score.html#sklearn.metrics.accuracy_score)

### 오차 행렬 (Confusion Matrix)

- 위 도표 처럼 주로 이진 분류에서 많이 사용하며 모델이 어떤 오류를 발생시켰는지 알 수 있습니다.

```py
from sklearn.metrics import plot_confusion_matrix, classification_report
print(classification_report(y_val, y_pred))

import matplitlib.pyplot as plt # 그래프 모듈

fig, ax = plt.subplot()
pcm = plot_confusion_matrix(model,
        x_val, y_val,
        cmap = ply.cm.Reds # 컬러테마
        ax = ax # plotting 할 좌표축 객체

plt.title(f'혼동행렬, n={len(y_val}', fontsize=16)
plt.show()

cm = pcm.confusion_matrix
cm
```

- [🔗 Confusion Matrix 공식 도큐먼트](https://scikit-learn.org/stable/auto_examples/model_selection/plot_confusion_matrix.html)

#### 정밀도(Precision), 재현율(Recall)
- 정밀도는 예측을 긍정으로 한 데이터 중에서 실제로 긍정인 비율을 말합니다.
- 재현율은 실제로 긍정인 데이터 중 예측을 긍정으로 한 비율을 말합니다.
- 정밀도와 재현율은 트레이드 오프`TradeOff` 관계를 갖습니다. 그래도 가장 좋은 경우는 두 지표가 적당히 높을 때 인거겠죠?

### F1 Score

$$ F1 =  \frac{2}{\frac{1}{RECALL} + \frac{1}{PRECISION}} = 2 * \frac{PPV * TPR}{PPV + TPR} $$

- 정밀도와 재현율 한쪽에 치우치지 않고 둘 다 **균형을 이루는 것**을 `F1 Score`라고 합니다. 또는 **조화평균(harmonic mean)** 이라고도 합니다.
- 분류 클래스간 **데이터 불균형이 심할 때 주로 사용**합니다.

```py
from sklearn.metrics import classification_report
classification_report(y_val, y_pred)
```

> ### 💡 임계값(Threshold) 조절 하기
> 임계값을 조절하면 정밀도와 재현율을 서로 강조시킬 수 있는 방법입니다.
> ```py
> y_pred_proba = pipe.predict_proba(X_val)[:, 1]
> threshold = 0.5 # 임계값 설정
> y_pred = y_pred_proba > threshold 
>
>ax = sns.histplot(y_pred_proba) # prob 시각화
>ax.axvline(threshold, color='red') # Threshold 시각화
>pd.Series(y_pred).value_counts() # False, True 값 계산
>```

### ROC-커브, AUC
#### ROC-Curve
- **FPR(False Positive Rate)가 변할 때, TPR(True Positive Rate)이 어떻게 변하는지** 곡선으로 나타낸 그래프입니다. 
- FPR = 0 (임계값이 1로 설정된 경우, 모두 부정으로 예측됩니다.)
- FPR = 1 (임계값이 0으로 설정된 경우, 모두 긍정으로 예측됩니다.)

```py
from sklearn.metrics import roc_curve
fpr,tpr, thresholds = roc_curve(y_val, y_pred_proba) # y_true(타겟값), y_score

roc = pd.DataFrame({
    'FPR(Fall-out)': fpr, # 위양성률
    'TPRate(Recall)': tpr, # 재현율
    'Threshold': thresholds # 임계값
})

# ROC 커브 그리기
plt.scatter(fpr, tpr)
plt.title('ROC curve')
plt.xlabel('FPR(Fall-out)')
plt.ylabel('TPR(Recall)');

# 최적의 임계값 찾기
optimal_idx = np.argmax(tpr-fpr) # # threshold 최대값의 인덱스, np.argmax()
optimal_threshold = thresholds[optimal_idx] # 최적의 threshold 값
print('idx:', optimal_idx, ', threshold:', optimal_threshold)
# plt.plot(tpr-fpr);

# 임계값 결과 확인하기
y_pred_optimal = y_pred_proba >= optimal_threshold
print(classification_report(y_val, y_pred_optimal))
```

- [🔗 ROC-Curve 공식 도큐먼트](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.roc_curve.html)
- [💻 ROC 커브 직접 적용해보기 ](http://www.navan.name/roc/)

#### AUC
- AUC는 **ROC 곡선의 너비**를 말합니다. 
- 1에 가까울수록 좋습니다.
- AUC가 높을 수록(왼쪽 위 모서리에 가까울 수록) 좋은 성능이 나온다고 판단합니다.
- 즉, 이 말은 TPR이 높고 FPR이 낮을수록 예측 오류가 낮기 때문에 성능이 잘나온다고 볼 수 있습니다. 

```py
from sklearn.metrics import roc_auc_score
auc_score = roc_auc_score(y_val, y_pred_proba)
auc_score
```

[🔗 auc 공식 도큐먼트](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.roc_auc_score.html#sklearn.metrics.roc_auc_score)

# Reference
- [분류 / 이진분류, 성능측정, 다중분류 - Bo-lim.log](https://velog.io/@bo-lim/분류-이진분류-성능측정-다중분류)
- [[ML] 분류(Classification) - Data Repository](https://wannabenice.tistory.com/11)
- [📼 Introduction to the Confusion Matrix in Classification](https://youtu.be/wpp3VfzgNcI)
- [📼 Precision, Recall & F-Measure](https://www.youtube.com/watch?v=j-EB6RqqjGI)
- [📼 Making sense of the confusion matrix](https://www.youtube.com/watch?v=8Oog7TXHvFY)
- [🔗 Classification metrics](https://stanford.edu/~shervine/teaching/cs-229/cheatsheet-machine-learning-tips-and-tricks#classification-metrics)