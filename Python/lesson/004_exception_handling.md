# Exception Handling
> - **예상 가능한 예외** : 사전에 인지할 수 있는 예외로 사용자의 입력이나 파일 호출시 파일 없음 발생
> - **예상 불가능한 예외** : 인터프리터 과정에서 발생하는 예외로 주로 개발자의 실수에서 일어난다. _e.g.range error, Zero division_

[🔗 Built-in Exception - Python Document](https://docs.python.org/ko/3.11/library/exceptions.html#bltin-exceptions)

## 예외 처리 `try ~ except`
```py
try:
	예외가 발생할 수 있는 코드
except(에러, 에러, 에러):
	예외가 발생 시 실행할 코드
else :
	예외 발생하지 않은 경우 실행할 코드
finally : 
	예외가 발생을 하던 안하던 항상 실행하는 코드
```

### 0으로 숫자를 나눌 때의 예외처리
```py
for i in range(10):
    try:
        print(10 / i)
    except ZeroDivisionError
        print("Not Division by 0")
```

<img src="https://user-images.githubusercontent.com/55238671/212086234-91929d29-6587-4b7e-a0f8-f17dc40937b9.png" width=400>

> 🔍 모든 예외는 BaseException에서 상속되므로 이 예외를 사용하여 서비스를 수행할 수 있습니다. 
가장 부모가 되는 에러를 하단으로 정해둡니다.

## 강제 예외 발생 `raise`
- `raise` 단계에서 코드를 멈춰주는 역할을 합니다.
```py
raise 예외 타입(예외 정보)
```

### 정수값을 입력하지 않았을 때 강제 예외 발생
```py
while True:
    value = input("변환할 정수값을 입력해주세요")
    for digit in value:
        if digit not in "0123456789": # 숫자가 이 문자열 안에 없을 경우
            raise ValueError("숫자값을 입력하지 않았어요")
    print("정수값으로 변환된 숫자 - ", int(value))
```
## Assert 구문
> 특정 조건에 만족하지 않을 경우(`False`) 예외 발생

```py
assert 예외 조건
```

### 
```py
def get_binary_number(decimal_number):
    assert isinstance(decimal_number, int) # False시, 에러 발생하여 멈춤
    return bin(decimal_number)

print(get_binary_number(10))
```
