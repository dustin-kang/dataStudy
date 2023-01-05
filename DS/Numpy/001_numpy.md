# Numpy
> 파이썬의 **고성능 과학 계산용 패키지**로 Matrix와 Vector와 같은 Array 연산을 할 수 있는 파이썬 패키지입니다.

- 일반 List에 비해 빠르고 메모리 효율적입니다.
- 반복문 없이 데이터 배열을 할 수 있습니다. 
- 선형 대수와 관련된 기능을 제공합니다.
- C, C++, 포트란 등의 언어와 통합이 가능합니다.

```
pip insall numpy
import numpy as np
```

[🔗 넘파이 공식 도큐먼트](https://numpy.org/doc/1.24/reference/index.html)

### 배열 생성
```py
test_array = np.array([1, 4, 5, "8"], float) # String 타입을 추가해도 flat으로 자동 형변환.
print(test_array)
type(test_array[3]) # 3번째 인자 인덱싱 
```
- numpy에서 생성한 Array 객체를 `ndarray` 객체라고 합니다.
- **List와 다르게 한 가지의 데이터 type만 배열에 넣을 수 있습니다.**
  
> [🔍 파이썬의 List와 Numpy의 Array의 차이](https://jakevdp.github.io/PythonDataScienceHandbook/02.01-understanding-data-types.html)

### 배열 크기

<img src="https://blog.finxter.com/wp-content/uploads/2021/01/numpy_shape-1-1024x576.jpg" width=600>

- **`shape`** : dimension 크기 구성을 반환함 (Array의 RANK에 따라 불리는 이름이 다릅니다. _scalar, vector, matrix, 3-tensor_), `tuple`

### 배열 데이터 타입
$$ \text{int64 =} 2^{64} \text{로 표현합니다.} $$

```py
np.array([[1, 2, 3,], [3.5, "5", "6"]], dtype=np.float32).nbytes
# 32bits == 4byte -> 6개의 데이터를 4Byte로 표현함. 
# 24
np.array([[1, 2, 3,], [3.5, "5", "6"]], dtype=np.int8).nbytes
#  8bits == 1byte -> 6개의 데이터를 1Byte로 표현함. 
# 6
```
- **`nbytes`** : 차지하는 메모리 크기를 반환함
- **`dtype`** : 데이터 type을 반환함

### 배열 변형
```py
test_matrix = [[1, 2, 3, 4], [1, 2, 5, 8]]
np.array(test_matrix).reshape(1,-1).shape
# (1, 8)
```
- `reshape` : **element 개수는 동일**하나, Array의 shape의 크기를 변경합니다.
  - `reshape(-1,2)` : 사이즈 기반으로 row 개수 선정 (자동적으로)
- `flatten` : 다차원 array를 1차원으로 평평하게 펴주는 역할

### 인덱싱과 슬라이싱
```py
# 인덱싱
a[0, 0] # = a[0][0]

# 슬라이싱
a[: 2:] # 전체 Row와 2열 이상
a[1, 1:3] # 1Row, 1~2 Columns
a[1:3] # 1 ~ 2 Rows 전체
a[:, -1] # 전체 Row의 마지막 컬럼
a[::2,::3] # start, end, step 으로 처음부터 끝까지 2칸 뛰면서, 3칸뛰면서를 의미합니다.
```
- 슬라이싱은 list와 다르게 행과 열을 나눠서 슬라이싱이 가능합니다.

### 범위 지정 
```py
np.arange(0, 5, 0.5) # 0 부터 5까지 0.5씩 건너뛰어라
```

### 영행렬
```py
np.zeros(shape=(10,), dtype=np.int8) 
np.ones(shape=(10,), dtype=np.int8)
np.empty((3,5)) # 메모리가 주어지고 비어있는 공간 (주소값만 채움)

np.ones_like(test_matrix) # 기존 ndarray의 shape 크기만큼 1, 0, empty로 반환.
```

### 항등 행렬(단위 행렬)
```py
np.indentity(n=3, dtype=np.int8)
np.eye(3,5 k=2) # k행부터 시작하여 대각선이 1인 행렬 (k 값이 없으면 단위행렬과 동일)
np.diag(matrix) # 대각선의 숫자들로 행렬을 만듬
```
- 대각선만 1이고 나머지는 0으로 채워져있는 상태

### 샘플링
```py
# 0에서 1까지 10개의 랜덤값을 생성
# 균등 분포
np.random.uniform(0, 1, 10).rehape(2, 5) 
# 정규 분포
np.random.noral(0, 1, 10).reshape(2, 5) 
#
np.random.exponential(scale=2, size=100)
```

## operation
<img src="https://blog.kakaocdn.net/dn/cSoMOs/btqt0a2Dc2y/QhkfwhiWqeUKvNfsM2H29K/img.png" width=600>

- `axis` : 모든 operation 함수를 실행할 때 기준이 되는 dimension 축 _(0,1)_
- `mean`, `std`, `sum` 등 기본 통계함수 뿐만 아니라 수학 함수도 가능합니다.
- 

### 배열 합치기
```py
a = np.array([[1, 2], [3, 4]])
b = np.array([[5, 6]])

b = b[np.newaxis, :]
np.concatenate((a, b.T), axis =1)
# array([[1, 2, 5], [3, 4, 6]])
```

- `vstack` : 행끼리 붙이기
- `hstack` : 열끼리 붙이기
- `concatenate(axis=0)` : 행으로 붙이기
- `concatenate(axis=1)` : 열으로 붙이기
- `np.newaxis` :축을 추가할 때 사용

### Element-wise operations 
- 같은 위치에 element 끼리 연산
```py
matrix_a = np.arange(1, 13).reshape(3, 4)
matrix_a * matrix_a
```

### 행렬 곱(dot product)
<img src="https://i.stack.imgur.com/0N7TO.png" width=500>

- `행렬A.dot(행렬 B)` : 행렬 곱을 하는 연산
- `행렬A.transpose(행렬B)` : `transpose()`이나 `T`를 통해 전치할 수 있다. 
- `matrix + scaler` : 브로드캐스팅 연산이라고 하며 스칼라 합, 스칼라 곱을 말한다. (이외에도 Matrix와 Vector간 연산도 지원한다.)

### timeit : 주피터 환경에서 코드의 퍼포먼스를 체크하는 함수
```py
iternation_max = 10000000
scalar = 2

%timeit [scalar * value for value in range(iternation_max)]
%timeit np.arange(iternation_max) * scalar
```  
- 일반적으로 list comprehension 보다는 numpy가 빠르다.


## Comparisons
> Array 비교

### All, Any
```py
a = np.arange(10)
a < 4 # 전체 element를 4와 비교하여 Boolean으로 나타냅니다.
np.all(a>5)
np.any(a>6)
```
- `any` : 하나라도 조건이 만족한다면 True (OR)
- `all` : 전체가 조건이 만족한다면 True (AND)
- numpy 배열 크기가 동일할 때 element 간 하나하나 비교한다.
- `logical_and(조건1, 조건2)` : 두 조건이 and 조건에 만족한다면 True, 이외에도 `not`과 `or`이 있다.

### Where
```py
np.where(a > 0, 3, 2) # where(condition, True, False)
np.where(a>5) # index 값 반환
np.isnan(a) # 숫자가 아니면 True로 반환
np.isfinite(a) # 발산한 값(np.inf)거나 존재하지 않은 값이 아니면 True 반환
```

### argmax
- `argmax` : 최대값의 인덱스를 반환 (최소값 : `argmin`), `axis` 기반으로 조절할 수 있다.
- `argsort` : 작은 값의 인덱스를 뽑아줌

## Boolean & Fancy Index
### Boolean Index
```py
condition = test_array < 3
a[condition]
```
- 특정 조건에 따른 값을 배열 형태로 추출
- 동일한 shape이어야 합니다.

### fancy Index
- array를 index value로 사용해서 값을 추출합니다.
```py
a = np.array([2, 4, 6, 8], float)
b = np.array([0, 0, 1, 3, 2, 1], int)
a[b]
# array([2., 2., 4., 8., 6., 4.])
```
- `take` 함수를 사용해도 같은 결과가 나옵니다.
- 매트릭스 형태도 사용이 가능합니다. _`a[b,c]`_

## Numpy data I/O
### 데이터 불러오기 / 저장하기
- `loadtxt("root")` : `txt` 파일 호출하기
- `astype(타입)` : 데이터 타입 변환하기
- `savetxt("root/data.csv", 객체, delimiter= "구분자")` :  데이터 파일 저장하기  