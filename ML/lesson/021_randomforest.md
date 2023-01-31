# 랜덤 포레스트
> [앙상블](https://github.com/dustin-kang/dataStudy/blob/main/ML/lesson/018_Ensemble.md#앙상블ensemble) 방법 중 **배깅(Bagging)** 에 해당하는 대표적인 예입니다.

<img src="https://user-images.githubusercontent.com/55238671/215721310-a1290494-aa7f-499e-8cd1-9719e534e14b.png" width=400>

랜덤포레스트는 트리들의 **편향을 유지**하면서, 여러 데이터셋 또는 경우에 대해 학습하기 때문에 **분산을 감소** 시킬 수 있다는 특징이 있씁니다. 이 때문에 랜덤 포레스트는 과적합 방지에 강한 모델입니다. 

||결정 트리|랜덤 포레스트|
|:--:|:--:|:--:|
|편향 / 분산|작은 편향 / 큰 분산|편향 유지 / 분산 감소 (과적합 방지)|
|노이즈|훈련 데이터에 매우 민감|여러트리의 평균으로 강인 (예측 변동성 감소, 결측치 강건)|

⛔️ 하지만 **데이터 수가 많아지면** 결정트리에 비해 **속도가 크게 떨어지고** 결과에 대한 **해석이 어렵다**는 단점이 있습니다.

> #### 💡 [Bagging 다시보기](https://github.com/dustin-kang/dataStudy/blob/main/ML/lesson/018_Ensemble.md#배깅bagging)
> Booststrap(복원 추출)후 이를 집계하는 방법으로 병렬적으로 데이터를 나누어 여러 개의 모델을 동시에 학습하는 방법입니다. (샘플링 도중 뽑히지 않은 샘플을 테스트 세트라(OOB SET)고 합니다. 이것을 통해 검증합니다.)
> ```py
> pipe.named_steps['randomforestclassifier'].oob_score_
> ```
> - 회귀 문제의 경우 결과들을 평균으로 결과를 냅니다.
> - 분류 문제의 경우 다수결로 가장 많은 모델들이 선택한 범주로 예측합니다.

```py
from ensemble import RandomForestClassifier

model = RandomForestClassifier(n_jobs = -1, random_state=2, oob_score=True)
model.fit(X_train, y_train)
```

- `max_depth` : 깊어질수록 과적합하므로 높은 값부터 천천히 감소시켜야 합니다.
- `n_estimators` : 적을 수록 과소적합, 높을 수록 긴 학습 시간이 요구 되므로 적당히 조정해야합니다.
- `min_samples_leaf` : 과적합의 경우 값을 높여주면 됩니다.
- `max_features` : 줄일 수록 다양한 트리를 생성할 수 있고 높이면 같은 특성(feature)을 사용하는 트리가 많아져 다양성이 줄어듭니다.
- [`class_weight`]() : 데이터가 불균형 클래스 인경우 맞추기위해 사용합니다.
- `n_jobs` : 컴퓨터 환경에서 사용할 프로세스 수를 말합니다. _전체사용 : -1_

## 랜덤 포레스트의 랜덤성
랜덤 포레스트가 트리를 랜덤하게 만드는 과정입니다.
랜덤포레스트는 과적합난 결정트리를을 많이 만들어 평균을 내기 떄문에 과적합이 줄어 성능이 유지하게 되는 것 기억하자!

### 1단계

- `bootstrap = True`
- 랜덤포레스트에서 학습되는 트리들은 배깅(Bagging)을 통해 만들어집니다.
- 랜덤으로 트리의 데이터가 선택된다.

### 2단계

- `max_features = auto`
- 무작위로 선택된 특성들을 가지고 분기를 시작합니다.



# Reference
- [📼 StatQuest 랜덤포레스트](https://www.youtube.com/watch?v=J4Wdy0Wc_xQ&feature=youtu.be)
- [🔗 랜덤포레스트 알고리즘 논문, 수도코드](https://pages.cs.wisc.edu/~matthewb/pages/notes/pdf/ensembles/RandomForests.pdf)
- [🔗 Bagging 알고리즘 - 콩나물](https://m.blog.naver.com/PostView.nhn?blogId=incastle_&logNo=221219689884&proxyReferer=https:%2F%2Fwww.google.com%2F)
- [🔗 머신러닝: Random Forest 특징, 개념, 장점, 단점 - 쵸코쿠키의 연습장](https://jjeongil.tistory.com/908)
- [🔗 Bagging 및 RandomForest 공식 도큐먼트](https://scikit-learn.org/stable/modules/ensemble.html#bagging)
- [🔗 랜덤포레스트 변수 중요도 테스트](https://www.zeileis.org/papers/Lifestat-2008.pdf)
- [💻 랜덤 포레스트 실습파일]()
