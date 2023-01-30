# 모델 해석 (Interpreting ML)
# 부분 의존도 그림(Patial Dependence Plots, PDP)
> 📌 **관측지들(데이터들)** 에 대한 전역적인 설명을 해주는 라이브러리

- 특성에 따라 타켓값이 증가 또는 감소하느냐와 같이 **미치는 영향에 대한 정보**를 알 수 있습니다.


> 💡 즉, 특성 중요도는 특성들의 성능 역할을 알 수 있다면 부분 의존도는 타겟값에 얼마나 영향을 주는지를 파악할 수 있습니다. 주로 복잡한 모델에 사용됩니다.

```py
pip install pdpbox
from pdpbox.pdp import pdp_isolate, pdp_plot
```

## ICE 곡선?
- 하나의 관측치에 대해 특성을 변화하고 이에 따른 타켓의 변화 곡선을 말합니다.
- 이 ICE 곡선들의 평균이 PDP 입니다. [🔗](https://twitter.com/i/status/1066398522608635904)


![Untitled1](https://user-images.githubusercontent.com/55238671/215487942-4ab5f3d0-6c5c-47d3-838c-606cecdae70a.png)

```py
feature = 'annual_inc' #확인할 특성

isolated = pdp_isolate(
		model = linear, # 학습 모델
		dataset = X_val, # 데이터 세트
		model_features = X_val.columns, # 데이터 세트의 특성
		feature = feature, # 타겟과의 관계를 확인할 특성
		grid_type = 'percentile', # 그리드 포인트를 백분위로 할것인지 `equal`처럼 기존과 같이 할것인지.
		num_grid_points = 10 #default : 특성의 변화 값을 grid_point로 나타낸다.(한점마다 예측)
)

pdp_plot(isolated
         , feature_name=feature
         , plot_lines=True # ICE plots 그리기
         , frac_to_plot=0.001 # or 10 (# 10000 val set * 0.001) 플롯할 줄 수를 의미한다.
         , plot_pts_dist=True # 데이터 포인트 분포(바코드) 표시 여부
) 

plt.xlim(20000,150000);

X_val_encoded['annual_inc'].value_counts() # 아래 바코드 모양처럼 데이터의 분포를 확인할 수 있다.
```

## 두 특성간 상호 작용

![Untitled](https://user-images.githubusercontent.com/55238671/215488003-34ade96b-a649-4070-b363-eef7a392d7b4.png)


```py
from pdpbox.pdp import pdp_interact, pdp_interact_plot

features = ['annual_inc', 'fico_range_high']

interaction = pdp_interact(
    model=boosting, 
    dataset=X_val_encoded,
    model_features=X_val.columns, 
    features=features
)

pdp_interact_plot(interaction, plot_type='grid',  
                  feature_names=features);
                  # 시각화 타입은 plot_type으로 설정할 수 있습니다.
```
- `pdp_interact`을 사용하여 두 특성 간의 상호작용을 확인할 수 있습니다. 
- 색이 파랗게 진할 수록 Target 값에 대한 영향이 낮아진다고 판단하면 됩니다. 

## PDP 범주형 특성 사용하기
범주가 있는 특성들은 주로 인코딩을 사용하는데 실제로 인코딩한 값으로 PDP를 그리면 실제 값을 확인하는데 어려움이 있습니다. PDP 카테고리 자동매핑을 통해 
인코딩이 되어 있는지 확인할 수 있습니다.

```py
feature = 'sex'
for item in encoder.mapping:
    if item['col'] == feature:
        feature_mapping = item['mapping'] # Series
        
feature_mapping = feature_mapping[feature_mapping.index.dropna()]
category_names = feature_mapping.index.tolist()
category_codes = feature_mapping.values.tolist()

pdp_dist = pdp.pdp_isolate(
    model= rf,
    dataset = feature_mapping, # 인코딩 데이터
    model_features = features, # 모델의 특성은 원래 특성들을 사용합니다. 
    feature = feature)
pdp.pdp_plot(pdp_dist, feature)

# xticks labels 설정을 인코딩된 코드리스트와, 카테고리 값 리스트를 넣어 수동으로 해보겠습니다.
plt.xticks([1, 2], ['male', 'female',]);

```

### 2D PDP 그리기

```py
# 2D PDP 를 Seaborn Heatmap으로 그리기 위해 데이터프레임으로 만듭니다
# 2D PDP
features = ['sex', 'age']

pdp = interaction.pdp.pivot_table(
	values = 'preds',
	columns = features[0], #sex
	index = features[1] # age
)[::-1]

pdp = pdp.rename(columns=dict(zip(category_codes, category_names)))
plt.figure(figsize=(6,5))
sns.heatmap(pdp, annot=True, fmt='.2f', cmap='viridis')
plt.title('PDP decoded categorical');
```

### 3D
```py
# 2D PDP dataframe, interaction 객체에서 pdp 속성 사용
interaction.pdp

# 위에서 만든 2D PDP를 테이블로 변환(using Pandas, df.pivot_table)하여 사용합니다

pdp = interaction.pdp.pivot_table(
    values='preds', # interaction['preds']
    columns=features[0], 
    index=features[1]
)[::-1] # 인덱스를 역순으로 만드는 slicing입니다

# 양단에 극단적인 annual_inc를 drop 합니다
pdp = pdp.drop(columns=[1764.0, 1500000.0])

import plotly.graph_objs as go

surface = go.Surface(
    x=pdp.columns, 
    y=pdp.index, 
    z=pdp.values
)


layout = go.Layout(
    scene=dict(
        xaxis=dict(title=features[0]), 
        yaxis=dict(title=features[1]), 
        zaxis=dict(title=target)
    )
)

fig = go.Figure(surface, layout)
fig.show()
```


---

# SHAP
> 📌 **개벌 관측지(데이터 하나)**에 대한 지역적인 설명을 해주는 라이브러리

SHAP(Shapley Additive exPlanation)은 블랙 박스를 화이트 박스로 만들어 어떤 **특성들이 어떤 방향으로 얼마나 영향을 주는지** 시각적으로 보여주는 라이브러리입니다.

```py
conda install -c conda-forge shap
# colab : !pip install shap

import shap
```

### Shapley Values
- 어떤 Features가 이 Model에 어느정도를 기여했는가를 나타낼 수 있는 값입니다.
- `shap`을 통해 도표를 시각화 할 수 있습니다.

## Force plot

<img width="800" alt="image" src="https://user-images.githubusercontent.com/55238671/215487889-bff1b221-a498-4eb1-9876-095d6945e0f0.png">


```py
row = X_test.iloc[[1]] # 결과물이 DataFrame을 나오게 특성의 범위를 지정합니다.

explainer = shap.TreeExplainer(model) # Shap value를 계산
# shap_values = explainer.shap_values(row)

shap.initjs # 인라인 자바 스크립트 객체 생성

shap.force_plot(
    base_value = explainer.expected_value # 평균값
    shap_values = explainer.shap_values(row) # Shap Value
    features = row # 데이터(관측치)
)

def predict(bedrooms, bathrooms, longt)
```

- `row` 특성의 범위를 `[:100]` 처럼 넓게 지정할 수 있지만 적게하는 것이 계산 속도를 빨리하는 방법입니다.

## Summary Plot
```py
shap_values = explainer.shap_values(X_test.iloc[:300])
shap.summary_plot(shap_values, X_test.iloc[:300], plot_type='violin')
shap.summary_plot(shap_values, X_test.iloc[:300], plot_type="bar")
```

> 🔍 [Shap 라이브러리](https://shap.readthedocs.io/en/latest/api.html)를 이 외에도 다양한 Plot이 존재합니다.




# Reference
- [🔗 PDP 라이브러리 - Github](https://github.com/SauceCat/PDPbox)
- [🔗 PDP 라이브러리 도큐먼트](https://pdpbox.readthedocs.io/en/latest/api.html)
- [🔗 SHAP 라이브러리 - Github](https://github.com/slundberg/shap)
- [🔗 SHAP 라이브러리 도큐먼트](https://shap.readthedocs.io/en/latest/generated/shap.plots.force.html)
