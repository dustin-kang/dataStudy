# File Handling
> - **File System** : OS에서 파일을 저장하는 **트리구조** 저장 체계
> - **Binary File** : 이진법 형식으로 저장된 파일, _e.g. Excel, Words_
> - **Text File** : 문자열 형식으로 저장된 파일 _e.g. Txt, HTML, py_

[🔗 ASCII CODE TABLE](https://ko.wikipedia.org/wiki/ASCII)

## 파일 읽기
- 대상파일이 **같은 디렉토리 경로에 있는 경우** 가능합니다.

<img width="660" alt="image" src="https://user-images.githubusercontent.com/55238671/212094780-c6203a53-c1fc-4e20-915b-e164cdd2d1da.png">


### 실행 시 마다 한 줄 씩 읽어오기
```py
with open("shopping_list.txt", "r") as my_file:
    i = 0
    while True:
        line = my_file.readline()
        if not line: 
            break
        print( str(i) + " ===" + line.replace("\n","")) # 한줄씩 값 출력
        i = i + 1
```

## OS 모듈
```py
import os
os.mkdir("디렉토리")
```
- `os.path.exists("파일명")` : 파일명의 파일이 존재하는지 `Boolean` 반환
- `os.path.isfile('file')` : 파일이 존재하는지 반환
- `os.path.isdir("log")` : 디렉토리 존재 여부 확인

### 소스 파일 옮기기
```py
import shutil

source = "a.txt"
dest = os.path.join("abc", "b.txt") # abc 폴더에 b 텍스트를 합친다.
shutil.copy(source, dest) # 파일 복사 함수

```

```py
import pathlib

cwd = pathlib.Path.cwd() # 현재 디렉토리
cwd.parent() # 부모 디렉토리
lidt(cwd.glob("*")) # 폴더 안 정보 확인
```

## Pickle
- 파이썬의 객체를 영속화하는 내장 객체
- 데이터나 오브젝트등 실행중 정보를 저장하거나 불러와서 사용할 때 사용
- 주로, 정보나 계산 또는 모델 등 활용이 많습니다.

<img src="https://user-images.githubusercontent.com/55238671/212094621-ff8241ff-e964-47f4-a6ea-7ebc3fde7bf2.png" width=500>

> 🔍 데이터베이스 영역에서의 부호화는 트랜잭션의 순서를 맞추는 용어로 사용되기도 합니다.
```py
import pickle

# 객체 쓰기
f = open("list.pickle", "wb") # write binary
test = [1,2,3,4,5]
pickle.dump(test, f)
f.close()

# 객체 읽기
f = open("list.pickle", "rb") # read binary
test_pickle = pickle.load(f)
print(test_pickle)
f.close()
```

> 📌 with 구문을 사용하면 file.close() 를 쓰지 않고  항상 자동으로 호출 할 수 있습니다. 
```py
with open("data.txt","r") as file:
	data = file.read()
```
## Logging
> - 프로그램이 실행되는 동안 일어난 정보를 기록하는 행위
> - 유저의 접근이나 예외, 함수등의 사용됩니다.

- `.debug` : 개발 시 처리 기록을 남겨야하는 로그 정보를 남김 _e.g. 함수호출, 변수사용_
- `.info` : 처리가 진행동안의 정보를 알림 _e.g. 서비 시작과 끝_
- `.warning` : 사용자가 잘못 입력한 정보나 처리는 가능하나 의도치 않은 정보가 들어왔을 때 알림
- `.error` : 잘못된 처리로 인해 에러 발생, 하지만 프로그램은 동작할 수 있을 경우 _e.g.외부서비스 연결 불가, 기록 파일의 부재_
- `.critical` : 잘못된 처리로 데이터 손실이나 프로그램을 동작할 수 없을 때 `_e.g. 파일 삭제됨, 강제 종료_


```py
import logging

if __name__ == "__main__":
    logger.debug("틀렸음.")
```
