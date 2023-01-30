# 특성 중요도 (Feature Importance)

## 회귀와 분류의 데이터 해석

> - 특성 중요도는 특성들이 **얼마나 모델을 위해 일을 잘하는 지**를 알아내는 것 입니다.
> - 순열 중요도는 기존 특성 중요도보다 더  정확한 계산이 가능합니다.

### 회귀
- Coefficient (회귀계수; 기울기)

> 💡 Correlation은 상관 계수를 의미하며 X와 Y간의 단순 관계를 나타내는 것으로 영향력이랑은 다른 의미입니다.

### 분류
- [Feature Importances(Mean Decrease Impurity, MDI)]() _특성 중요도_
- [Drop-Column Importances]()
- [Permutation Importances(Mean Decrease Accuracy, MDA)]() _순열 중요도_

> 💡 특성 중요도는 비단조(단조롭지 않음), 특성간의 상호 작용, 비선형 특징이 있는 데이터에 용이합니다. _ex. 결정트리_

## 특성 중요도(Feature Importances)

특성들이 **얼마나 일을 잘하내는지** 알아내는 것을 말합니다.

- 특성 중요도는 결과를 주의깊게 봐야되는데 각 특성이 모든트리에 평균 불순도 감도(Mean Decrease impurity)를 계산한 값이기 때문입니다. 
- **범주가 큰 특성(High Cardinarlity)** 들은 편향으로 인해 **과적합과 불순도 감소값이 높게 나오는 현상**이 일어납니다. _State, 시,군,동 등등_ 
- **범주가 큰 특성(High Cardinarlity)** 들은 불순도 감소 값이 높아 상위 랭크에 있다고 해서 그대로 해석하지 않습니다.

```py
importances = pd.Series(model.feature_importances, X_train.columns) # 특성 중요도 구하기
plt.figure(figsize=(10, 20)) # 시각화 생성
importances.sort_value()[-10:].plot.barh(); # 불순도가 큰 상위 10위까지 시각화
```
> ### 🔍 특성상호작용(Feature interactions)
> <img src="" width=400>
> 
> - 특성 중요도가 높은 특성들은 특성 상호 작용이 크게 있습니다. 즉, 시너지 효과라고 생각하시면 편합니다. 아래 데이터에서 볼 수 있듯이 **상호 작용이 있는 경우** 선형모델은 성능이 감소 하지만 **[결정트리]()는** 별 이상이 없습니다. 이유는 결정트리가 출력(Output)만 다를 뿐 **정확도에 영향을 받지 않는 Rule-Based Model 이기 때문입니다.**
>
> - [🔗 특성 상호작용의 대한 링크](https://christophm.github.io/interpretable-ml-book/interaction.html#feature-interaction)

## 순열 중요도(Permutation Importances)

`Drop-Column` 방식 처럼 제거하지 않고 특성값에 무작위로 노이즈를 주어 특성과의 연결 고리를 끊어내는 방식입니다.  (성능 평가지표의 감소량을 측정)

> 성능을 측정면에서 DCI보다 효율적입니다.

```py
## 1. value_counts로 특성의 분포를 확인한다.
feature = 'opinion_seas_risk'
X_val[feature].value_counts()

## 2. 특성의 값을 무작위로 섞는다.
X_val_permuted = X_val.copy()
X_val_permuted[feature] = np.random.RandomState(seed=7).permutation(X_val_permuted[feature])

#.permutaion(list) : 순열 

## 3. 특성 값의 순서가 뒤바뀐 것을 확인합니다
X_val_permuted[feature].head()

# 카테고리들의 분포는 바뀌지는 않았음을 확인합니다
X_val_permuted[feature].value_counts()

# 순열 중요도 값을 얻습니다. (재학습이 필요 없습니다!)
score_permuted = pipe.score(X_val_permuted, y_val)

print(f'검증 정확도 ({feature}): {pipe.score(X_val, y_val)}')
print(f'검증 정확도 (permuted "{feature}"): {score_permuted}')
print(f'순열 중요도: {pipe.score(X_val, y_val) - score_permuted}')
```

>### 💡 Drop-Column Importance(DCI)
> ```py
> pipe.fit(X_train.drop(columns=column), y_train)
> ```
> - 이론적으로는 좋지만 Drop 후 재학습을 해야하는 과정이 있으므로 매우 느립니다.
> - 모든 특성을 한번씩 돌아가면서 제거 하고 트레이닝 하는 방식이라 **데이터가  큰 것은 시간이 오래 걸립니다.**

## 📌 eli5
- `eli5` 라이브러리를 활용하면 **쉽게 순열 중요도를 계산**할 수 있습니다.

```py
!pip install eli5

import eli5
from eli5.sklearn import Permutation Importance
```

### Permuter 정의하고 score 계산하기
```py
import eli5
from eli5.sklearn import PermutationImportance

# permuter 정의
permuter = PermutationImportance(
    pipe.named_steps['rf'], # pipe >> model(rf)
    scoring='accuracy', # metric
    n_iter=5, #다른 random seed를 사용하여 5번 반복
    random_state=2
)

# permuter 계산은 preprocessing 된 X_val을 사용합니다.
X_val_transformed = pipe.named_steps['preprocessing'].transform(X_val) # pipe >> preprocessing

# 실제로 fit 의미보다는 스코어를 다시 계산하는 작업입니다
permuter.fit(X_val_transformed, y_val);

feature_names = X_val.columns.tolist() #Xval의 컬럼 *리스트화*
pd.Series(permuter.feature_importances_, feature_names).sort_values()
# 중요도가 낮은 값부터 나오게 됩니다. 
```

### `show_weights`로 높은 값 정렬하기, Feature Selection
```py
# 특성별 score 확인
eli5.show_weights(
    permuter, 
    top=None, # top n 지정 가능, None 일 경우 모든 특성 
    feature_names=feature_names # list 형식으로 넣어야 합니다
)

print('특성 삭제 전:', X_train.shape, X_val.shape)

minimum_importance = 0.001 # 최소 중요도 (최소 이정도 이상은 넘어야 한다.)
mask = permuter.feature_importances_ > minimum_importance
features = X_train.columns[mask]

X_train_selected = X_train[features]
X_val_selected = X_val[features]

print('특성 삭제 후:', X_train_selected.shape, X_val_selected.shape)
```

### 모델 적용하기
```py
# pipeline 다시 정의
pipe = Pipeline([
    ('preprocessing', make_pipeline(OrdinalEncoder(), SimpleImputer())),
    ('rf', RandomForestClassifier(n_estimators=100, random_state=2, n_jobs=-1)) 
], verbose=1)

pipe.fit(X_train_selected, y_train);

print('검증 정확도: ', pipe.score(X_val_selected, y_val))

# 순열 중요도의 평균 감소값과 그 표준편차의 차가 양수인 특징들을 확인할 수 있습니다.
permuter.feature_importances_ - permuter.feature_importances_std_ > 0
```
- 정확도는 약간 감소했으며, 모델이 더 효율적으로 만들어졌다.



# Reference
- [🔗 특성 중요도 공식 도큐먼트](https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeClassifier.html#sklearn.tree.DecisionTreeClassifier.feature_importances_)
- [🔗 eli5 순열 중요도 도큐먼트](https://eli5.readthedocs.io/en/latest/autodocs/sklearn.html#eli5.sklearn.permutation_importance.PermutationImportance)








