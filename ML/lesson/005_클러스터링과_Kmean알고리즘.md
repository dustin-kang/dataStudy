# Clustering (군집화)
> - 라벨이 없는 데이터들을 얼마나 유사한지 확인하는 기법입니다.
> - 정답을 보장할 수 없기 때문에 예측 용도보다 EDA 용도로 많이 사용됩니다.
## 군집화 종류

### Hirerachical (계층적 군집 분석)
![hirerachical](https://user-images.githubusercontent.com/55238671/209803324-cf059d9c-1509-4e0f-b182-13b6f8aefee5.png)

어떠한 포인트에서 **점점 크게 합쳐나가가거나** **점점 클러스터로 나눠가면서** **단계적으로** 클러스터링 하는 방법 (Agglomerative, Divisive)

### Point Assignment (분할 군집 분석)
클러스터의 갯수를 미리 선정한 다음, 하나씩 다시 계산해서 클러스터에 배정하는 방식 **_e.g. K-Means_**

### Hard vs Soft Clustering
<img src="https://user-images.githubusercontent.com/55238671/209803203-4d15d0ce-2e7d-4d98-a6d2-50395e5d3177.png" width=400>

- **Hard** : 데이터는 무조건 하나의 클러스터에만 할당합니다.
- **Soft** : 여러가지의 클러스터에 확률적으로 할당할 수 있습니다.

## 얼마나 유사한지, **Similarity (유사도)**
> 두 데이터들이 얼마나 유사한지 나타내는 척도

- Euclidiean(유클리디안) : $p$와 $q$의 유사성을 직선 거리 방식으로 표현 _e.g. L2Norm_
- Manhattan Distance : 수직, 수평으로만 이동한 거리의 합으로 정의 _e.g.리커트 척도(설문 조사)_
- Cosine(코사인) : 스케일을 고려하지 않고 방향 유사도를 측정하는 상황 _e.g. 상품 추천_
- Jaccard : 이진형 데이터에 적합하며 둘 중 하나라도 1을 가지는 특징 중 일치하는 비율을 고려한다. 
- Matching : 이진형 데이터에 적합,  전체 특징 중 일치하는 비율을 고려

[🔗 여러가지 유사도 측정방법](https://goofcode.github.io/similarity-measure)

> 🔍 **K-means 클러스팅은 유클리디안 방식을 사용한다.**<br> 주로 원 형태를 나타내며 원형이 아닌 경우 최적의 결과를 내기 위해 `CURE` 이나 `DBSCAN`을 사용하는게 적절합니다.

# K- Means 클러스터링
> 특성이 비슷한 데이터를 같은 그룹으로 묶어주는 클러스터링 알고리즘으로, **k 개의 군집 개수를 정해 군집의 중심점을 예측하고 거리를 비교하여 군집을 결정**합니다. (변동이 없을 때 까지 반복한다.)

<img width="1000" alt="image" src="https://user-images.githubusercontent.com/55238671/209803541-885a888a-d213-4d91-9dfd-77ec61f34735.png">


```py
from sklearn.cluster import KMeans
kmean = KMean(n_cluster=3)
kmean.fit(X)

kmean.cluster_centers_ # 중심점 확인 ([x,y])
```
  - `max_iter` : iteration의 반복 수를 의미합니다. 300번 이전에 끝나기 때문에 default 값이 300입니다.
  - `init` : default 값으로 `k-mean++`이 있는데 이는 초기 Centroid를 정하는 방법 중 하나입니다. (iteration 횟수를 좀 더 줄여줄 수 있습니다.)
  - `n_cluster` : 클러스터의 갯수 입니다. 최대 8개입니다.

[🔗 `sklearn.cluster.KMeans` 공식도큐먼트](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.KMeans.html)

### K-means 클러스터링의 단점
- K 를 몇개로 설정하냐에 따라 성능이 달라집니다.
- K 개 군집의 중심점을 예측해야하는데, **어디로 중심을 두냐**에 따라 성능이 달라집니다.
- 데이터가 잘 모여있는 경우에 효과적이지 노이즈가 많은 경우에는 효과적이지 않습니다.

### K 갯수 결정하는 방법
![elbow](https://user-images.githubusercontent.com/55238671/209803452-bf900b59-303e-4b13-80de-ab222e33a602.png)

- Eyeball Method : 사람의 주관적인 판단을 통해 임의로 지정하는 방법
- Metrics : 객관적인 지표로 최적화된 K를 선택하는 방법

```py
sum_of_squared_distances = []
K = range(1, 15)
for k in K: # 15번 학습
    km = KMeans(n_clusters = k)
    km = km.fit(points)

    sum_of_squared_distances.append(km.inertia_) 
```
- `.inertia_`를 이용하여 거리의 합을 확인할 수 있다. 
- 거리의 합이 작아야 유사성이 높다는 것을 알 수 있다. (완만해지기 시작하는 지점)

> 🔍 PCA 이후 군집화를 진행할 수 있지만 해석에 어려움이 있기 때문에 의미도출을 하지 않는 경우에 사용하는 게 좋다.

[💻 K-means 실습 파일 바로가기](https://github.com/dustin-kang/dataStudy/blob/main/ML/practice/005_kmeans_실습.ipynb)


### 실루엣 분석
- 군집화가 효율적으로 잘 되었는지를 평가할 수 있는 지표이지만 정확한 성능 평가는 아닙니다.
- 일반적으로 `score`가 높을 수록 군집화가 잘 됬다고 평가하지만 무조건적인 답은 내릴 수 없습니다.

```py
from sklearn.metrics import silhouette_samples, silhouette_score

score_samples = silhouette_samples(x, labels, metric='유사도') # 실루엣 계수
average_score = silhouette_score(x, labels, metric='유사도', sample_size=None) # 모든 데이터의 평균 실루엣 계수 값

irisDF.groupby('cluster')['score_samples'].mean() # 각 클러스터의 평균 실루엣 계수 값
```
- 전체 실루엣 평균값과 더불어 개별 군집의 편차가 크지 않아야 한다.
- 실루엣 점수가 1에 가까울 수록 좋다.






[🔗 K-means 시각화 시뮬레이션](https://www.naftaliharris.com/blog/visualizing-k-means-clustering/)
[🔗 머신러닝 - 7. K-평균 클러스터링(K-means Clustering) - 귀퉁이 서재](https://bkshin.tistory.com/entry/머신러닝-7-K-평균-군집화-K-means-Clustering)

# 다양한 군집 알고리즘
### Hierarchical (계층적 군집화)
-  **덴드로그램 모형(Dendrogram)** 으로 계층적으로 유사한 그룹끼리 군집화를 수행하는 알고리즘입니다.
- 클러스터 갯수를 선정할 필요 없습니다.
- 데이터 크기가 작은 문제에 적용됩니다.
- `sklearn.cluster.AgglomerativeClustering` 
- [클러스터링(군집화) 정리 - ssseok.log](https://velog.io/@ljs7463/클러스터링)


### Mean Shift (평균이동)
<img src="https://velog.velcdn.com/images%2Fyepark%2Fpost%2F57d1c47f-723e-4c05-bb22-3030a081d510%2F평균이동.PNG">

- 밀도가 가장 높은 쪽으로 군집 중심점이 이동하면서 군집화를 수행한다.
- 일반 업무 기반의 데이터셋 보다는 컴퓨터 비전 영역에서 개체를 구분하거나 움직임을 추척하는데 수행한다.

[💻 평균이동 실습 파일 바로가기](https://github.com/dustin-kang/dataStudy/blob/main/ML/practice/005a_mean_shift_실습.ipynb)

### GMM (Gaussian Mixture Model)
- 데이터가 여러개의 가우시안 분포를 모델로 섞어서 생성한 모델


### DBSCAN
- 밀도 기반 군집화로 복잡한 군집화에 효과적이다.

---
## Reference
- [🔗 [AI] Clustering (군집화) 개념과 알고리즘 종류 - 방구의 개발냄새](https://bangu4.tistory.com/98)
- [🔗 Clustering 개요 - ratsgo's blog](https://ratsgo.github.io/machine%20learning/2017/04/16/clustering/)
- [🔗 [머신러닝 완벽가이드] Chap.7 군집화(2) - yepark.log](https://velog.io/@yepark/머신러닝-완벽가이드-Chap.7-군집화-2)
