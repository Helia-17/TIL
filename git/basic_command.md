# git command

> git 기초 명령어 정리



## 설정

### init

+ `git init`
+ 폴더를 git으로 관리하기 위해 `.git` 폴더를 생성하는 명령어
+ 최초에 한번만 실행하면 된다.

### status

- `git status`
- 현재 git의 상태를 출력

### log

- `git log`
- 현재 쌓여있는 commit history를 출력



### diff

+ `git diff`
+ 마지막 commit과 지금 working directory의 상태를 비교
+ `add`전에 찍어야 비교 가능



### remote add

- `git remote add <별명> <주소>`
- staging area에 올라간 파일들을 스냅샷으로 저장



## 조작

### add

- `git add <파일이름>`
  - <파일이름>에 `.`을 입력하면 전체 파일이 추가된다.
- working directory에 있는 파일을 staging area(INDEX)에 올림.



### commit

- `git commit` 
- `-m`은 옵션
  + 옵션을 넣지 않으면 # Please enter the commit message가 뜸
    읽기모드와 쓰기 모드가 있음. 키보드로만 조작. 빠져나오기 : `:wq`(write&quit)
    -> 쓸 일 없도록 옵션 넣을 것
- staging area에 올라간 파일들을 스냅샷으로 저장



### push

- `git push <원격저장소 이름> <올릴 브랜치 이름>`
  - `git push origin master`
- commit history를 원격 저장소에 업로드

## 기타



- 물결표 (~): 보통 홈을 의미