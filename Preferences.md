# CLI

- 명령줄 인터페이스(Command-Line Interface / Command-Line user Interface / Character User Interface)
- (쉘 혹은 콘솔으로 부르기도 함)
- 윈도우에선 CMD, Powershell, 리눅스에선 Terminal

## CMD

## Git Bash

> ###### 디스플레이

- 파란색으로 표시 : 폴더 이름

- Initialized empty Git repository in C:/Users/e~~~e/first-git/.git/

  git 앞에 점 → 숨겨진 폴더인 것을 알 수 있음

- 오른쪽에 마스터! → .git이 있는 위치에서 뜬다고 생각하면 됨

- 아무것도 안나왔다? → 어지간하면 잘 된 것

- 너무 길게 나와서 드래그를 내려도 안보인다? -> 방향키로 가능

> 약속

- 폴더가 ```.```으로 시작한다면 숨겨진 폴더.
- `..`: 상위 폴더, `.`: 현재 폴더(하위 폴더를 포함)
- `*`: anything. ex)`*.log`
- 명령어와 명령어 사이 띄어쓰기 구분 필요
- `pip`: python package manager

> ###### 단축키

- 붙여넣기: Shift + Ins
- 복사: Ctrl + ins
- clear: Ctrl + L
- 특정 상황에서 빠져나가기 : Ctrl + c

| 명령어                                                       |                  기능                   | 비고                                                         |
| ------------------------------------------------------------ | :-------------------------------------: | ------------------------------------------------------------ |
| `$ pwd`                                                      |   내가 어디에 있는지 알아내는 명령어    | Print Working Directory                                      |
| `$ cd`                                                       |       폴더 이동, 더블클릭과 같음        | change directory<br />띄어쓰기 필요<br />`~`: 홈<br />`/`: 루트, 최상위<br />`..`: 상위 폴더<br />`폴더이름/`: 해당 폴더 |
| `$ clear`                                                    |      단축키 Ctrl +L, 내용 다 지움       |                                                              |
| `$ ls`                                                       |              목록 보여주기              |                                                              |
| `$ ls -a`                                                    |     (숨긴 목록 포함) 목록 보여주기      | all의 약자. 다 보여주라는 뜻. 숨김 폴더까지 보여짐           |
| `$ touch test.py `<br />`$ tocuh.test.md`<br />`$ touch a.txt b.txt c.txt` | 파일 생성<br />(파이썬, 마크다운, 다중) | ```$ touch 파일이름.확장자```                                |
| `$ mkdir test`                                               |                폴더 생성                | ```$ mkdir 폴더이름```                                       |
| `$ code .`                                                   |     VS code를 이용해 코드를 열어줌      |                                                              |

##### add, commit, push

> ###### 개념 설명

- `add` : working directory -> index
  - 비유 : 분장실에 있던 파일을 사진을 찍기 전 특정 파일을 무대에 올리는 것
- `remote`:
  - 비유 : 사진을 어떤 무대로 찍을지 지정하는 것
- `commit`:
  - 비유 : 사진에 메모를 작성
  - git이라는 사진사에게 사용자라는 의뢰자가 누군지 알려줘야 함
  - 무대에서 사진을 찍기 때문
  - 잔디심기의 기준!
- `log`
  - 비유 : 사진첩

> ###### 기본 순서

1. 파일 수정 + 저장
2. 변경사항 확인: `git diff`
3. `add` : `git add .` or `git add 파일명.확장자`
4. `commit`대상 확인: `git status` -> (`changes to be committed:` / `changes not staged for commit:`/ `nothing to commit`)
5. `commit` : `git commit -m "파일명.확장자 메모내용"`
6. `push` : `git push origin master`
7. Github 들어가서 확인

| 명령어                                                       | 기능                                     | 부가설명                                                     |
| ------------------------------------------------------------ | ---------------------------------------- | ------------------------------------------------------------ |
| `$ git init`                                                 | `(master)` 지정                          | initialize의 약자. 생성하다.<br />''깃아 나 이제 이 파일을 깃으로 관리할거야''<br />`.git` 안에 숨김 폴더로 항목을 생성해 기능할 수 있도록 함. `ls -a`으로 보면 `.git/`을 볼 수 있음<br />주의 : `~`(home)에서 `git init`을 하는 순간 내 모든 홈폴더 내용이 git으로 관리됨 |
| `$ rm -r .git/`                                              | `(master)` 해제                          | `git init`의 실행 취소                                       |
| `$ git status`                                               | 상태 보기                                | `Changes to be committed`:<br />`modified`: 가 초록색 -> commit 가능<br />`modified`: 가 빨강색 -> commit 불가능, add 필요<br />`nothing added to commit`:<br />add 안했을 확률 높음 |
| `$ get remote add`<br />`$ git remote add origin https://github.com/Helia-17/first-git.git`<br />`$ git remote -v` | 화살표 지정                              | 어떤 곳으로 보낼지 화살표 지정하는 기능<br />보통 1번만 필요 |
| `$ git remote -v`                                            | 화살표 확인                              | `remote`를 점검하는 경우                                     |
| `$ git remote remove origin`                                 | 화살표 해제                              | `remote`를 잘못 지정한 경우                                  |
| `$ git add helloworld.py`<br />`$ git add .`                 | 특정 파일 `add`<br />변경된 파일들 `add` | `add` : git의 sub-command 중 하나                            |
| `git diff`                                                   | 이전 커밋과 현재 상황을 비교하여 보여줌  | `git diff`로 변화를 보고 `git add .`으로 한번에 `add`하면 편함. |
| `$ git commit -m "메모내용"`                                 | `commit`                                 | `-m` : message option, 뺄 수 없음<br /><br />`'파일명.확장자 변경사항'`'<br />~로 시작하면 보통 short name 옵션<br />`Author identity unknown<br/>*** Please tell me who you are.`<br />->이름과 이메일을 등록해야 함<br />`Aborting commit due to empty commit message.` -> 메세지를 남겨야 함<br />`nothing to commit, working tree clean`<br />->무대에 아무도 없다는 말. (안올렸거나 이미 `commit`을 했거나) |
| `$ git config --global user name "Helia"`<br />`$ git config -- global user name "jyk.helia@gmail.com"` | 이름과 이메일 등록                       |                                                              |
| `$ git congif --global -l`                                   | 이름과 이메일 확인                       | `user.email=jyk.helia@gmail.com`<br />`user.name=Helia`      |
| `$ git log`                                                  | `commit`확인                             | 잘 찍혔는지 확인                                             |
| `$ git push origin master`                                   | `push`                                   | 백업의 기능. 매일 하지 않아도 됨(once a month)               |

