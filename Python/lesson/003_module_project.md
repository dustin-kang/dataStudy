# Module
## Module

> 프로그램을 사용하는 작은 프로그램의 조각으로 **다른 사람들이 편하게 이용** 하기 위해 모듈화를 하는 편입니다.

- 파이썬의 `.py` 파일을 의미합니다.
- `import`를 이용해 호출이 가능합니다.
- 함수 뿐만 아니라 변수도 생성할 수 있습니다.

fah_converter.py
```py
def convert_c_to_f(celcius_value):
    return celcius_value * 9.0 / 5 + 32
```

module_ex.py
```py
import fah_converter
celsius = float(input())
fahrenheit = fah_converter.convert_c_to_f(celcius)
print(fahrenheit)
```

> 📌 모듈 파일을 이용하려면 같은 디렉토리 안에 있어야 합니다.

### namespace
> 모듈 안에는 함수와 클래스 등이 존재하기 때문에 모듈을 호출할 때 **필요한 내용만 골라 범위를 지정**하는 방법

- `as` : 모듈명의 별칭을 사용합니다.
- `from A import B` : 모듈에서 특정 함수 또는 클래스만 호출합니다. (패키지 - 모듈 가능)
- `from A import *` : 모듈에서 모든 함수 또는 클래스를 호출합니다. (패키지 - 모듈 가능)

### Create Module
> `__main__` 모듈 이름이 저장되는 변수로 직접 실행됬을 때만 출력합니다.
> `__all__` : import 대상에서 어떤 것을 가져와야하는지 정해주는 변수

```py
if __name__ == "__main__": 
    print("이 부분은 모듈에서 직접 실행했을 때만 출력합니다.")
    
print(__name__)
```

### pip requirement
```py
pip freeze > requirements.txt # pip 리스트가 담긴 파일 생성하기
pip install -r requirements.txt # requirements 한번에 설치하기
```

### Built-in Module

> 파이썬에는 내장 모듈과 외부 모듈이 존재합니다.

<details>
    <summary> Python 표준 라이브러리 </summary>

  - 난수(랜덤) : `random`
  - 시간 : `time`, `datetime`
  - 웹 : `urllib.request`
  - 수학 : `math`
  - 실행환경 : `sys`
  - 파일 경로 : `os`
  - 정규표현식 : `re`
</details>

---

## Package
> 모듈을 모아놓은 단위, 하나의 프로그램

- 하나의 대형 프로젝트를 만드는 **코드의 묶음**
- 다양한 모듈들의 합으로 **디렉토리로 연결**됩니다.

### Create Package
- **현재 폴더가 패키지임을 알리는 초기화 스크립트**로 패키지 내에서 가장 먼저 실행합니다.
- `import` 와 `__all__` 키워드를 사용합니다.

```py
# __init__.py

__all__ = ["bgm", "echo"]

from . import bgm
from . import echo
```

```py
# __main__.py

if __name__ = "__main__":
    print()
```

> 🔍 **스크립트와 모듈의 차이** : 스크립트는 프로그램을 작동시키는 코드를 담은 **실행 용도의 파일**입니다.

### package namespace
- `from .A inport add` : 현재 디렉토리(A)에서 add 모듈 호출
- `from ..A.attack import special` : 부모 디렉토리 기준에서 모듈의 함수 호출하는 방법

<details>
    <summary> Install Youtube DL Package </summary>

    import youtube_dl

    ydl_opt = {
        # 'listformats' : True #다운로드가 가능한 모든 포맷들을 출력
        'format' : '399'
        # 'format' : 'best[height<=480]'
        # 'outtmpl' : '%(title)s %(resolution)s.%(ext)s' #파일 이름 자동적으로 바꾸기

    }
    with youtube_dl.YoutubeDL() as ydl:
        ydl.download(['XXXX'])

    - https://github.com/ytdl-org/youtube-dl

</details>

---

## Virtual Enviroment 
### `Virtualenv`
- 가장 대표적인 가상환경 관리 도구

### `conda`
- 사용 가상환경도구로 설치의 용이성이 있다.

[🔗 conda 관련 개념 찾아보기]()