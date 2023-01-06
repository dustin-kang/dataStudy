# How to Install Anaconda

### Anaconda 설치 방법
1. [Anaconda 공식 홈페이지](https://www.anaconda.com/products/individual)에서 `Download` 를 클릭 후 설치 합니다.
2. `AnacondaNavigator`를 클릭하시고 Enviorment에서 자신의 Conda 환경을 확인합니다.
3. 또는 터미널에서 `conda`를 입력 후 실행되는지 확인합니다.

만약에 실행되지 않는 경우
```zsh
conda init zsh
# conda init {사용하고 있는 쉘}
```
위 명령어를 통해 제대로 실행되는지 확인합니다.


### 터미널을 통해 주피터 노트북 여는 법
```zsh
$ echo 'export PATH="/opt/anaconda3/bin:$PATH"' >> ~/.bashrc
$ echo 'export PATH="/opt/anaconda3/bin:$PATH"' >> ~/.zshrc
$ source ~/.bashrc
$ source ~/.zshrc
```
echo(입력)한다. 따옴표 안의 내용을 >> ~/.zshrc라는 파일에
source(적용)한다.  ~/.zshrc라는 파일에

> `where conda`를 입력하면 콘다의 위치를 확인할 수 있다.

[참고자료](https://dockyum.tistory.com/39)

### 주피터 노트북 단축키

- 개발환경 테마 변환 : `JupyterLab > Setting > Jupyter Theme`

## 선택 모드의 경우

셀 선택(입력모드) `[enter]`

셀 선택 취소 `[Esc]`

> ⚠️ 셀 선택 취소된 상태에서 사용하세요.
> 

셀 위로 추가 `[a]`

셀 아래로 추가 `[b]`

셀 삭제 `[d] X 2`

셀 잘라내기 `[x]`

셀 복사 `[c]`

셀 아래의 추가하여 붙여넣기 `[v]`

셀과 아래셀과 합체 `[Shift] + [M]`

셀과 윗셀 같이 선택하기 `[Shift + ⬆︎]`

셀과 아래셀 같이 선택하기 `[Shift + ⬇︎]`

Markdown으로 변경 `[m]`

code로 변경 `[y]`

Raw로 변경 `[r]`

파일 저장 `[command/ctrl + s]`

페이지 스크롤 업 `[Shift] + [Space]`

페이지 스크롤 다운 `[Space]`

페이지 영화관 모드 `[Ctrl] + [B]`

## 입력 모드의 경우

선택 셀 코드 전체 선택 `[command] + [a]`

선택 셀 실행 취소 `[command] + [z]`

선택 셀 실행 재실행 `[command] + [y]`

커서 위치 라인 주석 처리 `[command] + [/]`

선택 셀 코드 실행 `[Ctrl] + [Enter]`

선택 셀 코드 실행후 다음 셀로 이동 `[Shift] + [Enter]`

선택 셀 코드 실행후 다음 셀로 추가 이동 `[option/alt] + [Enter]`

커서 시점부터 셀 둘로 나누기 `[Shift] + [Ctrl] + [-]`

도움말확인 `[Shift] + [Tab]`

입력할 코드 찾아보기 `[Tab]`

### 기타 명령어
- `%timeit` : 명령어 이후 함수명을 입력하면 시간을 잴 수 있습니다.