> ###### ignore

- 필요성 : 계속 필요없는 파일들이 생겨남
- http://gitignore.io/  - 속성 설정 - 생성 - `$ touch .gitignore`



---



# 코드 작성



## VScode 

> ###### 코드

-  스트링은 `''`으로 통일! (`""` x)

- 복사 시 드래그 대신 세 번 클릭하는 습관 들이기, 전체 복사는 ctrl + a

- 마크다운 및 미리보기 가능 but Typora 권장

  | 약어 |          |      |
  | ---- | -------- | ---- |
  | res  | requests |      |
  |      |          |      |
  |      |          |      |

> ###### 터미널

- 방향키 윗키를 누르면 바로 위에 것을 가져옴

- 오타를 방지하기 위해서 자동완성기능을 잘 사용하는 것이좋음

- t를 누르고 tab을 누르면 t를 자동완성해줌.

- 거기서 tab을 두번 누르면 이중에 뭘 입력할건지 보여줌

  | 명령어                         |                     |                           |
  | ------------------------------ | ------------------- | ------------------------- |
  | `$ pip install requests`       | requests 설치       | (도구상자 꺼내기)         |
  | `$ pip install beautifulsoup4` | beautifulsoup4 설치 | 인간이 보기위해 번역 작업 |
  | `$ python 파일명.py`           | 실행                |                           |



## jupyter notebook

- REPL(Read Eval Print Loop) : 
  - 읽고(read), 평가하고(eval), 출력하는(print) 반복(loop)
  - =CLI위에서 사용
- 딥러닝, 머신러닝, 데이터 분석 등에서 자주 사용

> 초기 설정

`$ pip install notebook`

- 글꼴 설정 : D2Coding Ver 1.3.2
  크롬 설정 - 모양 - 글꼴 맞춤설정 - 고정폭 글꼴

|                                                          | 단축키        |                                      |
| -------------------------------------------------------- | ------------- | ------------------------------------ |
| Command Mode -> Edit Mode<br />Edit Mode -> Command Mode | Esc / Enter   | Command mode (파랑)/ Edit Mode(초록) |
| 실행                                                     | Shift + Enter |                                      |
| 위/ 아래에 셀 생성                                       | a/ b          | (above) / (below)                    |
| 셀 제거                                                  | d             | (delete)                             |
| 마크다운 문법                                            | m             | 개념을 적을 수 있음                  |
| Keyboard Shortcuts                                       | h             | (help)                               |

- 커널 초기화 : kernel - Restart
- (업데이트 중단 - 주피터 다운그레이드 필요)목차 생성 확장 프로그램 `$ pip install jupyter_contrib_nbextensions` - Edit - nbextensions config - disable 체크 해제, Table of contents

## Typora

|                               |                         |      |
| ----------------------------- | ----------------------- | ---- |
| 소스코드 화면 / 미리보기 화면 | Ctrl + /                |      |
| 표 삽입                       | Ctrl + t                |      |
| 제목 설정                     | # 또는 Ctrl + 1 ~ 6     |      |
| 코드 입력                     | ``                      |      |
| 인용구                        | > 또는 Ctrl + Shift + q |      |
| 목차 보기 / 숨기기            | Ctrl + Shift + L        |      |



---



# 코드 공개



## Github

- repository : 레포라고 부름, 하나의 폴더 개념
- private / public : public으로 성장 과정을 모두 보여줄 것을 추천
- 폴더 설명 상세히 써서 구분하기 쉽도록 할 것

## Git Lab

+ 최신화
  1. 프로젝트 그대로 가져오기 :`$ git clone https://lab.ssafy.com/05/seoul01/homeworkshop-pull.git` - (Gitlab) clone - Clone with HTTPS
  2. pull : `$ git pull origin master` (전제, 마스터 폴더로 이동해있어야함)



---



# 커뮤니케이션



## Trello

- 카드에 코드 추가: 백틱 세번 + 언어 + 백틱 세번 (ex. ```+ python + yourcode +```
- 카드 삭제: archaive - delete

## Slack

