> #### **🔍 BoostCourse 자가진단 문제들을 참고했습니다.**

## Contents
- [다음의 조건을 만족하는 행렬 C의 차원은?](https://github.com/dustin-kang/dataStudy/blob/main/DS/Math_warmup.md#1)
- [다음 함수의 도함수로 적절한 것은?](https://github.com/dustin-kang/dataStudy/blob/main/DS/Math_warmup.md#2)
- [벡터의 이해 문제](https://github.com/dustin-kang/dataStudy/blob/main/DS/Math_warmup.md#3)
- [자연로그 문제](https://github.com/dustin-kang/dataStudy/blob/main/DS/Math_warmup.md#4)
- [조건부 확률](https://github.com/dustin-kang/dataStudy/blob/main/DS/Math_warmup.md#5)
---
## #1
#### 다음의 조건을 만족하는 행렬 $C$의 차원(Demension)은?
> $$ C = AB, A \in \mathbb{R}^{10\times256} B \in \mathbb{R}^{256\times1024} $$

<details> <summary>정답</summary>
<strong>10 * 1024</strong>

10 * 256 차원의 행렬 A 와 256 * 1024 차원의 행렬의 곱은 10* 1024 입니다. 
</details>


- [행렬 곱셈 - 위키백과](https://ko.wikipedia.org/wiki/행렬_곱셈)


---

## #2
#### 다음 함수의 도함수로 적절한 것은?
> $$ f(x) = e^x, f'(x) = ? $$

<details> <summary>정답</summary>
<strong>e^x</strong>

도함수 : x에 대한 미분계수를 함수로 나타낸 것.
미분 : 도함수를 구하는 것
즉, 연속함수의 도함수를 구하는 것은 미분계수를 구하는 것과 같습니다. 
</details>


- [도함수의 의미와 구하는법 - 학습지 제작소](https://calcproject.tistory.com/743)


---

## #3
#### 다음 중 틀린 것을 고르시오.
- [ ] 한 벡터에서 다른 벡터를 더하는 것은 원점으로부터의 상대적 위치를 표현한다.
- [ ] 벡터는 숫자르 원소로 가지는 리스트 또는 배열이다.
- [ ] 벡터에 양수인 숫자를 곱해주면 길이만 변한다.
- [ ] 벡터는 원점으로부터 상대적 위치를 표현한다.

<details> <summary>정답</summary>
<strong>한 벡터에서 다른 벡터를 더하는 것은 원점으로부터의 상대적 위치를 표현한다.</strong>

  - 상대적 위치를 표현하는 것이 아니라 한 벡터로부터 상대적 위치 이동을 표현하는 것입니다.

</details>


- [유클리드 벡터](https://ko.wikipedia.org/wiki/유클리드_벡터)


---

## #4
#### 다음 계산한 것으로 적절한 것은?
> $$ \lim_{x \to 0}(1 + x)^{\frac{1}{x}} $$

<details> <summary>정답</summary>
<strong>e</strong>

  x가 1/n이라고 했을 때, n에 대한 함수로 바꾼다면 [자연로그의 밑](https://ko.wikipedia.org/wiki/자연로그의_밑)인 상수 e가 나옵니다.

</details>


- [유클리드 벡터](https://ko.wikipedia.org/wiki/유클리드_벡터)


---

## #5
#### 아래 수식의 물음표에 들어갈 것으로 적절한 것은?
> $$ P(B|A) = ?  $$

- [ ] $\frac{P(B)}{P(A)}$
- [ ] $\frac{P(A)}{P(B)}$
- [ ] $\frac{P(A|B)P(B)}{P(A)}$
- [ ] $\frac{P(A|B)P(A)}{P(B)}$

<details> <summary>정답</summary>
<strong>3번</strong>
 https://ko.wikipedia.org/wiki/조건부_확률

</details>


---

## #6
#### 아래 수식의 물음표에 들어갈 것으로 적절한 것은?
> $$ f(x,y) = xy^2, \frac{\partial f}{\partial x} ?  $$

- [ ] $2xy$
- [ ] $2y$
- [ ] $y^2$
- [ ] $xy^2$

<details> <summary>정답</summary>
<strong>3번</strong>
- 위 partical f/partical x는 x 이외의 변수를 제외하 나머지 변수를 상수로 간주하고 미분하는 것을 말합니다.
- 즉, x를 미분하면 1이므로 y^2만 남게되어 y^2가 되는 것 입니다.

</details>

- [편미분 - 위키백과](https://ko.wikipedia.org/wiki/편미분)
