# Python Data Structure
> #### <details> <summary> 🤔 데이터 구조 생각해보기 </summary>
> 도서관에 있는 책들은 어떻게 정리할까? 편의점에 있는 재고들은 어떻게 정리되는 걸까? 이렇게 데이터들은 다른 형태들로 정리됩니다. </details>

### 스택 (Stack)

- 나중에 넣은 데이터를 가장 먼저 반환하는 자료 구조입니다. 
- 후입 선출 (LIFO, Last in First Out)
- 데이터의 입력을 **`push`**, `top` 위치에서 출력 **`pop`** 을 합니다.

```py
a = [1, 2, 3, 4, 5]
a.append(7)
a.append(9)
a.pop()
a.pop()
```

### 큐 (Queue)

- 먼저 넣은 데이터를 먼저 반환하는 자료구조입니다.
- 선입선출(FIFO, First In First Out)
- 데이터를 입력할 땐, `enqueue` 데이터를 출력할 땐 `dequeue`

```py
a = [1,2,3,4,5]
a.pop(0)
a.pop(0)
```

### 튜플 (tuple)

- **값의 변경이 불가능**한 리스트
- `()`을 사용하며, 리스트와 같이 연산, 인덱싱, 슬라이싱이 가능합니다.
- 주로 변경되지 않은 데이터인 **학번, 이름, 우편번호등**의 데이터를 저장합니다.

```py
t = (1,2,3)
t + t # (1,2,3,1,2,3)
t * 2 # (1,2,3,1,2,3)
t[1] = 5 # tuple은 값이 변경이 불가능하기 때문에 할당이 되지 않습니다.
```

> 🔍 값이 하나인 Tuple은 반드시 `(1, )` 처럼 `,`를 붙여야 합니다. 일반 정수로 인식하기 때문입니다.

### 집합 (set)
- 값의 **순서 상관없이** 저장되며 **중복되는 데이터는 저장되지 않습니다.**
- `set` 이라는 객체를 선언하여 객체를 생성합니다.
- 수학에서 사용하는 [🔗다양한 집합 연산](https://docs.python.org/3.11/library/stdtypes.html?highlight=set%20union#frozenset.union)등을 지원합니다.
```py
s = set([1,2,3,1,2,3])
s # {1,2,3}
# add, remove, update, discard, clear 등 메서드를 사용할 수 있습니다.
```

### 사전 (Dictionary)
- 데이터를 저장할때 구분지을 수 있는 값과 함께 저장합니다.
- 고유값(`Key`)와 데이터 값(`Value`)를 관리합니다.
- 주민등록 번호, 제품 모델 번호
- 다른 언어에서는 Hash Table이라고 합니다.

```py
student_info = { 20200101:'name_1', 20200302:'name_2'}

student_info[20200101]
student_info[20200101] = 'name_3'
```

--- 

## 📌 Collection 모듈
- List, Tuple, Dict에 대해 Python Built-in 확장 자료 구조
- **편의성과 실행 효율**등을 사용자에게 제공합니다.

### deque
- Stack과 Queue를 지원하는 모듈로 **List에 비해 빠르고 효율적**이다는 특징을 가졌다.
- linked list의 특성과 기존 list 형태 함수를 지원합니다. (`rotate`, `extend` )

```py
from collections import deque

deque_list = deque()
for i in range(5):
    deque_list.append(i)
print(deque_list)
deque_list.appendleft(10)
print(deque_list)
```
[🔗 deque에 관한 공식 도큐먼트](https://docs.python.org/3.11/library/collections.html?highlight=deque#collections.deque)

### defaultdict
- 딕셔너리 타입의 값에 기본 값을 지정, **신규값을 생성시** 사용하는 방법
- `keyerror`를 방지하는 모듈입니다.
- text mining 할 때 유용하게 사용할 수 있습니다.

```py
from collections import defaultdict

a = defaultdict(int) # 빈값의 딕셔너리를 만들 수 있다. (Default Dictionary)
a = defaultdict(lambda : 0) # 기본 값을 0으로 설정
a['A'] = 5
a['B'] = 4
a['C'] += 1 
```

### Counter
- **아이템에 대한 개수**를 계산해 딕셔너리로 리턴한다. **(리스트 → 딕셔너리)**
- 두개의 `Counter` 객체를 `substract`나 집합 연산(`+&|`)로 연산할 수 있습니다.
- `.most_common(n)` : 가장 빈도수가 높은 것 추출

```py
from collections import Counter
vote = [1,2,1,2,3,3,1,1,2]
c = Counter(vote) # Counter 객체 생성
print(c)
# Counter({1:4, 2:3, 3:2})
```

### namedtuple
- Tuple 형태로 **Data 구조체**를 저장하는 방법
- 저장되는 데이터의 변수를 사전에 지정해서 저장합니다.

```py
from collections import namedtuple
Point = namedtuple('Point', ['x','y']) # Point 구조체로 x,y값이 들어감을 약속
p = Point(11, y=22)
print(p[0] + p[1])
```