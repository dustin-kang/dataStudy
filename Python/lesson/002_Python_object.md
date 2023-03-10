# Object Oriented Programming(OOP)
> π€ κ°μ²΄ μ§ν₯ μΈμ΄μΈ νμ΄μ¬μ μ΄μ©ν΄ μ΄λ ν μ€λΈμ νΈ μ€μ¬μΌλ‘ κ°λ°μ ν΄λ³΄μμ.
> κ°μ²΄ μ§ν₯ νλ‘κ·Έλλ° μΈμ΄λ **μ€κ³ μ€μ¬μ¬κ³ **μ **μ¬μ¬μ©**μ μ€μ΄κ³ μ λ§λ€μ΄μ§ κ²μλλ€. [π](https://www.python.org/doc/essays/omg-darpa-mcc-position/)

<img width="813" alt="image" src="https://user-images.githubusercontent.com/55238671/210976638-f0cab41b-568a-42f6-ad9d-b6db3dd3a496.png">

## ν΄λμ€ λ§λ€κΈ°

### ν΄λμ€ μ μΈνκ³  Attribute μΆκ°νκΈ°
```py
class SoccerPlayer(object):
    def __init__(self, name, position, back_number):
        self.name = name
        self.position = position
        self.back_number = back_number 


son = SoccerPlayer("SON", "FW", 7)
lioris = SoccperPlayer("LIORIS", "GK", 1)
```
- `__init__` : **μμ±μ(Constructor)** λ‘ κ°μ²΄μ **μ΄κΈ°κ°μ μ€μ **ν  λ μ¬μ©νλ©° κ°μ²΄ μμ±κ³Ό λμμ λ©μλλ₯Ό μλμΌλ‘ νΈμΆνλ€. 
- `self.` : κ°μ²΄μ λν μμ±
- `class.` : ν΄λμ€μ λν μμ±
- `self.__` : ν΄λμ€ λ°μμλ μμ μ΄ λΆκ°λ₯ν μμ± 

[π λ€μ λ§ΉκΈλ§(name mangling)](https://blog.naver.com/PostView.naver?blogId=m1nna&logNo=222338251110&from=search&redirect=Log&widgetTypeCall=true&directAccess=false)
[π νμ΄μ¬ Magic Method `__main__`](https://corikachu.github.io/articles/python/python-magic-method)

> π Python Naming Rule
> - snake_case : νμ΄μ¬ ν¨μλ λ³μ
> - CamelCase : νμ΄μ¬ ν΄λμ€

### method κ΅¬ννκΈ°
```py
class SoccerPlayer(object):
    #...
    def change_back_number(self, new_number):
        print("μ μμ λ±λ²νΈλ₯Ό λ³κ²½ν©λλ€. : 
            From %d to %d % \
            (self.back_number, new_number))
        self.back_number = new_number 


kane = SoccerPlayer("KANE", "ST", 9)
kane.change_back_number(10)
```

## μμ (inheritance)
- λΆλͺ¨ ν΄λμ€λΆν° μμ±κ³Ό Methodλ₯Ό λ¬Όλ € λ°λ μμ ν΄λμ€λ₯Ό μμ±νλ κ²μλλ€.
- μμλ°μΌλ €λ©΄ μμ ν΄λμ€ μ΄λ¦ λ€ `(λΆλͺ¨ν΄λμ€)`λ₯Ό λ£μ΄μ£Όλ©΄ λ©λλ€.

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
-  `super().λ©μλ` : `super` λ©μλλ₯Ό ν΅ν΄ κΈ°μ‘΄ κΈ°λ₯μ κ·Έλλ‘ μμ λ°μ μ μμ΅λλ€.
-  λ©μλ μ€λ²λΌμ΄λ© : λΆλͺ¨μ κΈ°λ₯μ κ·Έλλ‘ κ°μ Έμ μ¬μ©νλ κ²μ λ§ν©λλ€. μμ±μλ₯Ό κ·Έλλ‘ κ°μ Έμ κΈ°λ₯μ λ³κ²½νμ¬ μ¬μ©ν  μ μμ΅λλ€.


## λ€νμ± (Polymorphism)
- κ°μ μ΄λ¦ λ©μλμ΄ λ΄λΆ λ‘μ§μ λ€λ₯΄κ² μμ±νλ μ½λ
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

## κ°μμ± (Visibility) = μΊ‘μν or μ λ³΄μλ
- κ°μ²΄ μ λ³΄λ₯Ό λ³Ό μ μλ λ λ²¨μ μ‘°μ νλ κ²μ λ§ν©λλ€.
- λκ΅¬λ κ°μ²΄ μμ λ³μλ₯Ό λͺ¨λ λ³Ό νμ μμΌλ μμ€λ₯Ό λ³΄νΈνκΈ° μν΄ μ¬μ©ν©λλ€.
- `_` : ν΄λμ€ λ΄λΆ λ³μλ κ°μ μ¬μ©νκ³  μΈλΆμμλ μ κ·Όμ΄ κ°λ₯νκ²λ νν
- `__` : ν΄λμ€ λ΄λΆμμλ§ κ΄λ¦¬
```py
class Produuct(object):
    pass

class Inventory(object):
    def __init__(self):
        self.__items = [] # Private λ³μλ‘ μ μΈ νκ°μ²΄κ° μ κ·Όμ λͺ»νκ²ν¨.
    
    def  add_new_item(self, product):
        if type(product) == Product:
            self.__items.append(product)
            print("new item added")
        else :
            rasis ValueError("Invaild Item")

    def get_number_of_items(self):
        return len(self.__items)

```

## μΈμ€ν΄μ€(Instance)

- μΈμ€ν΄μ€(κ°μ²΄)λΌλ μλ―Έ
- **μΈμ€ν΄μ€ λ©μλ** : μΈμ€ν΄μ€ μμ±μ μ κ·Όν  μ μλ λ©μλ `def`
- **ν΄λμ€ λ©μλ** : ν΄λμ€ μμ±μ μ κ·ΌνκΈ° μν λ©μλ `cls` λ₯Ό νλΌλ―Έν°λ‘ λ°λλ€. `@classmethod`
- **μ μ  λ©μλ** : κ°μ²΄(μΈμ€ν΄μ€)λ₯Ό λ§λ€ νμ μλ λ©μλλ‘ `self` λ₯Ό λ°μ§ μλλ€. `@staticmethod`
- **λ§€μ§ λ©μλ** : νΉλ³ν μν©μ νΈμΆνλ ν΄λμ€ μμ μ μν  μ μλ μ€νμ λ©μλ `__μ΄λ¦__`

```python
# ν΄λμ€ λ©μλ
@classmethod
def print_count(cls):
		print(f"{cls.companycode}"

# μ μ  λ©μλ
class Math:
	@staticmethod
	def add(x, y):
			return x + y

# λ§€μ§ λ©μλ __str__ : κ°μ²΄ μΆλ ₯ν  λ μ¬μ©νλ λ©μλ
def __str__(self): 
		return f"{self.age}"

# print(dir(κ°μ²΄))λ₯Ό ν΅ν΄ λ€μν λ©μλλ₯Ό νμΈν  μ μλ€.
```


# ν΄λμ€ νΉλ³ λ©μλ

### `@property`

- ν΄λμ€ λ΄μ λ€λ₯Έ νΉμ±κ³Ό μ°κ΄λ νΉμ±λ€μ κ΄λ¦¬ν  λ μ¬μ©νλ€.

```python
class Person:
	def __init__(self, first_name, last_name):
		 self.first_name = first_name
		 self.last_name = last_name
		 self.full_name = self.first_name + ' ' + self.last_name
```

μ ν΄λμ€λ₯Ό μ¬μ©ν΄μ λ€μμ μ€νν©λλ€.

```python
fred = Person('Fred', 'Williams')

print(fred.first_name)
print(fred.last_name)
print(fred.full_name)
```

μ¬κΈ°μ `first_name`μ  `Ted` λ‘ λ³κ²½νκ² λλ©΄?

```python
fred_first_name = 'Ted'

print(fred.first_name) #=> 'Ted'
print(fred.full_name) #=> 'Fred Williams'
```

μκ°νλλλ‘ `full_name`μΌλ‘ μ΄μ μ΄ λμ§ μμ΅λλ€.

κ·Έλ λ€λ©΄ μ΄λ κ² λ©μλλ₯Ό μ¬μ©ν΄λ΄μλ€.

```python
class Person:
	def __init__(self, first_name, last_name):
		self.first_name = first_name
		self.last_name = last_name

	def full_name(self):
		return self.first_name + ' ' + self.last_name
```

νμ§λ§ ν΄λμ€μ νΉμ±μ΄ μλ νλμ λ©μλλ‘ μ ν΄μΌ ν©λλ€. κ·Έλμ `@property` κ° νμν κ² μλλ€.

```python
class Person:
	def __init__(self, first_name, last_name):
		self.first_name = first_name
		self.last_name = last_name

	@property
	def full_name(self):
		return self.first_name + ' ' + self.last_name
```

μ΄λ κ² `first_name` κ³Ό λμΌνκ² μ κ·Όν  μ μμ΅λλ€.

### `getter` `setter`

μ΄λ²μλ λ°λλ‘ `full_name` μ μ€μ νλ©΄ `first_name` μΌλ‘ λ°κΏμ£Όλ λ°©λ²μλλ€.

λ¬Όλ‘  `@property` λ₯Ό μ¬μ©νλ©΄ ν΄λμ€μ νΉμ±μ λ§λ€μ΄μ£Όμ§λ§ λ λμκ° ν΄λΉ νΉμ±μ κ°μ Έμ€κ±°λ κ°μ μ€μ ν  λ μ’μ΅λλ€.

- `@property` : μ΄λ»κ² κ°μ Έμ¬μ§λ μ ν΄λ¨μΌλ μ€μ ν  νμκ° μλ€.
- `getter` : μ΄λ€ κ²μ κ°μ Έμ¬ λ
- `setter` : κ°μ μ€μ ν΄μ£Όλ νλ β λ³λμ λ©μλλ₯Ό λ§λ λ€. (μ§μ  μ κ·Ό X)

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

ν΄λΉ νΉμ± μ΄λ¦μ μ¬μ©ν΄μ setter λ₯Ό μ€μ ν  μ μμ΅λλ€.

`@full_name.setter` λ κ·Έμ  `full_name` μ λ³κ²½ν  λ μ΄λ»κ² λ°κΎΈλμ§ μλ €μ£Όλ ν¨μμλλ€.

μλλ₯Ό λ³΄μλ©΄ μ μ μμ΅λλ€.

```python
fred = Person('Fred', 'Williams')

print(fred.first_name) #=> 'Fred'
print(fred.full_name) #=> 'Fred Williams'

fred.full_name = 'Ted Bottleneck'

print(fred.first_name) #=> 'Ted'
print(fred.last_name) #=> 'Bottleneck'
print(fred.full_name) #=> 'Ted Bottleneck'
```
