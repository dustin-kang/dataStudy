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