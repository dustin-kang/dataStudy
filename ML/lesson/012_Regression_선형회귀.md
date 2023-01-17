# 선형 회귀 (Linear Regression)
독립변수에 따라 종속변수가 **선형적으로** 변하는 모델을 선형 회귀 모델이라고 합니다. 선형 회귀 모델에는 대표적인 선형 회귀로는 단순 선형회귀, 다항 선형회귀, 다중 선형회귀가 있습니다.

```py
from sklearn.linear_model import LinearRegression
model = LinearRegression()

model.coef_ # 회귀 계수(기울기), a
model.intercept_ # 절편, b
```

> 다항 선형회귀는 기존 단순 선형회귀에서 독립변수(원인)의 차수만 증가한 것을 말합니다.

## 단순 선형 회귀 (Simple Linear Regression)

<img width="512" alt="image" src="https://user-images.githubusercontent.com/55238671/212875091-d6b9f02e-7318-4eaf-843f-6d07a10fa1f2.png">


### 조건
1. 선형성 : 선형을 이루어야 한다.
2. 독립성 : 변수들의 상관관계가 높으면 안된다.
3. 등분산성 : 데이터가 고르게 분포해야한다.
4. 정규성 : 정규분포를 띄어야 한다.

### 장점
- **보간(interpolate)** 를 통해 주어져 있지 않은 점을 예측할 수 있습니다.
- 기존 데이터 범위에 벗어나는 값을 예측하기 위해 **외삽(extrapolate)** 를 이용합니다.

## 다중 선형 회귀 (Multiple Regression)

<img width="650" alt="image" src="https://user-images.githubusercontent.com/55238671/212875124-8fa98d1d-bddd-471b-b3c6-3c5198023c16.png">


직선으로 잡을 수 없는 데이터 패턴을 잡기 위해 **특성이 두개 이상으로 사용하는** 회귀 모델입니다. 

[💻 선형 회귀 실습 파일]()

### 💻 Plotly로 3D Plot 시각화하기

```py

# Matplotlib

import matplotlib.pyplot as plt
import numpy as np
from matplotlib import style

style.use('seaborn-talk')
fig = plt.figure()

## 3d 플롯 만들기
ax = fig.gca(projection = '3d') # 3차원 그래프를 그리는 함수를 호출한다.

ax.scatter(train['GrLivArea'], train['OverallQual'], train['SalePrice']) # 3차원 데이터 기입하기
ax.set_xlabel('GrLivArea', labelpad=12)
ax.set_ylabel('OverallQual', labelpad=10)
ax.set_zlabel('SalePrice', labelpad=20) # 라벨링

plt.suptitle('Housing Prices', fontsize=15)
plt.show()


# Plotly

import plotly.express as px

px.scatter_3d(
    train,
    x = 'GrLivArea',
    y = 'OverallQual',
    z = 'SalePrice',
    title = 'House Prices'
)
```

---

## Reference
- [🔗 Plotly 시각화 툴 공식 도큐먼트](https://plotly.com/python/getting-started/#jupyterlab-support-python-35)
- [🔗 Using Interact](https://ipywidgets.readthedocs.io/en/stable/examples/Using%20Interact.html#Using-Interact)
- [🔗 LinearRegression](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html)
