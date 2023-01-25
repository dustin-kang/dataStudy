# 결정트리 (Decision Trees)

> 결정트리는 이전 로지스틱 회귀(Logistic Regression)과 다르게 **비선형 모델**이며 비용함수를 최소화하도록 **노드를 분할하는 알고리즘** 입니다.

<img src="https://user-images.githubusercontent.com/55238671/214507276-693775b6-0556-43e5-af82-f6a55bacf9e1.jpg" width=500>


- 결정트리 구조는 특정 수치를 가지고 질문에 대한 답을 찾아가는 스무고개와 비슷한 방식입니다. 
- 결정트리는 회귀, 분류 문제에 둘다 적용이 가능합니다.
- [🔗 결정트리 확인하기](http://www.r2d3.us/visual-intro-to-machine-learning-part-1/)

## 순도와 불순도
결정트리를 이용해 노드를 분할하기위해 **지니불순도(Gini Impurity)** 라는 개념을 이해해야 합니다. _이는 정보이득(IG)와 의미적으로 동일한 말입니다._

<img src="https://user-images.githubusercontent.com/55238671/214506838-30cd10e2-c6e3-4032-ba8c-be8f258957a2.png" width=500>

> - 정보획득 = 엔트로피 감소량
> - 불순도 = 엔트로피
> - 정보획득 = 분할 전 노드 불순도 - 분할 후 노드 불순도

- 만약 서로 다른 유형의 데이터들이 한 공간에 적게 모여 있을 경우, 순도가 높다고 의미합니다. (많이 모여있으면 불순도가 높겠죠.)
- 블순도의 감소 정도는 상대적이지만, 불순도가 가장 많이 감소될수록 많이 순수해지기 떄문에 그만큼 확실히 분류된 정보를 많이 얻을 수 있습니다.
- **분할에 사용할 Feature(Root Node)은 타겟변수(Target)을 잘 구별하는(정보 획득이 큰) 것을 선택합니다.**


## 결정트리 

> 📌 결정트리 모델은 **표준화(StandardScaler)를 할 필요 없는** 규직 기반(Rule-based) 모델입니다. 유의하세요!

```py
from sklearn.tree import DecisionTreeClassifier # 결정트리 객체 임포트

model = DecisionTreeClassifier(random_state=2, criterion='entropy')
# criterion : 노드를 분할하는 방법으로 'entropy'를 지정함.

model.fit(X_train, y_train) # 결정트리 모델 학습
y_pred = model.predict(X_val) # 검증 Features 데이터 셋으로 예측.
axxuracy_score(y_val, y_pred) # 예측 결과 비교

y_val.value_count(normalize=True) # 기준 모델(y_val)의 성능을 비교


# conda install -c conda-forge python-graphviz 

import graphviz
from sklearn.tree import export_graphviz

columns = X_val.columns # 검증 Features 데이터 셋의 Features를 변수로 지정

dot_data = export_graphviz(model,
                        max_depth = 3,
                        feature_names = columns, # 트리 시각화
                        class_names = ['no','yes'],
                        filled = True,
                        proportion=True)

display(graphviz.Source(dot_data))

```
- `criterion` : 노드를 분할하는 방법
- `min_samples_split` : 분기를 만들기 위해 최소한 얼마나 되는 샘플이 노드에 있는지 확인
- `min_samples_leaf` : **마지막 리프노드에 최소한 몇개의 샘플**을 지정할지
- `max_depth` : 트리의 **전체적인 깊이**를 설정


> 📌 나뭇가지가 많아지면 [과적합(Overfitting)](https://github.com/dustin-kang/dataStudy/blob/main/ML/lesson/007_모델_평가와_모델_개선.md#과대적합overfitting)이 일어날 확률이 높습니다.

# Reference
- [🔗 DecisionTree Classifier 공식문서](https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeClassifier.html#sklearn.tree.DecisionTreeClassifier)
- [🔗 DecisionTree Regressor 공식문서](https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeRegressor.html)
- [🔗 Random Forests for Complete Beginners The definitive guide to Random Forests and Decision ](https://victorzhou.com/blog/intro-to-random-forests/)
- [🔗 결정트리의 장단점](https://christophm.github.io/interpretable-ml-book/tree.html#advantages-2)
