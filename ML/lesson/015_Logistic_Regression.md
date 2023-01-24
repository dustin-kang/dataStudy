#  Logistic Regression (로지스틱 회귀)

> 거리를 제곱하여 구하는 게 아니라 **어느 카테고리에 속하는지를 예측**하기 위해 0과 1사이의 범위로 나태내어 표현하는 분류 모델입니다. _무한대에서 거리를 구할 수 없기 때문에 최소 제곱법을 사용하지 못합니다._


## 로짓 변환 (Logit Transformation)

<img width="430" alt="image" src="https://user-images.githubusercontent.com/55238671/214308945-1b44783c-2bb6-4c37-ac60-7bf3f0365b5f.png">


- 회귀 계수의 의미를 해석하기 위해 `로짓변환`을 사용하여 비선형 함수를 선형함수로 바꿉니다. 
- 오즈에 로그를 취한 방식이라고 생각하시면 됩니다.

### 오즈(Odds)
오즈는 사건이 발생할 확률을 사건이 발생하지 않을 확률로 나는 비율입니다.

$$ \text{odds} = \frac{p \text{(발생 률, 클래스 1)}}{1-p\text{(발생X 확률, 클래스 0)}}  $$

이는 Feature의 갯수가 증가할 수록 로짓은 얼마나 변하는지를 해석할 수 있습니다.
즉, Feature의 갯수가 증가할 수록 확률이 P배 증가한다고 할 수 있습니다.

[🔗 로지스틱 회귀 - 기내식은수박바](https://soobarkbar.tistory.com/12?category=793437)

## 로지스틱 회귀
- [로지스틱 회귀](https://en.wikipedia.org/wiki/Logistic_regression#Probability_of_passing_an_exam_versus_hours_of_study)는 시그모이드 함수(Sigmoid Function)를 통해 **선형함수를 0과 1사이로 바꾼 것**으로 공식은 아래와 같습니다.

$$ S(x) = \frac{1}{1+e^{-x}} = \frac{e^x}{e^x + 1} $$

$$ H(x) = \frac{1}{1+e^{-(W_x + b)}} = S(W_x + b) = \sigma(W_x + b) $$

```py
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split
frim sklearn.metrics import accuracy_score

model.fit(X_train_scaled, y_train)
y_pred = model.predict(X_val_scaled)
accuracy_score(y_val, y_pred)

### 특성 중요 계수 확인하기
coeff = pd.Series(model.coef_[0], X_train_encoded.columns)
coeff

coeff.sort_values().plot.barh();
```

> #### 💡 분류문제에 선형회귀가 적합하지 않는 이유
> - 예측 값이 확률이 아니기 때문에 클래스를 구분할 수 있는 의미 있는 임계값이 없습니다.
> - 다중 클래스를 가지는 분류 문제로 확장할 수 없습니다.
> - x값에 너무 민감하게 반응하기 때문에 모델을 만들 수 없습니다.
> - [🔗 선형회귀가 분류 문제에 안되는 이유 - TooTouch](https://tootouch.github.io/IML/logistic_regression/#선형-회귀가-분류-문제에-안되는-이유는-무엇인가)
> - [🔗 모두를 위한 딥러닝 - cdjs의 코딩 공부방](https://cding.tistory.com/55)


# Reference
- [💻 로지스틱 회귀 실습 자료]()
- [🔗 5 Reasons “Logistic Regression” should be the first thing you learn when becoming a Data Scientist](https://towardsdatascience.com/5-reasons-logistic-regression-should-be-the-first-thing-you-learn-when-become-a-data-scientist-fcaae46605c4)
- [📼 Logistic Regression Details Pt1: Coefficients](https://youtu.be/vN5cNN2-HWE)
- [📼 Logistic Regression Details Pt 2: Maximum Likelihood](https://youtu.be/BfKanl1aSG0)
- [🔗 로지스틱 회귀 공식문서](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html)
