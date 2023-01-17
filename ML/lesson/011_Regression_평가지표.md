# 회귀 (Regression)
회귀 모델은 두개 이상의 독립변수(원인)에 따라 종속변수(결과)를 예측하는 모델을 의미합니다.
대표적인 회귀 모델로는 선형회귀(Linear Regression), 결정 트리(Decision Tree), kNN 등이 존재 합니다.

> #### 피어슨 상관계수 (Pearson Correlation)
> 피어슨 상관계수는 선형 관계의 강도와 방향을 나타내며 -1부터 1사이의 값을 표시합니다. (0에 가깝다면 선형적 관계가 없다는 겁니다. 그러나 비선형적 관계를 가질 수도 있습니다.)
> 
> <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FDxp4J%2FbtqCsIidh0q%2FaYvZ2Z8sdIaTd6IV4958b1%2Fimg.png" width=300>

## 회귀 모델
최적의 회귀 모델은 가장 잘맞는 최적의 선을 긋는 모델입니다. 여기서, **최적의 선**은 **잔차(residual) 제곱의 합의 최소화**하는 직선을 의미하는데요. 이를 회귀선이라고 부릅니다. 

> - 잔차(residual) : 예측값 - 실제 관측값 (비용 또는 손실이라 생각하면 됩니다.)
> - 잔차 제곱의 합(RSS: Residual sum of Squares = SSE)
> $$RSS = \sum_{i=1}^n (y_i - (\alpha x_i + \beta))^2$$
> - 즉, 잔차 제곱의 합을 최소화 해야하기 때문에 **회귀 모델의 비용함수**가 되는 거죠.

<img width="284" alt="image" src="https://user-images.githubusercontent.com/55238671/212865134-deadf539-cf7b-44ee-9483-25bbfbc376a2.png">


## 최소 제곱법(OLS, Ordinary Least Squares)
최소 제곱법이 갑자기 등장했을 거라 생각하지만, 잔차 제곱의 합을 최소화하는 방법을 최소 제곱합 또는 최소자승법이라고 부릅니다. 즉, **최소 제곱법으로 데이터를 잘 표현하는 선형 회귀선을 그릴 수 있는겁니다.**

이 공식을 통해서 최소화하는 변수(가중치)를 추정할 수 있습니다.

<img width="727" alt="image" src="https://user-images.githubusercontent.com/55238671/212865192-5a52f506-9b5f-4e4f-8fb1-adb197751968.png">


> 💡 OLS는 이상치에 영향력이 크기 때문에 이상치가 있는 경우에는 그다지 좋지 않습니다. 왜냐하면 전체 합에 영향을 주기 때문이죠.
>
> 


## 평가 지표 (Metrics)
### MAE(Mean Absolute Error, 절대 평균 오차)
  - 예측값과 실제값들의 차이의 **절대값의 평균**을 말합니다.
  - 단위가 같은 데이터 해석에 용이합니다. (단위 스케일이 변하지 않습니다.)
  - 주로, 모델을 구별하는 용도로 사용합니다.
  - `np.abs(np.substract(x,y)).mean()`


$$ \frac{1}{n}\sum_{i=1}^n|y_i - \hat y_i| $$

### MSE(Mean Square Error, 평균 제곱 오차)
  - 예측값과 실제값들의 차이의 **제곱의 평균**을 말합니다.
  - 제곱을 했기 때문에 **이상치나 특이값에 민감**합니다.
  - 어떻게 오류가 발생했는지 알 수 없습니다.
  - `np.square(np.substract(x,y)).mean()`


$$ \frac{1}{n}\sum_{i=1}^n(y_i - \hat y_i)^2 $$

### RMSE(Root Mean Square Error, 평균 제곱근 오차)
  - **MSE의 오류 민감도를 개선**하기 위해 사용하며, 제곱으로 스케일된 값을 되돌리는데 사용합니다.
  - 큰 오류에 대해 가중치를 부여하는 방식입니다.


$$ \sqrt {MSE} $$

### RMSLE(Root Mean Square Logarithmic Error, 평균 제곱근 로그 오차)
  - RMSE와 비슷한 공식이지만, 예측값과 정닶값에 **각각 로그를 씌워 계산**한다는 것에 차이가 있습니다.

$$ \sqrt {\frac{1}{n}\sum_{i=1}^n(\log(y_i + 1) - \log(\hat y_i + 1))^2} $$


### R-Squared (coefficient of Determination, 결정계수)
  - **모형의 설명력**을 의미합니다.
  - 분산을 기반으로 예측성능을 평가하는 지표를 말하며, **1에 가까울 수록 설명력이 좋다고 판단**한다.
  - 회귀선에서 설명되는 오차 / 전체 오차

$$ 1 - \frac{\sum_{i=1}^n(y_i -\hat y_i)^2}{\sum_{i=1}^n(y_i -\bar y_i)^2} = 1 - \frac{SSE}{SST} = \frac{SSR}{SST} = \frac{\sum_{i=1}^n(\hat y_i -\bar y_i)}{\sum_{i=1}^n(y_i -\bar y_i)^2} $$


> - SSE(RSS) : 관측치와 예측치 차이 제곱 평균
> - SSR : 예측치와 평균 차이 제곱 평균
> - SST : 관측치와 평균 차이 SSE + SSR

### 수정된 결정계수
위 공식은 실제로 모형이 설명력이 높은 건지 아니면 독립변수들의 개수가 많은 건지 **신뢰를 할 수 없는 문제**가 발생합니다. 이를 **해결**하기 위해 아래 수정된 결정계수로 문제를 해결합니다.

- 표본의 크기는 $n$, 독립변수의 수는 $p$로 정의합니다.
- 주로 단순 회귀보다 다중 회귀 분석에서 이 식이 사용됩니다. 

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbzVAKA%2FbtqAZPjxN7O%2FRfR1KgULS95W2ETHkueYX1%2Fimg.png">

$$ AdjR^2 = 1 - \frac{n -1}{(n-p-1)(1-R^2)} $$

> 결정계수는 독립변수의 개수가 많아질수록 결정계수가 1에 가까워집니다.

## Reference
- [🔗 DATA - 17. 최소자승법(OLS)을 활용한 단순 선형 회귀 (Simple Linear Regression) - 귀퉁이 서재](https://bkshin.tistory.com/entry/DATA-17-Regression)
- [🔗 [결정계수] R square와 adjusted R square - specialsence](https://specialscene.tistory.com/63)
- [🔗 3 Best metrics to evaluate Regression Model? - Songhao Wu](https://towardsdatascience.com/what-are-the-best-metrics-to-evaluate-your-regression-model-418ca481755b)
- [📼 How to calculate linear regression using least square method](https://www.youtube.com/watch?v=JvS2triCgOY)
- [📼 An Introduction to Linear Regression Analysis](https://www.youtube.com/watch?v=zPG4NjIkCjc)
- [🔗 Python Data Science Handbook, Chapter 5.2: Introducing Scikit-Learn](https://jakevdp.github.io/PythonDataScienceHandbook/05.02-introducing-scikit-learn.html#Basics-of-the-API)
- [🔗 2.4.2.2. Supervised Learning](https://ogrisel.github.io/scikit-learn.org/sklearn-tutorial/tutorial/text_analytics/general_concepts.html#supervised-learning-model-fit-x-y)
- [🔗 sklearn.linear_model.LinearRegression](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html)
- [🔗 sklearn.metrics.mean_absolute_error](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.mean_absolute_error.html)
