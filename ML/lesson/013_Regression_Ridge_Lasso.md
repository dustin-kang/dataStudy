# 릿지회귀 라쏘 회귀
[정규화](https://github.com/dustin-kang/dataStudy/blob/main/ML/lesson/007_모델_평가와_모델_개선.md#일반화generalization)의 목적은 모델이 학습 데이터에 Overfitting 되지 않고 처음 보는 테스트 - 데이터에도 좋은 성능을 내도록 하는 것입니다. 이떄 loss 함수에 `L1, L2 항`을  추가하게되면 **기존의 loss도 줄이면서 정규화 항도 줄이는 방향으로 학습**됩니다. 

> 💡 모델의 **피쳐값이 줄어듦에 따라** 특정 피쳐가 너무 큰 값을 갖지 않게 되면서 오버피팅을 방지할 수 있게 됩니다. (패널티를 부여하여 회귀계수가 줄어드는 것입니다.)


람다 값이 증가할 수록 회귀 계수들은 0으로 수렴하게 되는데 이러면 **점점 복잡한 모델에서 단순한 모델이 됩니다**. (단순한 모델이라는 것은 편향을 증가하여 분산을 줄이기 때문에 기울기가 줄어드는 효과가 있습니다.) 

## Lasso (L1 정규화), LAE

$$ L1Loss = \sum^n_{i=1} |y_i - f(x_i)| $$

- 특정 Feature의 값이 매우 낮은 경우(= Outlier) **0이 되는 특징**이 있습니다.
- 즉, 0에 수렴하는 경우는 [Feature Selection](https://github.com/dustin-kang/dataStudy/blob/main/ML/lesson/010_데이터_전처리와_특성선택.md#embedded-method)과 동일하다고 볼 수 있습니다.

### 장단점

- L1 Loss가 0인 지점에서는 미분이 불가능합니다.
- 이상치(Outlier)에 대해 L2 보다 덜 민감합니다. (Robust)

## Ridge (L2 정규화), LSE

$$ L2Loss = \sum^n_{i=1} (y_i - f(x_i))^2 $$

- 0에 수렴까진 하지 않고, 가중치들이 **0에 가깝게 하는 특징(수렴)** 이 있습니다. 
- L1 정규화에 비해 강하지 않게 정규화를 실행하여 선형모델에 일반화 효과를 줄 수 있습니다.

### 장단점


- 이상치(Outlier)에 대해 민감합니다. 최소제곱법 아시죠? (Not very Robust)

[💻 Ridge 회귀 실습]()

## ElasticNet

- L1와 L2의 가중치를 조절하여 만듭니다. 
- 라쏘(Lasso)와 릿지(Ridge)의 최적화 지점이 다르기 때문에 **두 정규화 항을 합쳐서** **r로 규제 정도를 조절**합니다.

> ### Norm?
> Norm은 벡터의 크기를 나타낸 것으로 **L1은 절댓값의 크기, L2는 직선 거리(제곱의 루트)** 를 나타냅니다.



## Reference
- [🔗 딥러닝 용어 정리, L1 Regularization, L2 Regularization 의 이해, 용도와 차이 설명 - 빛나는 나무](https://light-tree.tistory.com/125)
- [🔗 릿지회귀, 라쏘회귀, 엘라스틱넷 - 대학원생이 쉽게 설명해보기](https://hwiyong.tistory.com/93)
- [🔗 L1, L2 Norm, Loss, Regularization? - 생각 정리](https://junklee.tistory.com/29)
- [📼 Regularization Part 1: Ridge (L2) Regression - StatQuest](https://youtu.be/Q81RR3yKn30?t=635)
- [🔗 Sklearn RidgeCV 공식도큐먼트 ](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.RidgeCV.html)
- [🔗 Sklearn Ridge 공식도큐먼트 ](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.Ridge.html#sklearn.linear_model.Ridge)
