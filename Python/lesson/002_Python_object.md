# Object Oriented Programming(OOP)
> 🤔 객체 지향 언어인 파이썬을 이용해 어떠한 오브젝트 중심으로 개발을 해보아요.
> 객체 지향 프로그래밍 언어는 **설계 중심사고**와 **재사용**을 줄이고자 만들어진 것입니다. [🔗](https://www.python.org/doc/essays/omg-darpa-mcc-position/)

<img width="813" alt="image" src="https://user-images.githubusercontent.com/55238671/210976638-f0cab41b-568a-42f6-ad9d-b6db3dd3a496.png">

## 클래스 만들기

### 클래스 선언하고 Attribute 추가하기
```py
class SoccerPlayer(object):
    def __init__(self, name, position, back_number):
        self.name = name
        self.position = position
        self.back_number = back_number 


son = SoccerPlayer("SON", "FW", 7)
lioris = SoccperPlayer("LIORIS", "GK", 1)
```
- `__init__` : **생성자(Constructor)** 로 객체의 **초기값을 설정**할 때 사용하며 객체 생성과 동시에 메소드를 자동으로 호출한다. 
- `self.` : 객체에 대한 속성
- `class.` : 클래스에 대한 속성
- `self.__` : 클래스 밖에서는 수정이 불가능한 속성 

[🔗 네임 맹글링(name mangling)](https://blog.naver.com/PostView.naver?blogId=m1nna&logNo=222338251110&from=search&redirect=Log&widgetTypeCall=true&directAccess=false)
[🔗 파이썬 Magic Method `__main__`](https://corikachu.github.io/articles/python/python-magic-method)

> 🔍 Python Naming Rule
> - snake_case : 파이썬 함수나 변수
> - CamelCase : 파이썬 클래스

### method 구현하기
```py
class SoccerPlayer(object):
    #...
    def change_back_number(self, new_number):
        print("선수의 등번호를 변경합니다. : 
            From %d to %d % \
            (self.back_number, new_number))
        self.back_number = new_number 


kane = SoccerPlayer("KANE", "ST", 9)
kane.change_back_number(10)
```

## 상속 (inheritance)
- 부모 클래스부터 속성과 Method를 물려 받는 자식 클래스를 생성하는 것입니다.
- 상속받으려면 자식 클래스 이름 뒤 `(부모클래스)`를 넣어주면 됩니다.

```py
class Person(object):
    def __init__(self, name, age):
        self.name = name
        self.age = age


class Korean(Person):
    pass

first_korean = Korean("DONGWOO", 20)
print(first_korean.name)
```
-  `super().메소드` : `super` 메소드를 통해 기존 기능을 그대로 상속 받을 수 있습니다.
-  메소드 오버라이딩 : 부모의 기능을 그대로 가져와 사용하는 것을 말합니다. 생성자를 그대로 가져와 기능을 변경하여 사용할 수 있습니다.


## 다형성 (Polymorphism)
- 같은 이름 메소드이 내부 로직을 다르게 작성하는 코드
```py
class Animal:
    def __init__(self, name):
        self.name = name
    def talk(self):
        raise NotImplemtedError("")

class Dog(Animal):
    def talk(self):
        return 'Woof! Woof!'

class Cat(Animal):
    def talk(self):
        return 'Meow!'
```

## 가시성 (Visibility) = 캡슐화 or 정보은닉
- 객체 정보를 볼 수 있는 레벨을 조절하는 것을 말합니다.
- 누구나 객체 안에 변수를 모두 볼 필요 없으니 소스를 보호하기 위해 사용합니다.
- `_` : 클래스 내부 변수나 값을 사용하고 외부에서도 접근이 가능하게끔 표현
- `__` : 클래스 내부에서만 관리
```py
class Produuct(object):
    pass

class Inventory(object):
    def __init__(self):
        self.__items = [] # Private 변수로 선언 타객체가 접근을 못하게함.
    
    def  add_new_item(self, product):
        if type(product) == Product:
            self.__items.append(product)
            print("new item added")
        else :
            rasis ValueError("Invaild Item")

    def get_number_of_items(self):
        return len(self.__items)

```

## 인스턴스(Instance)

- 인스턴스(객체)라는 의미
- **인스턴스 메서드** : 인스턴스 속성에 접근할 수 있는 메서드 `def`
- **클래스 메서드** : 클래스 속성에 접근하기 위한 메서드 `cls` 를 파라미터로 받는다. `@classmethod`
- **정적 메서드** : 객체(인스턴스)를 만들 필요 없는 메서드로 `self` 를 받지 않는다. `@staticmethod`
- **매직 메서드** : 특별한 상황에 호출하는 클래스 안에 정의할 수 있는 스페셜 메서드 `__이름__`

```python
# 클래스 메서드
@classmethod
def print_count(cls):
		print(f"{cls.companycode}"

# 정적 메서드
class Math:
	@staticmethod
	def add(x, y):
			return x + y

# 매직 메서드 __str__ : 객체 출력할 때 사용하는 메서드
def __str__(self): 
		return f"{self.age}"

# print(dir(객체))를 통해 다양한 메서드를 확인할 수 있다.
```


# 클래스 특별 메소드

### `@property`

- 클래스 내에 다른 특성과 연관된 특성들을 관리할 때 사용한다.

```python
class Person:
	def __init__(self, first_name, last_name):
		 self.first_name = first_name
		 self.last_name = last_name
		 self.full_name = self.first_name + ' ' + self.last_name
```

위 클래스를 사용해서 다음을 실행합니다.

```python
fred = Person('Fred', 'Williams')

print(fred.first_name)
print(fred.last_name)
print(fred.full_name)
```

여기서 `first_name`을  `Ted` 로 변경하게 되면?

```python
fred_first_name = 'Ted'

print(fred.first_name) #=> 'Ted'
print(fred.full_name) #=> 'Fred Williams'
```

생각하던대로 `full_name`으로 이전이 되지 않습니다.

그렇다면 이렇게 메소드를 사용해봅시다.

```python
class Person:
	def __init__(self, first_name, last_name):
		self.first_name = first_name
		self.last_name = last_name

	def full_name(self):
		return self.first_name + ' ' + self.last_name
```

하지만 클래스의 특성이 아닌 하나의 메소드로 접해야 합니다. 그래서 `@property` 가 필요한 것 입니다.

```python
class Person:
	def __init__(self, first_name, last_name):
		self.first_name = first_name
		self.last_name = last_name

	@property
	def full_name(self):
		return self.first_name + ' ' + self.last_name
```

이렇게 `first_name` 과 동일하게 접근할 수 있습니다.

### `getter` `setter`

이번에는 반대로 `full_name` 을 설정하면 `first_name` 으로 바꿔주는 방법입니다.

물론 `@property` 를 사용하면 클래스의 특성을 만들어주지만 더 나아가 해당 특성을 가져오거나 값을 설정할 때 좋습니다.

- `@property` : 어떻게 가져올지는 정해놨으니 설정할 필요가 없다.
- `getter` : 어떤 것을 가져올 때
- `setter` : 값을 설정해주는 행동 → 별도의 메소드를 만든다. (직접 접근 X)

```python
class Person:
	def __init__(self, first_name, last_name):
		self.first_name = first_name
		self.last_name = last_name

	@property
	def full_name(self):
		return self.first_name + ' ' + self.last_name
		
	@full_name.setter
	def full_name(self, new_full_name):
		first_name, last_name = new_full_name.split()
		self.first_name = first_name
		self.last_name = last_name
```

해당 특성 이름을 사용해서 setter 를 설정할 수 있습니다.

`@full_name.setter` 는 그저 `full_name` 을 변경할 때 어떻게 바꾸는지 알려주는 함수입니다.

아래를 보시면 알 수 있습니다.

```python
fred = Person('Fred', 'Williams')

print(fred.first_name) #=> 'Fred'
print(fred.full_name) #=> 'Fred Williams'

fred.full_name = 'Ted Bottleneck'

print(fred.first_name) #=> 'Ted'
print(fred.last_name) #=> 'Bottleneck'
print(fred.full_name) #=> 'Ted Bottleneck'
```
